
+++
title = "Qué es más peligroso, la corriente o el voltaje?"
description = "Un vistazo a las principales características y diferencias entre ellos"
author = "Miguel Freytes"
date = 2021-02-21
tags = ["voltaje","corriente", "resistencia"]
categories = ["general"]
[[images]]
  src = "img/2021/02/current-or-voltage.jpg"
  alt = "Líneas de Transmisión"
  stretch = "stretchH"
+++
<p style="text-align: justify;">Alguna vez has recibido una descarga manipulando un electrodoméstico? Si la respuesta es afirmativa te sentirás identificado con el tema que hablaremos hoy, y si nunca te ha ocurrido sigue leyendo y sabrás como evitarlas en un futuro. 

La energía eléctrica es parte fundamental de nuestras vidas, la podemos ver en todas partes y sin ella no viviríamos en la sociedad moderna que hoy tenemos, sin embargo así como es uno de los ejes de la sociedad actual, tambien existe mucho desconocimiento acerca de la misma y a lo largo de este post se estarán aclarando algunos conceptos básicos y algunas medidas de seguridad que se deben tener en cuenta.

Uno de los mitos más extendidos actualmente, es el hecho de que el alto voltaje es el causante de la mayoría de los accidentes eléctricos, y aunque en parte es cierto, se debe tener en cuenta que hay más factores involucrados y en ocasiones puede ser igual de letal el flujo de corriente de miles de voltios que un flujo de corriente causado por unos pocos voltios.  

Según la ley de Ohm, el voltaje es igual a la resistencia multiplicada por la corriente:

<div>$$V=I \cdot R$$</div>

La resistencia es la oposición que presentan los materiales al flujo de corriente, un buen conductor como lo puede ser el cobre o el oro presenta una resistencia baja, mientras que un material aislante como la madera o la goma presentan una resistencia alta. 

En cuanto a nuestro cuerpo, la resistencia de la piel seca es de alrededor de unos 4000 Ohms, esto quiere decir que para un voltaje bajo como lo puede ser una bateria AA (1.5 V), la corriente que fluye a través de nuestro cuerpo es bastante pequeña (aproximadamente 0.3 mA), sin embargo cuando las tensiones comienzan a ser más altas, los riesgos de lesión se incrementan.

A continuación se muestra una tabla de los efectos de la corriente para sus diferentes valores:


</p>

<table border="1">
	<tr style="background-color: #5B99FF;"><th>Corriente</th><th>Reacción</th></tr>
	<tr><th>1 mA</th><th>Nivel de Percepción. Solo un ligero cosquilleo</th></tr>
	<tr><th>5 mA</th><th>Se siente un ligero shock, no doloroso pero molesto. El individuo promedio puede liberarse del circuito. SIn embargo fuertes reacciones involuntarias en este rango pueden causar heridas</th></tr>
	<tr><th>6 - 25 mA</th><th>(Mujeres) Shock Doloroso, pérdida de control muscular</th></tr>
	<tr><th>9 - 30 mA</th><th>(Hombres) Este es el valor límite en que puede liberarse del circuito por sí mismo</th></tr>
	<tr><th>50 - 150 mA</th><th>Dolor extremo, paro respiratorio, contracciones musculares severas. La persona no puede liberarse</th></tr>
	<tr><th>1000 - 4300 mA</th><th>Fibrilación Ventricular. Cesa el bombeo rítmico del corazón. Ocurren daños al sistema nervioso y contracción muscular involuntaria. Muerte muy probable</th></tr>
	<tr><th>10000 mA</th><th>Paro Cardíaco, quemaduras severas y probable muerte.</th></tr>
</table>

<p style="text-align: justify;"> Aplicando la ley de Ohm para los valores de la tabla y tomando en cuenta la resistencia de la piel, es posible observar que para el caso de 30 mA son necesarios 120V, el cual es el valor de tensión doméstica más común en latino américa, cabe destacar que estos valores son obtenidos cuando son tocados ambos bornes de una fuente de tensión sin nada más conectado, pero qué ocurriría si hay otro elemento de por medio? Como una lampara o un electrodoméstico? 

Bueno la respuesta a esa duda se encuentra en la asociación de resistencias, todo equipo o electrodoméstico puede ser representado como una resistencia de mayor o menor valor. Tomemos el ejemplo de una lámpara de 12 V y 8 amperios, como podemos observar la corriente que fluye a través de la lampara es mucho mayor a la necesaria para causar algún daño, la clave está en que toda esa corriente no fluye a través del cuerpo humano, veamos el por qué.

Si se aplica la ley de Ohm para la lámpara de 12 V tenemos:

<div>$$R = \frac V I = \frac {12}{8} = 1.5 \Omega$$<div>

Se puede observar que la resistencia de la lámpara es bastante pequeña con respecto al valor de la resistencia de la piel humana, si la lámpara es conectada a la bateria en un extremo y en el otro extremo nos encontramos nosotros, el circuito que formaríamos es el siguiente:

</p>


![Lampara en serie con manos](/img/2021/02/current-series.png)

<p style="text-align: justify;">
En este caso la resistencia de la lampara se suma a la de nuestro cuerpo, siendo la resistencia total igual a 4001.5 Ohms de tal forma que por ley de ohm la corriente en el circuito va a ser menos de 3 mA, la lampara no se encenderá y la corriente será inofensiva para nosotros.

Otra situación posible es la siguiente:
</p>

![Lampara en paralelo con manos](/img/2021/02/current-parallel.png)

<p>
Cuando dos resistencias se encuentran en paralelo, el voltaje en cada una de ellas es el mismo, por lo tanto es posible aplicar la ley de ohm independientemente, de tal forma que para la lámpara, la corriente resultante van a ser los 8 amperios requeridos y la misma se va a encender, sin embargo la resistencia de nuestro cuerpo sigue siendo de un gran valor, y la corriente a través de él seguirá sin superar los 3 mA.
</p>

<script type="text/javascript"
    src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>

<script type="text/x-mathjax-config">
MathJax.Hub.Config({
  tex2jax: {
    inlineMath: [['$','$'], ['\\(','\\)']],
    displayMath: [['$$','$$'], ['\[','\]']],
    processEscapes: true,
    processEnvironments: true,
    skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
    TeX: { equationNumbers: { autoNumber: "AMS" },
         extensions: ["AMSmath.js", "AMSsymbols.js"] }
  }
});
</script>

<script type="text/x-mathjax-config">
  MathJax.Hub.Queue(function() {
    // Fix <code> tags after MathJax finishes running. This is a
    // hack to overcome a shortcoming of Markdown. Discussion at
    // https://github.com/mojombo/jekyll/issues/199
    var all = MathJax.Hub.getAllJax(), i;
    for(i = 0; i < all.length; i += 1) {
        all[i].SourceElement().parentNode.className += ' has-jax';
    }
});
</script>


