12/09/24
# Introducción a los Métodos Algebraicos 
Los métodos algebraicos en control digital son técnicas que permiten analizar y diseñar sistemas de control que operan en tiempo discreto, es decir, en terminos de "z". A través de herramientas como la transformada Z y el uso de ecuaciones de diferencia, estos métodos transforman la dinámica de los sistemas continuos en un entorno discreto. Al hacerlo, facilitan el estudio de la estabilidad, respuestas en frecuencia y el diseño de controladores como los PID, que son esenciales en la implementación de controladores modernos.

# Métodos Algebraicos 
>  🔑 Definición: Se realizan para determinar el comportamiento del sistema en lazo cerrado y modificarlo
## Características:
* Se pueden usar en el espacio de LaPlace, en términos de "s" y en el espacio de las "z". Los métodos algebraicos no discriminan esto.
* Se parte del conocimiento del comportamiento de la planta -> Tanto su modelo, como el modelo en lazo cerrado.
* Se modela completamente la función de transferencia. 

Existen dos tipos de métodos algebraicos: 
## 1. Igualación de modelo: 
* G(z) lazo abierto, es conocida 
* G0(z) lazo cerrado, es lo que se desea

$$G_{0}(z)= \frac{C(z)G(z)}{1+C(z)G(z)} \to C(z)= \frac{G_{0}(z)}{G(z)(1-G_{0}(z))}$$   

# 💡Ejemplo 1
Se tiene la siguiente planta:

$$G(z)= \frac{0.01(z+1)}{z^{3}-2.01z+1}$$ 

DATOS:
* zita = 0.6
* Tp = 0.5
* $$0.5=\frac{\pi}{Wn(\sqrt{1-(0.6)^{2}})} \to 7.85 rad/s$$
* K= 1
* T = 0.1 segundos

  $$G_{0}(s)= \frac{61.62}{s^{2}+9.42s+61.62}$$
  
  $$G_{0}(z)= \frac{61.62}{(\frac{z-1}{0.1})^{2}+9.42(\frac{z-1}{0.1})+61.62}$$
  
  $$G_{0}(z)= \frac{0.009z+0.008}{z^{3}-1.801z+0.818}$$
  
El controlador quedaría:

$$C(z)= \frac{\frac{0.009z+0.008}{z^{3}-1.801z+0.818}}{\frac{0.01(z+1)}{z^{3}-2.01z+1}(1-\frac{0.009z+0.008}{z^{3}-1.801z+0.818})}$$

Lo que da como resultado:

$$C(z)= \frac{0.934z^{3}-1.004z^{2}-0.822z+0.973}{z^{3}-0.81z^{2}-z+0.81}$$

## 2. Igualación de coeficientes: 
> 🔑 ¿Que se hace?: Se analizan los coeficientes del polinomio característico.

Características adicionales:
* Se conocen la ubicación de los polos que se desea, así que se busca la representación del polinomio característico.
* Se puede obtener el C(z) Controlador que asegura el comportamiento deseado.
* Se hace una igualación coeficiente a coeficiente. 

# 💡Ejemplo 2
Si se tiene G(z) de la siguiente manera: 

$$G(z)= \frac{0.0043}{z^{2}-1.819z+0.8187}$$

Ahora bien, si se desea tener un controlador para ubicar los nuevos polos de la siguiente manera: 

$$p_{1}=0.91+0.23j; p_{2}=0.91-0.23j$$

Entonces el polinomio característico, es decir, el que se desea en lazo cerrado es: 

$$(z-0.91+0.23j)(z-0.91-0.23j)= {\color{Red} z^{2}-1.82z+0.881}$$

Si en lazo cerrado $$G_{0}(z)= \frac{KG(z)}{1+KG(z)}$$, entonces se hacen los siguientes cálculos: 

$$G_{0}(z)= \frac{K(\frac{0.0043}{z^{2}-1.819z+0.8187})}{1+K(\frac{0.0043}{z^{2}-1.819z+0.8187})}$$

$$G_{0}(z)=\frac{K(0.0043)}{z^{2}-1.819z+0.8187+K(0.0043)}$$

* Al igualar los coeficientes se puede observar que el término que acompaña a las z a ambos lados del igual, son diferentes, por lo tanto no se puede realizar con acción proporcional.Entonces...

## Funciones causales(Propias) 
### Características
* El controlador tiene que ser de un orden menor que el orden de la planta.
* Debe ser BIPROPIO.
* Se le debe agregar un polo y un zero.
* Este concepto no se aplica para funciones de primer orden.

$$G(z)=\frac{N(z)}{D(z)}; C(z)=\frac{B(z)}{A(z)}; G_{0}(z)=\frac{N_{0}(z)}{D_{0}(z)}$$

Si $$ G_{0}(z)=\frac{C(z)G(z)}{1+C(z)G(z)}\Rightarrow \frac{B(z)N(z)}{{\color{Orchid} A(z)D(z)}+{\color{Green} B(z)}N(z)}$$

* Donde A(z) y D(z) son los valores causantes de que se suba un orden. Y B(z) y A(z) son las variables a solucionar para hallar el controlador.

# 💡Ejemplo 3
Siguiendo el ejemplo 1 y teniendo un controlador que no es bipropio, sucede:

  $$C(z)=\frac{B_{0}}{A_{0}+A_{1}z}$$
  
  Ahora el sistema tendrá 3 polos, por lo que: $$(z-0.91+0.23j)(z-0.91-0.23j)(z-0.91)= {\color{Red} z^{3}-2.73z^{2}+2.537z-0.8017}$$
  
  En lazo cerrado: $$G_{0}(s)=\frac{0.0043B_{0}}{A_{1}z^{3}+z^{2}(A_{0}-1.819A_{1})+(0.8187A_{1}-1.819A_{0})z+0.8187A_{0}+0.0043B_{0}}$$
  
  * Resolviendo la igualdad entre ambos polinomios característicos, se obtiene que NO se satisfacen todas las ecuaciones.
  * Se analiza qué Número de incógnitas debe ser igual a numero de ecuaciones.

# 💡Ejemplo 4
Siguiendo el ejemplo 2 y teniendo un controlador bipropio, sucede: 
  $$C(z)=\frac{B_{0}+B_{1}z}{A_{0}+A_{1}z}$$
  Ahora el sistema seguirá teniendo 3 polos, por lo que: $$(z-0.91+0.23j)(z-0.91-0.23j)(z-0.91)= {\color{Red} z^{3}-2.73z^{2}+2.537z-0.8017}$$
  En lazo cerrado: $$G_{0}(s)=\frac{0.0043(B_{0}+B_{1}z)}{A_{1}z^{3}+z^{2}(A_{0}-1.819A_{1})+(0.8187A_{1}-1.819A_{0}+0.0043B_{1})z+0.8187A_{0}+0.0043B_{0}}$$
* Resolviendo la igualdad entre ambos polinomios característicos, se obtiene que A_{0}= -0.911; A_{1}= 1; B_{0}= -12.99 y B_{1}= 14.23
* Los coeficientes obtenidos satisfacen lo requerido para obtener el controlador, por ende, el controlador resulta siendo:
    $$C(z)=\frac{-12.99+14.23z}{-0.911+z}$$

# Ecuaciones Diofánticas
* Dado que lo que interesa es el polinomio característico y B(z) y A(z) son las variables a solucionar, entonces se generaliza y simplifica todo con una ecuación diofántica, en donde, D_{0} serán los puntos de la dinámica del sistema (Denominador) deseados.
* Se realiza de la siguiente manera:

![Figura de prueba](Ecuaciones_Diofanticas.png)

Figura 1. Ecuaciones Diofánticas y su uso.

# 💡Ejemplo 5
Se tiene $$G(z)=\frac{0.005+0.005z}{z^{2}-2z+1}; C(z)=\frac{B_{0}+B_{1}z}{A_{0}+A_{1}z}$$
Entonces en lazo cerrado sería: $$G_{0}(s)=\frac{(0.005+0.005z)(B_{0}+B_{1}z)}{(A_{0}+A_{1}z)(z^{2}-2z+1)+(B_{0}+B_{1}z)(0.005+0.005z)}$$

$$D_{0} = A_{1}z^{3}+(A_{0}-2A_{1}+0.005B_{1})z^{2}+(A_{1}-2A_{0}+0.005B_{1}+0.005B_{0})z+A_{0}+0.005B_{0}$$
Y el polinomio deseado es $$(z+0.2)^3$$ por ende la ecuación diofántica quedaría:

![Figura de prueba](ejercicio_ED_1.png)

Figura 2. Ejercicio Ecuaciones diafónticas.

Los resultados obtenidos dan el siguiente controlador:

 $$C(z)=\frac{345.6z-172.8}{z+0.872}$$

 # 📚 Ejercicios 
1. Se tiene la siguiente planta:
   
   $$G(s)=\frac{1}{(s+1)(s+3)} \to \frac{1}{s^2+4s+3}$$

   Los datos deseados que se quieren obtener en lazo cerrado son:
   * Error de estado estacionario = 0
   * Mp < 10%
   * Ts = 1 segundo
   * T = 0.2 segundos

   $$\zeta = \sqrt{\frac{ln^{2}(0.1)}{\pi^{2}+ln^{2}(0.1)}}\to 0.59$$

   $$1=\frac{4}{(0.59)Wn}\to Wn= 6.77$$

   Como el error de estado estacionario debe ser 0, la ganancia proporcional resulta siendo infinito, asi que se supone un valor elevado (10000= para poder realizar el procedimiento de hallar el controlador.

   $$G_{0}(s)=\frac{458300}{s^{2}+7.98s+45.83}$$

   $$G_{0}(z)=\frac{458300}{(\frac{z-1}{0.2})^{2}+7.98(\frac{z-1}{0.2})+45.83}$$

   $$G_{0}(z)=\frac{458300}{25z^{2}-10.1z+30.93}$$

   De forma canonica se tiene:

   $$G_{0}(z)=\frac{18332}{z^{2}-0.40z+1.23}$$

   Y ahora se discretiza G(s) para obtener G(z)

   $$G(z)=\frac{1}{\frac{z^{2}-2z+1}{0.04}+4(\frac{z-1}{0.2})+3}$$

   $$G(z)=\frac{1}{25z^{2}-30z+8} \to \frac{0.04}{z^{2}-1.2z+0.32}$$


   El controlador sería:

   $$C(z)=\frac{\frac{18332}{z^{2}-0.40z+1.23}}{\frac{0.04}{z^{2}-1.2z+0.32}(1-\frac{18332}{z^{2}-0.40z+1.23})}$$

2. Se tiene la siguiente planta:
   $$G(z)= \frac{1}{z^{2}-z+3}$$

   Se desea un controlador con la siguiente función:
   $$C(z)= \frac{B_{0}+B_{1}z}{A_{0}+A_{1}z}$$

   Con la siguiente ubicación de polos deseados en:
   $$P1 = -3; P2=-0.5; P3= 0.2$$

   El polinomio deseado sería:
   $$(z+3)(z+0.5)(z-0.2)= z^{2}+3.5z+1.5(z-0.2) = z^{3}+3.5z^{2}+1.5z-0.2z^{2}-0.7z-0.3 = z^{3}+3.3z^{2}+0.8z-0.3$$
   
   $$G_{0}(z)= \frac{\frac{B_{0}+B_{1}z}{A_{0}+A_{1}z}(\frac{1}{z^{2}-z+3})}{1+(\frac{1}{z^{2}-z+3})(\frac{B_{0}+B_{1}z}{A_{0}+A_{1}z})}$$
   
   $$G_{0}(z)= \frac{1(B_{0}+B_{1}z)}{(A_{0}+A_{1}z)(z^{2}-z+3)+B_{0}+B_{1}z}$$

   $$G_{0}(z)= \frac{1(B_{0}+B_{1}z)}{A_{1}z^{3}+z^{2}(A_{0}-A_{1})+(3A_{1}-A_{0}+B_{1})z+3A_{0}+B_{0}}$$
   
   Al igualar se tiene:
   $$z^{3}+3.3z^{2}+0.8z-0.3 = A_{1}z^{3}+z^{2}(A_{0}-A_{1})+(3A_{1}-A_{0}+B_{1})z+3A_{0}+B_{0}$$

   $$A_{1} = 1$$
   
   $$A_{0}-A_{1}= 3.3$$
   
   $$0.8 = 3A_{1}-A_{0}+B_{1}$$
   
   $$-0.3 = 3A_{0}+B_{0}$$

   Con las cuatro ecuaciones y las cuatro incógnitos se procede a analizar por sustitución y se obtiene que:
   
   $$A_{0}= 4.3; A_{1}= 1; B_{0}= -13.2; B_{1}= 2.1$$

   Entonces el controlador por método de igualación de coeficientes quedaría:

   $$C(z)= \frac{2.1z-13.2}{z+4.3}$$
   
# Conclusiones 
Al aplicar estos métodos, es posible garantizar la estabilidad y eficiencia de los sistemas, adaptándolas a ciertas restricciones/ limitaciones del entorno digital. Y no solo eso, los métodos algebraicos permiten modelar  cualquier sistema en lazo cerrado; Sin embargo, hay que siempre tener en cuenta que aunque matemáticamente den los cálculos, en el ámbito del control a veces es casi imposible implementarlos, por lo que hay que tener cuidado. Además, proporcionan una base sólida para el desarrollo de controladores precisos en aplicaciones industriales, de automatización y mecatrónica, contribuyendo al avance tecnológico en múltiples sectores.
