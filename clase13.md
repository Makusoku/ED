# Haciendo la épica parte 4
## Ticos CTC

- Ahora vamos a usar el tico1 para observar el funcionamiento de 16 bits
- El compare match nos ayuda, solito se pone a 0
- Las patitas (OC1A, OC1B) responden segun la configuracion 

```
.equ TOP_tico1 = 1914
.equ f_io = 1000000
.equ N = 1
.equ f_do = 261
.equ ocr1a_do = f_io/2/n/f_do - 1

.cseg
.org 0

ldi r16, ( 0 << WGM11 | 0 << WGM10  | 0 << COM1A1 | 1 << COM1A0 )
out tccr1a, r16

ldi r16, ( 0 << WGM13 | 1 << WGM12  | 0 << CS12 | 0 << CS11 | 1 << CS10 )
out tccr1b, r16

ldi r16, high(ocr1a_do)
out ocr1ah, r16
ldi r16, low(ocr1a_do)
out ocr1al, r16

sbi r16, 5

dormammu:

rjmp dormammu
```
- Para obtener las frecuencias, solo alteras el top (ocr1A)

```
.equ do4 = 0x03BA
.equ si3 = 0x03F3
.equ la3 = 0x046F
.equ sol3 = 0x04FA
.equ fa3 = 0x0596
.equ mi3 = 0x05EB
.equ re3 = 0x06A5
.equ do3 = 0x0776

.equ f_io = 1000000
.equ N = 1
.equ ocr1a_do3 = f_io/2/n/do3 - 1
.equ ocr1a_re3 = f_io/2/n/re3 - 1
.equ ocr1a_mi3 = f_io/2/n/mi3 - 1
.equ ocr1a_fa3 = f_io/2/n/fa3 - 1
.equ ocr1a_sol3 = f_io/2/n/sol3 - 1
.equ ocr1a_la3 = f_io/2/n/la3 - 1
.equ ocr1a_si3 = f_io/2/n/si3 - 1
.equ ocr1a_do4 = f_io/2/n/do4 - 1


.cseg
.org 0

ldi r16, ( 0 << WGM11 | 0 << WGM10  | 0 << COM1A1 | 1 << COM1A0 )
out tccr1a, r16

ldi r16, ( 0 << WGM13 | 1 << WGM12  | 0 << CS12 | 0 << CS11 | 1 << CS10 )
out tccr1b, r16

sbi ddrd, 5
clr r16
out ddra, r16

loop:

in r16, pina

sbis pina, 0
rjmp next1
ldi r16, high(ocr1a_do3)
out ocr1ah, r16
ldi r16, low(ocr1a_do3)
out ocr1al, r16

next1:
sbis pina, 1
rjmp next2
ldi r16, high(ocr1a_re3)
out ocr1ah, r16
ldi r16, low(ocr1a_re3)
out ocr1al, r16

next2:
sbis pina, 2
rjmp next3
ldi r16, high(ocr1a_mi3)
out ocr1ah, r16
ldi r16, low(ocr1a_mi3)
out ocr1al, r16

next3:
sbis pina, 3
rjmp next4
ldi r16, high(ocr1a_fa3)
out ocr1ah, r16
ldi r16, low(ocr1a_fa3)
out ocr1al, r16

next4:
sbis pina, 4
rjmp next5
ldi r16, high(ocr1a_sol3)
out ocr1ah, r16
ldi r16, low(ocr1a_sol3)
out ocr1al, r16

next5:
sbis pina, 5
rjmp next6
ldi r16, high(ocr1a_la3)
out ocr1ah, r16
ldi r16, low(ocr1a_la3)
out ocr1al, r16

next6:
sbis pina, 6
rjmp next7
ldi r16, high(ocr1a_si3)
out ocr1ah, r16
ldi r16, low(ocr1a_si3)
out ocr1al, r16

next7:
sbis pina, 7
rjmp next8
ldi r16, high(ocr1a_do4)
out ocr1ah, r16
ldi r16, low(ocr1a_do4)
out ocr1al, r16

next8:
in r16, pina
cpi r16, 0
brne loop
ldi r16, 0
out ocr1ah, r16
ldi r16, 0
out ocr1al, r16


rjmp loop


dormammu:

rjmp dormammu
```

> Esta clase fue basicamente ejercicios