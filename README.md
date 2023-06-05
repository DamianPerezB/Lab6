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
#### Descripción detallada:

## Reset_Handler
#### Códificación:
#### Descripción detallada:

## EXTI0_Handler
#### Códificación:
#### Descripción detallada:

## EXTI1_Handler
#### Códificación:
#### Descripción detallada:

## output
#### Códificación:
#### Descripción detallada:


## Diagrama del circuito:
![ADD_page-0001](https://github.com/DamianRPG/Lab5/assets/126529855/9685ae01-5383-47ab-bb22-805555e3bf0d)

# Descricpión de circuito:
- Puertos de entrada: PA10 y PA11.
- Puertos de salida: PA0 - PA9.
- Una vez definidos los puertos de salida, estos harán conexión con la parte positiva de los leds (el ánodo); por otra parte, cada una de sus partes negativas (el cátodo), tendrán una conexión a una resistencia de 220OMS, esto con el fin de evitar que el sistema sufra sobrecargas. El pin G (tierra) alimentará a estos resistores.
Mientras tanto los buttons, que constan de dos pines, tendrán una conexión al pin de entrada correspondiente al STM32f103c8t6; mientras que el restante estará conectado al pin 3.3 (voltaje emitido por el microcontrolador).

