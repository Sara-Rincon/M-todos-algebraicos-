12/09/24
# Métodos Algebraicos 
Se realizan para determinar el comportamiento del sistema en lazo cerrado y modificarlo
## Caracteristicas:
* Se pueden usar en el espacio de LaPlace, en terminos de "s" y en el espacio de las "z". Los métodos algebraicos no discriminan esto.
* Se parte del conocimiento del comportamiento de la planta -> Tanto su modelo, como el modelo en lazo cerrado.

imagen 

Existen dos tipos de métodos algebraicos: 
## Igualación de modelo: 
* G(z) lazo abierto, es conocida 
* G0(z) lazo cerrado, es lo que se desea

$$G_{0}(z)= \frac{C(z)G(z)}{1+C(z)G(z)} \to C(z)= \frac{G_{0}(z)}{G(z)(1-G_{0}(z))}  G_{0}(z)= \frac{C(z)G(z)}{1+C(z)G(z)}$$   

