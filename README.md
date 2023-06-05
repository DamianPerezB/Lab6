# LAB6: Manejo de interrupciones

*El siguiente repositorio contiene la documentación correspondiente a la actividad LAB6: Manejo de interrupciones.*

---

## El código utilizado consta de las siguientes funciones:
1) main
2) delay
3) Default_Handler
4) EXTI0_Handler
5) EXIT1_Handler
6) output.s
7) SysTick_Handler
8) Reset_Handler


# Funcionamiento del código

## main
#### Códificación:
#### Descripción detallada:

## delay
#### Códificación:
#### Descripción detallada:

## Default_Handler
#### Códificación:
![image](https://github.com/DamianPerezB/Lab6/assets/89427173/d3ad1323-ac63-4326-baf4-58de240718d6)
#### Descripción detallada:
Es una subrutina no implementada en ISR, es decir, será ejecutada cada vez que la interrupción apropiada no sea definida.

## SysTick_Handler
#### Códificación:
![image](https://github.com/DamianPerezB/Lab6/assets/89427173/2c369df5-03eb-4481-9e4f-4b059a5e4532)
#### Descripción detallada:
Es una excepción que se dispara cada vez que el reloj llega a 0. Se invoca de forma automática por el hardware del procesador cuando ocurre una interrupción del temporizador

## Reset_Handler
#### Códificación:
![image](https://github.com/DamianPerezB/Lab6/assets/89427173/e6f3e1f2-ea93-406a-89f9-0b3286a50aa9)
![image](https://github.com/DamianPerezB/Lab6/assets/89427173/1d19ea9e-18b5-4776-b2df-bd0193522b3d)

#### Descripción detallada:
Se encarga de la inicialización y configuración del sistema cuando ocurre la interrupción de reinicio (RESET). Es el punto de partida del programa y se ejecuta antes de cualquier otra rutina o función en el sistema.
En este caso se utilizan a los registros r8, r9 y r10 como variables locales, donde cada uno representa la velocidad, dirección y contador de leds respectivamente.
Al final de la misma se hace un llamado a la función main

## EXTI0_Handler
#### Códificación:
#### Descripción detallada:

## EXTI1_Handler
#### Códificación:
#### Descripción detallada:

## output
#### Códificación:
![image](https://github.com/DamianPerezB/Lab6/assets/89427173/0c897266-fbbf-44b7-bdb6-58dd0975cf83)
#### Descripción detallada:


## Diagrama del circuito:
![image](https://github.com/DamianPerezB/Lab6/assets/89427173/43475c5b-b9c1-42e5-bae7-dca48eeb227a)

# Descricpión de su funcionamiento:
El microcontrolador en su estado inicial, mantiene una cuenta ascendente en numeración binaria, la cual es representada de forma visual con ayuda de 10 leds.
Además consta de dos botones, cuyo funcionamiento es el siguiente.
Botón 1: Al ser presionado, la cuenta cambia de ascendente a descendente.
Botón 2: Al ser presionado, la velocidad con la que fluye la cuenta se modifica a x2, x4, x8 y volviendo a x1 según el número de veces que sea ejecutada la interrupción.

