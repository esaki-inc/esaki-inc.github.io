+++
title="Generador de Señales con Microcontrolador Pic"
date= 2021-02-24
author = "Miguel Freytes"
tags = ["generador","microcontrolador", "pic"]
categories = ["microcontroladores"]
[[images]]
  src = "img/2021/02/wave-generator.jpg"
  alt = "Generador de Ondas con pic"
  stretch = "stretchH"
+++

<p style="text-align: justify-all;">
Los generadores de señales son unos dispositivos muy útiles en caso de que queramos observar el comportamiento de un circuito para diferentes señales de entrada, en este post se explicará como hacer uno con algunas características básicas pero puede ser tomado como base para un proyecto aun más complejo.

En este post hablaremos un poco de programación en C y Python, si no estás muy familiarizado con estos lenguajes no te preocupes, ya que explicaremos cada línea paso por paso, sin embargo es importante que tengas noción de las estructuras básicas de programación.

Lista de Materiales:

</p>

<ul>
	<li>Microcontrolador PIC 16f84A</li>
	<li>9 Resistencias de 20kΩ</li>
	<li>8 Resistencias de 10kΩ</li>
	<li>Pulsador</li>
	<li>Fuente de Alimentación</li>
</ul>

<p style="text-align: justify-all;">
Para este ejemplo estaremos usando el microcontrolador PIC 16f84A, pero es posible utilizar cualquier otro microcontrolador siempre y cuando tenga 2 puertos, y uno de ellos sea de 8 bits.

El funcionamiento del generador de señales que estaremos armando se basa en el principio del convertidor Digital - Analógico (ADC), mediante el codigo que cargaremos al microcontrolador tendremos una salida digital de 8 bits variante en el tiempo y a través del uso del ADC generaremos la señal deseada.

Si no estás muy familiarizado con el funcionamiento del convertidor ADC te recomendamos que visites nuestro post referente a los ADC <a href="#">aquí</a>.

A continuación se muestra el codigo que estaremos empleando, es importante destacar que estamos utilizando el compilador <strong>PIC C Compiler</strong> por lo que puede tener ciertas diferencias con el tuyo en específico, sin embargo las funciones en todos los compiladores son muy similares.

</p>

<pre class="r"><code>
// Directivas de Preprocesado
#include < 16f84A.h >
#include < math.h >
#fuses XT, NOWDT, NOPROTECT

// Definiendo la Velocidad del Reloj 4MHz
#use delay (clock = 4000000)
// Definiendo el puerto predeterminado al puerto B
#use standard_io(b)

// Inicialización de variables
int i = 0;
int j = 0x00;
int sel = 0;
int seno[52] = {128, 143, 159, 174, 188, 201, 213, 224, 234, 242, 248, 252, 254, 255, 253,
250, 245, 238, 229, 219, 207, 195, 181, 166, 151, 135, 120, 104, 89, 74, 60, 48, 36, 26,
17, 10, 5, 2, 0, 1, 3, 7, 13, 21, 31, 42, 54, 67, 81, 96, 112, 127};

void main(){
   // Definiendo Función de los pines de los puertos
   // "0" para usar los puertos como salida
   // "1" para usarlos como entradas

   set_tris_b(0x00);
   set_tris_a(0b00011111);

   // Inicializando los pines del puerto B a 0
   output_b(0);

   while(TRUE){
      // Leemos el pin 0 del puerto A, si el botón está presionado incrementa en 1 la variable de selección
      if(input(PIN_A0)){
         sel++;
         // Debemos ponerle cierto delay para que evite detectar pulsaciones repetidas
         delay_ms(100);

         // En caso de que el selector llegue a la 3era señal y se vuelva a presionar se reinicia
         if(sel>=3){
            sel = 0;
         }
      }

      // Si el selector se encuentra en 0 la salida es la onda cuadrada
      if(sel == 0){
         if(i==255){
            i=0;
         }else{
            if(i<128){
               output_b(0xff);
               i++;
            }
            else{
               output_b(0x00);
               i++;
            }
         }
      }

      // Si el selector se encuentra en 1 la salida es la señal diente de sierra
      if(sel == 1){
         if(j==0xff){
            j = 0x00;
            output_b(j);
         }else{
            j++;
            output_b(j);
         }
      }


      // Si el selector se encuentra en 2 la salida es la señal senoidal
      if(sel == 2){
         if(i==52){
            i = 0;
            
         }else{
            
            output_b(seno[i]);
            
            i++;
         }
      }

   }
}


</code></pre>

<p style="text-align: justify-all;">
El funcionamiento del codigo es bastante sencillo, simplemente iniciamos un ciclo que estará activo todo el tiempo y que se encargará de verificar la señal que tenemos seleccionada y generarla. Basicamente al momento de presionar el pulsador, cambiará la variable de selección y dependiendo del valor de esa variable, la señal de salida será una u otra.

<strong>Onda Cuadrada</strong>

Para el caso de la onda cuadrada, tendremos un contador que irá desde 0 a 255, y se estará incrementando cada pulso de reloj, para esta forma de onda se requiere que la mitad del ciclo de trabajo tenga tensión y la otra mitad no la tenga, por lo tanto cuando el contador alcanza la mitad del valor máximo varía a su segundo estado, si el contador alcanza el limite máximo se reinicia, volviendo a comenzar de nuevo.

<strong>Onda Diente de Sierra</strong>

La señal diente de sierra tiene una forma particular, la cual va incrementando su valor progresivamente hasta llegar a su máximo donde se reinicia, por lo tanto solo fue necesario el uso de un contador que al llegar a 256 volviera a comenzar, dando como resultado la forma de onda deseada.

<strong>Onda Senoidal</strong>

Para la onda senoidal el proceso es algo más complejo, debido a que el dispositivo no dispone de mucha memoria RAM, no es posible calcular los valores de la señal senoidal en tiempo real, por lo tanto es necesario precargar en la memoria del dispositivo los valores a ejecutar. Para ello se empleo un array de enteros con los valores precalculados y posteriormente se iba leyendo dicho array con el contador usado en la onda cuadrada.

Si deseas obtener los valores para la señal senoidal puedes emplear varios métodos, a continuación se muestra un código básico de python que genera un número determinado de valores de la función seno:

</p>

<pre>
<code>
import math

// Creación del array para los valores
numeros = []

// Ciclo con 255 valores que avanza en pasos de 5
// Si posees un microcontrolador de mayor capacidad puedes emplear más valores
// y tendrá una forma más fiel a la función seno

for i in range(0,256,5):

   // Regla de 3 para convertir el valor de i en un angulo no mayor a 360°
   angle = (i*360.0)/255.0;

   // Convirtiendo el angulo obtenido a radianes
   radian = angle*math.pi/180.0;

   // Determinando el seno del angulo y sumando 1 para evitar valores negativos
   angleSin = math.sin(radian)+1.0;

   // Aplicando una regla de 3 nuevamente para tener valores entre 0 y 255
   digital = round(angleSin*255.0/2.0);

   // Anexando los valores al array
   numeros.append(digital)

print(numeros)
</code>
</pre>

<p style="text-align: justify-all;">
Ejecutando el codigo anterior puedes obtener una serie de valores de la onda seno que van entre 0 y 255 para ser enviados al puerto B directamente.

Luego de haber compilado y cargado el programa en el microcontrolador, procedemos a realizar el montaje del circuito del esquema.

</p>

{{% figure src="/img/2021/02/wave-generator-diagram.jpg" alt="Diagrama generador de señales con PIC"%}}

<p style="text-align: justify-all;">
La simulación anterior muestra un osciloscopio conectado a la salida del convertidor ADC, dando como resultado las siguientes salidas:
</p>

{{% figure src="/img/2021/02/wave-generator-output.jpg" alt="Salida del Generador de Señales con PIC"%}}

<p style="text-align: justify-all;">
Gracias por leer! Śiguenos y no te pierdas los demás proyectos que publicamos.
</p>