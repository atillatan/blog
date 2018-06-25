---
layout: article
permalink: null
name: null
file_type: null
title: Factory Pattern with Javascript
description: Factory Pattern with Javascript
tags: javascript
category: null
sort_order: 74
rating: 100
changefreq: monthly
priority: 0.5
published: true
create_date: 2017-11-13 00:00:00 +0000
modified_date: 2017-11-13
created_by: atilla
modified_by: atilla
comments: true
redirect_url: null
---

# Factory Pattern with Javascript


```JavaScript
function Sword(desc){
  this.weaponType = "Sword";
  this.metal = desc.metal || "Steel";
  this.style = desc.style || "Longsword";
  this.hasMagic = desc.hasMagic || false;
}

function Bow(desc){
  this.weaponType = "Bow";
  this.metal = desc.metal || "Wood";
  this.style = desc.style || "Longbow";
  this.hasMagic = desc.hasMagic || false;
}

function WeaponFactory () {};
WeaponFactory.prototype.makeWeapon = function(desc){
  var weaponClass = null;

  if(desc.weaponType === "Sword"){
    weaponClass = Sword;
  } else if (desc.weaponType === "Bow"){
    weaponClass = Bow;
  } else {
    return false;
  }

  return new weaponClass(desc);
}

var myWeaponFactory = new WeaponFactory();

var bladeFist = myWeaponFactory.makeWeapon({
  weaponType: "Sword",
  metal: "Dark Iron",
  style: "Scythe",
  hasMagic: true
});

document.write(bladeFist.weaponType + " of type " + bladeFist.style + " crafted from " + bladeFist.metal );

```
