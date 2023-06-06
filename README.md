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
#### Descripción detallada:

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
#### Descripción detallada:

## Output
#### Códificación:
![image](https://github.com/DamianPerezB/Lab6/assets/89427173/1ea02dfc-2277-41f6-9467-6514f6db0a9c)
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
#### Descripción detallada:


## Diagrama del circuito:
![image](https://github.com/DamianPerezB/Lab6/assets/89427173/43475c5b-b9c1-42e5-bae7-dca48eeb227a)

# Descricpión de su funcionamiento:
El microcontrolador en su estado inicial, mantiene una cuenta ascendente en numeración binaria, la cual es representada de forma visual con ayuda de 10 leds.
Además consta de dos botones, cuyo funcionamiento es el siguiente.  
Botón 1: Al ser presionado, la cuenta cambia de ascendente a descendente.  
Botón 2: Al ser presionado, la velocidad con la que fluye la cuenta se modifica a x2, x4, x8 y volviendo a x1 según el número de veces que sea ejecutada la interrupción.

