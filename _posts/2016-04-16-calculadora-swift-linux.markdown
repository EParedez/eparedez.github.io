---
layout: post
title:  "Haciendo una calculadora con Swift en linux!"
date:   2016-04-16 00:50:40 -0500
categories: jekyll update
---
El tutorial que veremos en realidad es algo burdo y simple, sin embargo el objetivo es ver que como podemos resolver
los problemas que tengamos haciendo codigo swift en linux.
Vamos alla!.

Crearemos una clase llamada **Operacion.swift** con el siguiente codigo:<br />

{% highlight swift %}
public class Operacion{


 public init() {

 }

  public func sumar(a:Int, b:Int) -> Int {
    return a+b
  }

}

{% endhighlight %}

Posteriormente procedemos a crear otro archivo llamado, **Calculadora.swift**, de esta forma:

{% highlight swift %}
import operacion

var opera = Operacion()
var suma = opera.sumar(2,b:4);
print("La suma es: \(suma)");
{% endhighlight %}

Ahora necesitamos compilar, para ello es necesario hacer los siguientes pasos:
{% highlight bash %}
swiftc -emit-library operacion.swift -module-name operacion //
swiftc -emit-module -module-name operacion operacion.swift //
swiftc -I. -c Calculadora.swift //
swiftc -o Calculadora.exe Calculadora.o -L. -loperacion -lcurl -lswiftGlibc -lFoundation
LD_LIBRARY_PATH=.:$LD_LIBRARY_PATH ./Calculadora.exe
{% endhighlight %}

Pueden revisar el codigo fuente desde [aqui](https://www.google.com)
