---
layout: post
title:  "Haciendo una calculadora con Swift en linux!"
date:   2016-04-16 00:50:40 -0500
categories: jekyll update
---
El tutorial que veremos en realidad es algo burdo y simple, sin embargo el objetivo es ver que como podemos resolver
los problemas que tengamos haciendo codigo(en este caso operaciones simples como sumar, restar, etc) swift en linux.
Vamos alla!.

Crearemos una clase llamada **Operacion.swift** con el siguiente codigo:<br />

{% highlight swift %}
public class Operacion{


 public init() {

 }

 public func sumar(a:Int, b:Int) -> Int {
     return a+b
   }

   public func restar(a:Int, b:Int) -> Int {
     return a - b
   }

   public func dividir(a:Int, b:Int) -> Int {
     return a / b
   }

   public func multiplicar(a:Int, b:Int) -> Int {
     return a * b
   }

}

{% endhighlight %}

Posteriormente procedemos a crear otro archivo llamado, **Calculadora.swift**, de esta forma(esta archivo invocara al primero):

{% highlight swift %}
import operacion

var opera = Operacion()
var suma = opera.sumar(a: 2,b:4)
print("La suma es: \(suma)")
{% endhighlight %}

Procedemos a compilar el programa, para ello, tipeamos en la terminal:

{% highlight bash %}
swiftc Calculadora.swift
{% endhighlight bash %}

Nos dara como respuesta un bonito error:

{% highlight bash %}
Calculadora.swift:1:8: error: no such module 'operacion'
{% endhighlight bash %}

El compilador intenta llamar a nuestro archivo Operacion.swift como si fuera un modulo, bien; no nos complicamos,
y creamos el modulo:

{% highlight bash %}
swiftc -emit-library Operacion.swift -module-name operacion //crea la libreria
swiftc -emit-module -module-name operacion Operacion.swift  //permite que el modulo sea importable
{% endhighlight bash %}

Posteriormente procedemos a crear los ejecutables:

{% highlight bash %}
swiftc -I. -c Calculadora.swift //toma el directorio actual para compilar y buscar los modulos
swiftc -o Calculadora.exe Calculadora.o -L. -loperacion //crea el ejecutable
LD_LIBRARY_PATH=.:$LD_LIBRARY_PATH ./Calculadora.exe
{% endhighlight %}

Y obtenemos el siguiente resultado:
{% highlight bash %}
La suma es: 6
La resta es: -2
La division es: 0
La multiplicacion es: 8
{% endhighlight %}

Pueden revisar el codigo fuente desde [aqui](https://github.com/EParedez/calculadora-swift)

<div id="disqus_thread"></div>
<script>

/**
*  RECOMMENDED CONFIGURATION VARIABLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
*  LEARN WHY DEFINING THESE VARIABLES IS IMPORTANT: https://disqus.com/admin/universalcode/#configuration-variables*/
/*
var disqus_config = function () {
this.page.url = PAGE_URL;  // Replace PAGE_URL with your page's canonical URL variable
this.page.identifier = PAGE_IDENTIFIER; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
};
*/
(function() { // DON'T EDIT BELOW THIS LINE
var d = document, s = d.createElement('script');
s.src = '//eparedezgithubio.disqus.com/embed.js';
s.setAttribute('data-timestamp', +new Date());
(d.head || d.body).appendChild(s);
})();
</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
