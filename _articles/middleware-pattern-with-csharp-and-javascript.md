---
layout: article
permalink:
name:
file_type:
title:
description: >-
  Enterprise Integration with Middleware Pattern,
tags:  
category:  
sort_order: 24
rating: 100
changefreq: monthly
priority: 0.5
published: true
create_date: 2017-10-23T10:20:00Z
modified_date: 2017-10-23
created_by: atilla
modified_by: atilla
comments: true
redirect_url:
---

# Enterprise Integration with Middleware Pattern

- Middleware Pattern is a practice-proven solution to recurring technical challenges within a given context
- The middleware pattern is an other variation of the Chain of Responsibility Pattern (CoR) pattern in which a chain of functions are used to handle an incoming event.
- Middleware Pattern is very useful in enterprise architecture projects
- Middleware reminds of software suites that shield developers from having to deal with many of the low-level and difficult issues, allowing developers to concentrate on business logic.
- These tasks are not business logic of an application. Instead, they are "cross cutting concerns" applicable throughout the application and affecting the entire application.


## Back-End implementations

### Simple middleware implementation

it is published on  [https://github.com/atillatan/ChainOfResponsibility](https://github.com/atillatan/ChainOfResponsibility)

Startup class

```csharp
public class Program
{
    private static AppBuilder app = new AppBuilder();

    public static void Main(string[] args)
    {
        app.Use(new LogManager())
           .Use(new AuthorizationManager())
           .UseCacheManager();

        //Run
        app.Run("data");
    }
}
```

Abstract Middleware class

```csharp
public abstract class Middleware
{
    protected Middleware next;

    public Middleware Use(Middleware middleware)
    {
        this.next = middleware;
        return middleware;
    }

    public abstract void Run(object request);
}
```

and AppBuilder class it is a first chain


```csharp
public class AppBuilder : Middleware
{
    public AppBuilder()
    {
    }

    public override void Run(object request)
    {
        Console.WriteLine("Begin AppBuilder.");

        next?.Run(request);

        Console.WriteLine("End AppBuilder.");

        Console.ReadKey();
    }
}
```

Next chain is LogManager class



```csharp
public class LogManager : Middleware
{
    public LogManager()
    {
    }

    public override void Run(object request)
    {
        Console.WriteLine("Begin LogManager.");

        next?.Run(request);

        Console.WriteLine("End LogManager.");
    }
}
```

Next chain is AuthorizationManager class

```csharp
public class AuthorizationManager : Middleware
{
    public AuthorizationManager()
    {
    }

    public override void Run(object request)
    {
        Console.WriteLine("Begin AuthorizationManager.");

        next?.Run(request);

        Console.WriteLine("End AuthorizationManager.");
    }
}
```

next chain is CacheManager

```csharp
public class CacheManager : Middleware
{
    public CacheManager()
    {
    }

    public override void Run(object request)
    {
        Console.WriteLine("Begin CacheManager.");

        next?.Run(request);

        Console.WriteLine("End CacheManager.");
    }
}

public static class CacheManagerExtension
{
    public static Middleware UseCacheManager(this Middleware middleware)
    {
        return middleware.Use(new CacheManager());
    }
}
```

### Advanced Middleware implementation (.net core implementation)

[https://github.com/atillatan/robo-middleware-framework](https://github.com/atillatan/robo-middleware-framework)

```csharp
public class Program
    {
        public static void Main(string[] args)
        {
            IApplicationBuilder app = Application.Current.appBuilder;

            app.UseMiddleware<LoggerManager>("param1", "param2");

            app.UseMiddleware<CacheManager>();

            app.Use(next =>
            {
                return async invokeContext =>
                {
                    Console.WriteLine("Begin Inline middleware");

                    await next(invokeContext);

                    Console.WriteLine("End Inline middleware");
                };
            });

            app.UseMiddleware<Invoker>();

            Application.Current.Build();

            //// Example Method Call ////

            PersonService personService = new PersonService();

            var result = personService.Invoke<string>(() => personService.Method1(3));

            Console.ReadKey();
        }
    }
```

```csharp
public interface IApplicationBuilder
    {
        InvokeDelegate Build();

        IApplicationBuilder Use(Func<InvokeDelegate, InvokeDelegate> middleware);

        IDictionary<string, object> Properties { get; }

        IApplicationBuilder New();
    }
```

```csharp
public class ApplicationBuilder : IApplicationBuilder
    {
        public readonly IList<Func<InvokeDelegate, InvokeDelegate>> _middlewares = new List<Func<InvokeDelegate, InvokeDelegate>>();

        public IDictionary<string, object> Properties { get; }

        private ApplicationBuilder(ApplicationBuilder builder)
        {
            Properties = builder.Properties;
        }

        public ApplicationBuilder()
        {
            Properties = new Dictionary<string, object>();
        }

        public IApplicationBuilder New()
        {
            return new ApplicationBuilder(this);
        }

        public InvokeDelegate Build()
        {
            InvokeDelegate next = context => Task.Run(() => { });

            foreach (var current in _middlewares.Reverse())
            {
                next = current(next);
            }

            return next;
        }

        public virtual IApplicationBuilder Use(Func<InvokeDelegate, InvokeDelegate> middleware)
        {
            _middlewares.Add(middleware);
            return this;
        }

        private T GetProperty<T>(string key)
        {
            object value;
            return Properties.TryGetValue(key, out value) ? (T)value : default(T);
        }

        private void SetProperty<T>(string key, T value)
        {
            Properties[key] = value;
        }
    }
```

```csharp
public class Application
    {
        #region Singleton Implementation

        private static Application _application = null;
        private static readonly object SyncRoot = new Object();

        private Application()
        {
        }

        public static Application Current
        {
            get
            {
                if (_application == null)
                {
                    lock (SyncRoot)
                    {
                        if (_application == null)
                            _application = new Application();
                    }
                }
                return _application;
            }
        }

        #endregion Singleton Implementation

        public IApplicationBuilder appBuilder = new ApplicationBuilder.ApplicationBuilder();

        public InvokeDelegate app;

        public void Build()
        {
            app = appBuilder.Build();
        }

        public static TResult Invoke<TResult>(Expression<Func<object>> function, object instance) where TResult : class
        {
            InvokeContext context = new InvokeContext(function, instance, typeof(TResult));
            Application.Current.app.Invoke(context).Wait();

            if (context?.Result?.Value.GetType() != typeof(TResult))
            {
                throw new ArgumentException("Given type mismatch with result type");
            }
            return context.Result.Value as TResult;
        }

        public static Task<TResult> InvokeAsync<TResult>(Expression<Func<object>> function, object instance) where TResult : class
        {
            return Task.Run(() => Application.Invoke<TResult>(function, instance));
        }
    }
```

```csharp
public class CacheManager
    {
        private readonly InvokeDelegate _next;

        public CacheManager(InvokeDelegate next)
        {
            _next = next;
        }

        public async Task Invoke(InvokeContext context)
        {
            if (context == null)
            {
                throw new ArgumentNullException(nameof(context));
            }

            Console.WriteLine("Begin CacheManager.");

            await _next.Invoke(context);

            Console.WriteLine("End CacheManager.");
        }
    }
```

## Front-End implementations


In Javascript, the middleware pattern is extensively used by the "Express", "Connect" and "Koa" frameworks.
- Logging requests
- Authenticating/authorizing requests
- Parsing the body of requests
- End a request – response lifecycle
- Call the next middleware function in the stack.


```javascript

var Middleware = function() {};

Middleware.prototype.use = function(fn) {
  var self = this;

  this.go = (function(stack) {
    return function(next) {
      stack.call(self, function() {
        fn.call(self, next.bind(self));
      });
    }.bind(this);
  })(this.go);
};

Middleware.prototype.go = function(next) {
  next();
};
```


```javascript
var middleware = new Middleware();

middleware.use(function(next) {
  var self = this;
  setTimeout(function() {
    self.result1 = true;
    next();
  }, 10);
});

middleware.use(function(next) {
  var self = this;
  setTimeout(function() {
    self.result2 = true;
    next();
  }, 10);
});

var start = new Date();

middleware.go(function() {
  console.log(this.result1); // true
  console.log(this.result2); // true
  console.log(new Date() - start);
});



```
