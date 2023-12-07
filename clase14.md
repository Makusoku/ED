# Haciendo la épica parte 5
## FLASH
- La flash es la memoria de programa (16 bits)
- Solo funciona con el puntero Z
- Tenemos 2 directivas: .db .dw
- .db -> Para guardar bytes (16 bits o sale warning)
- .dq -> Para guardar words

```
    .cseg
        .org 15

    rjmp    start
        mensaje:
            .db     10
            .db     0xff
            .db     0b1111, 0b1011

    start:
        ldi     r16,    high(2*mensaje)
        ldi     zH,     r16
        ldi     r16,    low(2*mensaje)
        ldi     zL,     r16

        lpm     r16,    z+
        lpm     r16,    z+
        lpm     r16,    z+
```
```
.cseg
.org 0
rjmp llego_tu_carry

luces:
.db 0b00000001, 0b00000010
.db 0b00000100, 0b00001000
.db 0b00010000, 0b00100000
.db 0b01000000, 0b10000000

llego_tu_carry:
    ldi R16,high(ramend)
    out SPH,R16
    ldi R16,low(ramend)
    out SPL,R16

ldi ZH, high(2*luces)
ldi ZL, low(2*luces)

;configurar todo el puerto A como salida
    SER R16
    OUT ddrA,r16

lpm R16, Z+
out portA, R16
RCALL delay
RCALL delay

lpm R16, Z+
out portA, R16
RCALL delay
RCALL delay

lpm R16, Z+
out portA, R16
RCALL delay
RCALL delay

lpm R16, Z+
out portA, R16
RCALL delay
RCALL delay

lpm R16, Z+
out portA, R16
RCALL delay
RCALL delay
lpm R16, Z+
out portA, R16
RCALL delay
RCALL delay

lpm R16, Z+
out portA, R16
RCALL delay 
RCALL delay

lpm R16, Z+
out portA, R16
RCALL delay
RCALL delay

    bucle:
    rjmp bucle


    delay:
push R16
push R17
ldi R16,255
ldi R17,255
lazo_2:
lazo_1:
dec R16
breq end_lazo_1
rjmp lazo_1
end_lazo_1:
dec R17
breq end_lazo_2
ser R16
RJMP lazo_2
end_lazo_2:
pop R17
POP R16
RET
```

## Interrupciones
- Son hardware
- SEI  -> Habilitador de interrupciones
- RETI -> Como el RET pero para interrupciones
- Los ticos generan interrupcion cuando desbordan
- Compare match generan interrupciones
- Existen vectores predifinidos por los puertos de entrada 0x02, 0x04
- Se configura con MCUCR, GICR

```
    .cseg
    .org    0x00    rjmp inicio
    ;vectores de interrupcion
    .org    0x02    rjmp aaa
    .org    0x02    rjmp bbb

    inicio:
    ldi     r16,    (1<<ISC11|1<<ISC10|1<<ISC01|1<<ISC00)
    out     MUCR,   r16

    ldi     r16,    (1<<INT1|1<<INT0)
    out     GICR,   r16

```