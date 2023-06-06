# LAB6: Manejo de interrupciones

*El siguiente repositorio contiene la documentación correspondiente a la actividad LAB6: Manejo de interrupciones.*

---

## El código utilizado consta de las siguientes funciones:
1) main
2) Delay
3) Default_Handler
4) EXIT15_11_Handler
5) Output.s
6) SysTick_Handler
7) Config_Reset_Handler
8) Reset_Handler
9) Speed


# Funcionamiento del código

## main
#### Códificación:
![image](https://github.com/DamianPerezB/Lab6/assets/89427173/68678753-d5c8-4664-8da1-cc6d539840ed)
![image](https://github.com/DamianPerezB/Lab6/assets/89427173/4e448a7d-a26e-47e4-8c3b-15e272b79804)
![image](https://github.com/DamianPerezB/Lab6/assets/89427173/ee76a7f6-6919-4ec4-8004-059ccf094bf7)

#### Descripción detallada:
Habilita el reloj del puerto A, define los pines PA0 a PA9 como salidas y PA10 junto con PA11 como entradas.  
Además configura a PA10 y PA11 como entradas para generar las interrupciones EXTI10 y EXTI11 y llama a la función config para inicializar los registros globales.  
A continuación se realiza la configuración para que NVIC sea el encargado de atender las interrupciones de la función EXTI, esto se consigue cargando el bit definido para la interrupción y enmascarandolo con NVIC_ISER1_OFFSET.  
Seguido de esto, deshabilitamos Systick IRQ y Systick timer, para así establecer a SysTick_CRL. Por consiguiente se limpia el valor de SysTick y se establece la prioridad en la que se atenderán las interrupciones, para así configurar a SysTick CRL para habulitar el temporizador de las interrupciones.
Finalmente se verifica la dirección en que debe avanzar la cuenta con el registro global r10, donde aumentará o disminuirá dependiendo su valor almacenado, se mostrará el retraso y terminará verificando la velocidad en la que se encuentra la cuenta y generando un pequeño retraso.

## Delay
#### Códificación:
![image](https://github.com/DamianPerezB/Lab6/assets/89427173/87c97e74-371c-4038-932b-f7f6ade1975a)
#### Descripción detallada:
Función encargada de generar un retraso. Cargará el valor de la velocidad en un registro temporal para compararlo con 0. En caso de que este no sea el mismo, Systick_Handler generará un retraso al decrementar 1 al registro global y volver a hacer la comparación hasta que el mismo sea igual a 0.

## Default_Handler
#### Códificación:
![image](https://github.com/DamianPerezB/Lab6/assets/89427173/f6ac55a6-0ae9-45d5-a809-941aefbd8709)
#### Descripción detallada:
Es una subrutina no implementada en ISR, es decir, será ejecutada cada vez que la interrupción apropiada no sea definida.

## EXIT15_11_Handler
#### Códificación:
![image](https://github.com/DamianPerezB/Lab6/assets/89427173/85747e0f-0839-43bb-a50d-b75146de189d)
![image](https://github.com/DamianPerezB/Lab6/assets/89427173/fd93f58a-c647-4f5c-82e5-4ca2ec9e134a)
#### Descripción detallada:
En la primer parte (EXTI15_10) Se define que interrupción se va a ejecutar. Para este caso se seleccionó 10 y 11. La comparación se utiliza para ver el número (x400 para la posición 10 y x800 para la posición 11). Dependiendo de que botón esté presionado, saltará a EXTI10 o EXTI11.  
EXTI10: Encargada de cambiar la direeción de la cuenta con el registro global r8, aumenta de uno en uno y limpia el PR para que se encuentre listo en la siguiente interrupción.
EXTI11: Encargada de aumentar la velocidad con el registro global r10, aumenta de uno en uno y limpia el PR para que se encuentre listo en la siguiente interrupción.

## Output
#### Códificación:
![image](https://github.com/DamianPerezB/Lab6/assets/89427173/d364ba08-b2fb-4e92-89ad-e61f4d9c733b)
#### Descripción detallada:
Encargado de mostrar el valor en el puerto digital, incialmente carga 1023 (que en bits nos retorna 10 veces uno) y compara con la cuenta actual del registro global r11. Esto nos permite mostrarlo como salida al cargar el valor en la base GPIOA

## SysTick_Handler
#### Códificación:
![image](https://github.com/DamianPerezB/Lab6/assets/89427173/ebf03a20-24ca-42d2-94fc-60a09b8ddaa4)
#### Descripción detallada:
Es una excepción que se dispara cada vez que el reloj llega a 0. Se invoca de forma automática por el hardware del procesador cuando ocurre una interrupción del temporizador

## Config_Reset_Handler
#### Códificación:
![image](https://github.com/DamianPerezB/Lab6/assets/89427173/b2115312-af44-4624-a3b7-6972703aa176)
#### Descripción detallada:
Simula reservar 4 registros para hacerlos "globales"  
r8: velocidad inicial  
r9: modificador de velocidad  
r10: dirección de la cuenta  
r11: cuenta o contador  

## Reset_Handler
#### Códificación:
![image](https://github.com/DamianPerezB/Lab6/assets/89427173/cd80151c-074b-48dd-b538-b42778aa8739)
#### Descripción detallada:
Es el punto de partida del programa y se ejecuta antes de cualquier otra rutina o función en el sistema.  
Inicia haciendo un llamado a la función main y a esta le suma 1 para indicar que es una función thumb; en caso de que retorne a la misma, hará un loop infinito

## Speed
#### Códificación:
![image](https://github.com/DamianPerezB/Lab6/assets/89427173/f0150115-accc-485b-bd4d-b61381e189bf)
#### Descripción detallada:
Es un conjunto de if´s en los cuales se busca ver el número de pulsaciones en el botón para identificar a que velocidad irá aumentando o disminuyendo la cuenta.  
La velocidad inicial es de 1000 ms, pero esta irá disminuyendo por la mitad hasta llegar a 125 (velocidad x8) donde, en caso de verse oprimido nuevamente el botón, la misma pasará de nuevo a su estado inicial (1000 ms).


## Diagrama del circuito:
![image](https://github.com/DamianPerezB/Lab6/assets/89427173/43475c5b-b9c1-42e5-bae7-dca48eeb227a)

# Descricpión de su funcionamiento:
El microcontrolador en su estado inicial, mantiene una cuenta ascendente en numeración binaria, la cual es representada de forma visual con ayuda de 10 leds.
Además consta de dos botones, cuyo funcionamiento es el siguiente.  
Botón 1: Al ser presionado, la cuenta cambia de ascendente a descendente.  
Botón 2: Al ser presionado, la velocidad con la que fluye la cuenta se modifica a x2, x4, x8 y volviendo a x1 según el número de veces que sea ejecutada la interrupción.

