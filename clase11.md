# Haciendo la épica parte 2
## RAM
. Memoria de datos
. Los primero 96 espacios estan ocupados por los registros multipropositos y los registros
. Empieza del 0x60, osea desde el 96 :v
. 32 multipropositos
. 64 de entrada y salida
. Para la RAM tiene 4 instrucciones
. LDS Rd,   k   -> Leer datos   
. STS  k,   Rd  -> Guardar datos
. El "k" es una dirección de memoria

```
    .cseg
        .org    0
        ldi     r16,    0x23
        sts     0x60,   r16; guarda el valor del r16 en la direccion 0x60
        lds     r16,    0x60; leer el dato guardado en 0x60
```

. Esas instrucciones (LDS, STS) no son muy útiles a la hora de guardar varios datos. Ahora usaremos punteros
. Los 6 últimos registros (R26 - R31) son 3 punteros:
    . X : R27:R26
    . Y : R29:R28
    . Z : R31:R30

. LD    X,  Rd -> Guarda el valor en la memoria a la que apunta el puntero
. ST    Rd, X  -> Leer el valor de la memoria a la que apunta el puntero

```
    .cseg
        .org    0
        ldi     r27,    0x00; XH
        ldi     r26,    0x70; XL
        ldi     r16,    12
        st      X,      r16  
```
. Puedes hacer un postincremento (X+) o un predecremento (-X)
. Puedes usar BREQ como un indicador de que un registro llego a 0 (la bandera Z es 1)

## PILA
- Es una estructura de datos LIFO 
- push -> ingresa dato
- pop  -> lee, NO ELIMINA, el ultimo dato ingresado
- stack pointer: puntero especial para la pila, registro de entrada y salida, se actualiza automaticamente cuando guardas valores

```
    .cseg
        .org    0
        ldi    r16,    0x00
        out    sph,    r16
        ldi    r16,    0x80
        out    spl,    r16
```

. Tambien puede ser con constantes:

```
    .equ    dir1 = 0x0080
    .cseg
        .org    0
        ldi    r16,    high(dir1)
        out    sph,    r16
        ldi    r16,    low(dir1)
        out    spl,    r16

        ldi     r16,    21
        push    r16
        pop     r16; Lee los valores, si haces otro push vas a "chancar"
```

. Puede ocurrir un stack overflow que es cuando sobreescribimos los valores de un espacio de memoria al hacer push con la pila. Para disminuir el riesgo, el sp debe apuntar al valor más alto de la RAM, osea al RAMEND

## SUBRUTINAS
. En resumen, son funciones que son llamadas en el programa, es para evitar el código repetido
. RCALL -> Llama a la subrutina
. RET   -> Regresa al comportamiento
. Usa la pila, el program counter (indica en que instruccion estoy), por lo que es importante indicar el stack pointer

```
    .cseg
        .org    0
        ldi    r16,    high(RAMEND)
        out    sph,    r16
        ldi    r16,    low(RAMEND)
        out    spl,    r16

        rcall sub

        dorm:
        rjmp    dorm

        sub:
            push    r16
            nop
            nop
            pop     r16
        ret
```
. Si usas un push en la subrutina, necesitas usar un pop para no modificar el program counter
. Se usa el push pop para salvar valores de los registros
