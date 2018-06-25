---
layout: article
permalink:
name:
file_type:
title: AOP Framework without proxy pattern
description: >-
  AOP Framework without proxy pattern
tags:  
category:  
sort_order: 22
rating: 40
changefreq: monthly
priority: 0.5
published: true
create_date: 2017-11-23T00:00:00.000Z
modified_date: 2017-11-23T00:00:00.000Z
created_by: atilla
modified_by: atilla
comments: true
redirect_url:
---

# AOP Framework without proxy pattern

AOP addresses the problem of cross-cutting concerns, which would be any kind of code that is repeated in different methods.
separating of concerns prevents code repetitions.

People generally use proxy pattern (Dynamic Proxy generators) for Applying AOP in C#,
This example don't use dynamic proxy generators, it is simple because it uses only function definition.


[example code](https://github.com/atillatan/robo-aspect-framework)


# robo-aspect-framework

Attributes for AOP

```csharp
public class PersonService : BaseService, IPersonService
{
    [Cache]
    [Log]
    public virtual string Method1(int x)
    {
        return $"input is {x}";
    }
}
```

Invoking Methods:

```csharp

PersonService personService = new PersonService();

var result = personService.Invoke<string>(() => personService.Method1(3));

```



Invoker:


```csharp

public static class Invoker
{
    public static object Invoke(InvokeContext context)
    {
        if (context == null)
        {
            throw new ArgumentNullException(nameof(context));
        }

        Expression<Func<object>> _function = context.Request.Function;
        object _instance = context.Request.Instance;

        var timer = Stopwatch.StartNew();
        if (_instance == null) throw new Exception("Service is null!");
        var fbody = _function.Body as MethodCallExpression;
        if (fbody == null || fbody.Method == null) throw new Exception("Expression must be a method call.");
        string methodName = fbody.Method.Name;
        dynamic result = null;

        List<object> args = new List<object>();

        foreach (var argument in fbody.Arguments)
        {
            var constant = argument as ConstantExpression;
            if (constant != null)
            {
                args.Add(constant.Value);
            }
        }

        IEnumerable<Attribute> aspects = _instance.GetType().GetMethod(methodName).GetCustomAttributes(true);

        RunBeforeAspects(context, aspects);

        //if cache aspect or other aspects, returns response.
        if (context?.Result?.Value != null)
        {
            return context.Result.Value;
        }

        try
        {
            result = fbody.Method.Invoke(_instance, args.ToArray<object>());
            Type t = context.Result.ResultType;
            context.Result.Value = result;
        }
        catch (Exception e)
        {
            throw e;
        }
        finally
        {
            timer.Stop();
            Console.WriteLine($"{methodName}() method invoked in :{Convert.ToDouble(timer.ElapsedMilliseconds)}ms ");
        }

        RunAfterAspects(context, aspects);

        return result;
    }

    private static void RunBeforeAspects(InvokeContext context, IEnumerable<Attribute> aspects)
    {
        foreach (var aspect in aspects)
        {
            if (aspect.GetType().GetTypeInfo().BaseType == typeof(AspectBase))
            {
                ((IAspect)aspect).OnBefore(context);
            }
        }
    }

    private static void RunAfterAspects(InvokeContext context, IEnumerable<Attribute> aspects)
    {
        foreach (var aspect in aspects)
        {
            if (aspect.GetType().GetTypeInfo().BaseType == typeof(AspectBase))
            {
                ((IAspect)aspect).OnAfter(context);
            }
        }
    }
}
```
