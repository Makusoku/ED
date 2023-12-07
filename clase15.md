# Haciendo la épica parte 6
- Tenemos que configurar la interrupción del Tico0
- Vector de interrucpcion 0x26
- Necesitamos usar el registro TIMSK 
- TIMSK,    el habilitador del compare match para el tico0

```
    ldi     r16,    (1<<OCIE0)
    out     TIMSK,  r16
```

- Es necesario activar el SEI, para habilitar los registros
- Mirar el codigo del muro
- Mientras mas grande es el preescalador, mayor es el rango de error

- Ahora configuramos el Tico1 para obtener las frecuencias que queremos
> TiCo1 CTC, N = 1, OC1A en toggle
- IMPORTANTE

```
    ldi     r17,    0x01
    ldi     r16,    0xff
    ; Guardar primero H y luego L
    out     tcnt1H, r17
    out     tcnt1L, r16
    ; Para leer primero L y luego H
    in      r16,    tcnt1L
    in      r16,    tcnt1H
```

```
.equ do4 = 0x03BA
.equ si3 = 0x03F3
.equ la3 = 0x046F
.equ sol3 = 0x04FA
.equ fa3 = 0x0596
.equ mi3 = 0x05EB
.equ re3 = 0x06A5
.equ do3 = 0x0000

.equ dir_notas_H = 0x0060
.equ dir_notas_L = 0x0070
.equ song = 0x0080


.cseg
 .org 0  RJMP start
 ; acá definimos las interrupciones que utilicemos
 .org 0x26 rjmp TiCo0_compare_match

 start:
 ldi  R16, high(ramend)
 out  SPH, R16    ; vector de int. de INT0
 ldi  R16, low(ramend)
 out  SPL, R16

 rcall save_notes

 rcall save_song

 ; configuración del TiCo0 en modo CTC con N=64 y OC0 desconectado
 ldi  R16, (1<<WGM01|0<<WGM00|0<<CS02|1<<CS01|1<<CS00)
 out  TCCR0, R16
 ldi  R16, 244
 out  OCR0, R16

 ; Configurar TiCo1 en modo CTC con N=1 y con OC1A en toggle
 ldi  R16, (0<<WGM11 | 0<<WGM10 | 0<<COM1A1 | 1<<COM1A0 | 0<<COM1B1 | 0<<COM1B0)
 out  TCCR1A, R16
 ldi  R16, (0<<WGM13 | 1<<WGM12 | 0<<CS12 | 0<<CS11 | 1<<CS10)
 out  TCCR1B, R16

 sbi  ddrD, 5; porque PD5 es OC1A, y tiene que estar como salida

 clr  R16
 out  OCR1AH, R16 ; mini-tarea: ¿qué frecuencia se genera cuando OCR1A=0?
 out  OCR1AL, R16

 ; configurar la interrupción del TiCo0
 ldi  R16, (1<<OCIE0)
 out  TIMSK, R16

 sei

 ; vuelvo a apuntar al inicio del espacio de RAM donde están las notas
 ldi  XH, high(song)
 ldi  XL, low(song)
 ldi  YH, high(dir_notas_H)
 ldi  YL, low(dir_notas_H)
 ldi  ZH, high(dir_notas_L)
 ldi  ZL, low(dir_notas_L)

 ld  R16, X+
 mov  R17, R16
 andi R17, 0b00011111 ; enmascaro y me quedo con la duración
 lsr  R16  ; cinco veces logical shift to the right
 lsr  R16
 lsr  R16
 lsr  R16
 lsr  R16

 add  YL,  R16
 add  ZL,  R16
 ld  R16, Y+
 out  OCR1AH, R16
 ld  R16, Z+
 out  OCR1AL, R16

 dormammu:
 rjmp dormammu

 ; ISR: Interruption sub-routine
 TiCo0_compare_match:

  dec  R17
  brne sigue_esperando

  ld  R16, X+
  mov  R17, R16
  andi R17, 0b00011111 ; enmascaro y me quedo con la duración
  lsr  R16  ; cinco veces logical shift to the right
  lsr  R16
  lsr  R16
  lsr  R16
  lsr  R16

  ldi  YH, high(dir_notas_H)
  ldi  YL, low(dir_notas_H)
  ldi  ZH, high(dir_notas_L)
  ldi  ZL, low(dir_notas_L)

  ; moviendo los punteros Y y Z para que apunten a la frecuencia corrrecta
  add  YL,  R16
  add  ZL,  R16
  ld  R16, Y+
  out  OCR1AH, R16

  cpi  R16, 0xFF
  brne sigue
  cli
  sigue:

  ld  R16, Z+
  out  OCR1AL, R16

  sigue_esperando:

 reti



 save_song:
  ldi  XH, high(song)
  ldi  XL, low(song)

  ldi  R16, 0b00011111
  st  X+,  R16
  ldi  R16, 0b00111111
  st  X+,  R16
  ldi  R16, 0b01011111
  st  X+,  R16
  ldi  R16, 0b01111111
  st  X+,  R16
  ldi  R16, 0b11111111
  st  X+,  R16

 ret



 save_notes:
  ldi  XH, high(dir_notas_H)
  ldi  XL, low(dir_notas_H)
  ldi  YH, high(dir_notas_L)
  ldi  YL, low(dir_notas_L)

  ldi R16, high(do4)
  st X+, R16
  ldi R16, low(do4)
  st Y+, R16
  ldi R16, high(si3)
  st X+, R16
  ldi R16, low(si3)
  st Y+, R16
  ldi R16, high(la3)
  st X+, R16
  ldi R16, low(la3)
  st Y+, R16
  ldi R16, high(sol3)
  st X+, R16
  ldi R16, low(sol3)
  st Y+, R16
  ldi R16, high(fa3)
  st X+, R16
  ldi R16, low(fa3)
  st Y+, R16
  ldi R16, high(mi3)
  st X+, R16
  ldi R16, low(mi3)
  st Y+, R16
  ldi R16, high(re3)
  st X+, R16
  ldi R16, low(re3)
  st Y+, R16
  ldi R16, high(do3)
  st X+, R16
  ldi R16, low(do3)
  st Y+, R16

 ret

```