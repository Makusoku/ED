# Con fe
```
.equ do5 = 0x01DC
.equ si4 = 0x01F9
.equ la4 = 0x0237
.equ la4b = 0x0258
.equ sol4 = 0x027C
.equ sol4b = 0x02A2
.equ fa4 = 0x02CA
.equ mi4 = 0x02F5
.equ mi4b = 0x0322
.equ re4 = 0x0352
.equ do4 = 0x03BA
.equ si3 = 0x03F3
.equ si3b = 0x042F 
.equ la3 = 0x046F
.equ la3b = 0x04B2
.equ sol3 = 0x04FA
.equ fa3 = 0x0596
.equ mi3 = 0x05EB
.equ re3 = 0x06A5
.equ do3 = 0x0776
.equ si2 = 0x07E7
.equ mi3b = 0x0646
.equ re4b = 0x0384
.equ sol3b = 0x0546
.equ si4b = 0217



.cseg
	.org 0x00 rjmp start

	.org 0x26 rjmp Tico0_ON_COMPARE_MATCH

	.org 0x30

;guardamos las notas en la FLASH a partir de 0x30
guardar_notas:
	.dw do5; 0
	.dw si4; 1
	.dw la4; 2
	.dw la4b ;3
	.dw sol4 ;4
	.dw sol4b ;5
	.dw fa4 ;6
	.dw mi4 ;7
	.dw mi4b ;8
	.dw re4 ;9
	.dw do4 ;10
	.dw si3 ;11
	.dw si3b ;12
	.dw la3 ;13
	.dw la3b ;14
	.dw sol3 ;15
	.dw fa3 ;16
	.dw mi3 ;17
	.dw mi3b ;18
	.dw re3 ;19
	.dw do3 ;20
	.dw 0 ;21
	.dw si2 ;22
	.dw re4b ;23
	.dw sol3b ;24
	.dw si4b ;25


guardar_codigo_notas:
	.dw 0x0C08 
	.dw 0x1504 
	.dw 0x0C08 ;sib3
	.dw 0x1504 
	
	.dw 0x0808 
	.dw 0x1504 
	.dw 0x0820 
	.dw 0x1504 
	
	.dw 0x0C15
	.dw 0x1504 
	
	.dw 0x0810
	.dw 0x1504 
	
	.dw 0x0620
	.dw 0x1504 
	
	.dw 0x0808 ;mi4b
	.dw 0x1504 
	.dw 0x0608 ;fa4
	.dw 0x1504 
	.dw 0x0308 ;la4b
	.dw 0x1504 
	.dw 0x0408 ;sol4
	.dw 0x1504 
	.dw 0x0810
	.dw 0x1504 
	
	.dw 0x0E08 
	.dw 0x1504 
	.dw 0x0E08 
	.dw 0x1504 
	.dw 0x0C08
	.dw 0x1504 
	.dw 0x0C08
	.dw 0x1504 
	.dw 0x0C08
	.dw 0x1504 
	.dw 0x0C08
	.dw 0x1504 

	.dw 0x0808 
	.dw 0x1504 
	.dw 0x0820 
	.dw 0x1504 
	
	.dw 0x0C15
	.dw 0x1504 
	
	.dw 0x0810
	.dw 0x1504 
	
	.dw 0x0620
	.dw 0x1504 

	.dw 0x0608 ;fa4
	.dw 0x1504
	.dw 0x0308 ;la4b
	.dw 0x1504 
	.dw 0x0408 ;sol4
	.dw 0x1504 
	.dw 0x0608 ;fa4
	.dw 0x1504
	.dw 0x0808 ;mi4b
	.dw 0x1504 
	.dw 0x0608 ;fa4
	.dw 0x1504
	.dw 0x0820 ;mi4b
	.dw 0x1504 

	.dw 0x0610 ;fa4
	.dw 0x1504
	.dw 0x0810 ;mi4b
	.dw 0x1504 

	.dw 0x0408 ;sol4
	.dw 0x1504 
	.dw 0x0608 ;fa4
	.dw 0x1504
	.dw 0x0808 ;mi4b
	.dw 0x1504 
	.dw 0x0608 ;fa4
	.dw 0x1504
	.dw 0x0808 ;mi4b
	.dw 0x1504 
	.dw 0x0608 ;fa4
	.dw 0x1504
	.dw 0x0408 ;sol4
	.dw 0x1504 

	.dw 0x0408 ;sol4
	.dw 0x1504 
	.dw 0x0608 ;fa4
	.dw 0x1504
	.dw 0x0808 ;mi4b
	.dw 0x1504 
	.dw 0x0608 ;fa4
	.dw 0x1504
	.dw 0x0508 ;mi4b
	.dw 0x1504 
	.dw 0x0608 ;fa4
	.dw 0x1504
	.dw 0x0820 ;mi4b
	.dw 0x1504


	.dw 0x0E08 ;la3b
	.dw 0x1504 
	.dw 0x0C08 ;si3b
	.dw 0x1504 
	.dw 0x0E08 ;la3b
	.dw 0x1504
	.dw 0x0F08 ;sol3
	.dw 0x1504 
	.dw 0x1008 ;fa3
	.dw 0x1504 
	.dw 0x1208 ;mi3b
	.dw 0x1504 

	.dw 0x1708 ;re4b
	.dw 0x1504 
	.dw 0x0A08 ;do4
	.dw 0x1504 
	.dw 0x0C08 ;si3b
	.dw 0x1504 
	.dw 0x0E08 ;la3b
	.dw 0x1504 
	.dw 0x0C08 ;si3b
	.dw 0x1504 

	.dw 0x0C08 ;si3b
	.dw 0x1504 
	.dw 0x0C08 ;si3b
	.dw 0x1504 
	.dw 0x0E08 ;la3b
	.dw 0x1504 
	.dw 0x0F08 ;sol3
	.dw 0x1504 
	.dw 0x1008 ;fa3
	.dw 0x1504 
	.dw 0x1208 ;mi3b
	.dw 0x1504 

	.dw 0x1208 ;mi3b
	.dw 0x1504 
	.dw 0x1008 ;fa3
	.dw 0x1504 
	.dw 0x1808 ;sol3b
	.dw 0x1504 
	.dw 0x0C08 ;si3b
	.dw 0x1504 
	.dw 0x0E08 ;la3b
	.dw 0x1504 
	.dw 0x1808 ;sol3b
	.dw 0x1504 
	.dw 0x0E08 ;la3b
	.dw 0x1504 

	.dw 0x0C08 ;si3b
	.dw 0x1504 
	.dw 0x0C08 ;si3b
	.dw 0x1504 
	.dw 0x0C08 ;si3b
	.dw 0x1504 
	.dw 0x0E08 ;la3b
	.dw 0x1504 
	.dw 0x0F08 ;sol3
	.dw 0x1504
	.dw 0x1008 ;fa3
	.dw 0x1504 
	.dw 0x1208 ;mi3b
	.dw 0x1504 

	.dw 0x1208 ;mi3b
	.dw 0x1504 
	.dw 0x1208 ;mi3b
	.dw 0x1504 
	.dw 0x0810 ;mi4b
	.dw 0x1504 
	.dw 0x0810 ;mi4b
	.dw 0x1504 
	.dw 0x0608 ;fa4
	.dw 0x1504
	.dw 0x0908 ;re4
	.dw 0x1504 
	.dw 0x0810 ;mi4b
	.dw 0x1504 

	.dw 0x0908 ;re4
	.dw 0x1504 
	.dw 0x0908 ;re4
	.dw 0x1504 
	.dw 0x0810 ;mi4b
	.dw 0x1504 
	.dw 0x0810 ;mi4b
	.dw 0x1504 
	.dw 0x0908 ;re4
	.dw 0x1504 
	.dw 0x0A08 ;do4
	.dw 0x1504 
	.dw 0x0C08 ;si3b
	.dw 0x1504 
	.dw 0x0F08 ;sol3
	.dw 0x1504
	.dw 0x0A08 ;do4
	.dw 0x1504
	.dw 0x1008 ;fa3
	.dw 0x1504 
	.dw 0x0F08 ;sol3
	.dw 0x1504
	.dw 0x0E08 ;la3b
	.dw 0x1504 
	.dw 0x0C08 ;si3b
	.dw 0x1504 
	.dw 0x0F08 ;sol3
	.dw 0x1504
	.dw 0x1008 ;fa3
	.dw 0x1504 
	.dw 0x1208 ;mi3b
	.dw 0x1504 

	.dw 0x0C08 ;si3b
	.dw 0x1504 
	.dw 0x0A08 ;do4
	.dw 0x1504
	.dw 0x1708 ;re4b
	.dw 0x1504 
	.dw 0x0608 ;fa4
	.dw 0x1504
	.dw 0x0608 ;fa4
	.dw 0x1504
	.dw 0x0820 ;mi4b
	.dw 0x1504
	.dw 0x0820 ;mi4b
	.dw 0x1504
	.dw 0x0A08 ;do4
	.dw 0x1504
	.dw 0x0C08 ;si3b
	.dw 0x1504 
	.dw 0x0E08 ;la3b
	.dw 0x1504 
	.dw 0x0C08 ;si3b
	.dw 0x1504 
	.dw 0x0F08 ;sol3
	.dw 0x1504
	.dw 0x1008 ;fa3
	.dw 0x1504 
	.dw 0x1208 ;mi3b
	.dw 0x1504 

	.dw 0x0C08 ;si3b
	.dw 0x1504 
	.dw 0x0A08 ;do4
	.dw 0x1504
	.dw 0x1708 ;re4b
	.dw 0x1504 
	.dw 0x0608 ;fa4
	.dw 0x1504
	.dw 0x0608 ;fa4
	.dw 0x1504
	.dw 0x0710 ;mi4
	.dw 0x1504
	.dw 0x0710 ;mi4
	.dw 0x1504
	.dw 0x0608 ;fa4
	.dw 0x1504
	.dw 0x0408 ;sol4
	.dw 0x1504 
	.dw 0x0308 ;la4b
	.dw 0x1504

	.dw 0xFFFF ;acaba la rola

start:
;configuracion del puerto PD5 como salida
ldi r16,0b000100000
out DDRD,r16

;configuracion del TICO1
;modo CTC,toggle on compare match,N=1
ldi r16,(1<<COM1A0)
out TCCR1A,r16
;ldi r16,(1<<WGM12||1<<CS10)
ldi r16,0b00001001
out TCCR1B,r16
;configuracion del stack
ldi r16,high(RAMEND)
out SPH,r16
ldi r16,low(RAMEND)
out SPL,r16
;configuraqcion del TICO0 -> va a implementar la duracion de las notas
;modo CTC, 0c0 desconectado,N=64
clr r16
ldi r16,(1<<WGM01|1<<CS00|1<<CS01)
out TCCR0,r16
;El TOP va a ser 244 para lograr la duracion de la semifusa aprox con N=64
ldi r16,244
out OCR0,r16
;Configuramos la interrupcion del TICO0
ldi r16,(1<<OCIE0)
out TIMSK,r16
;habilitador universal de interrupciones
sei

clr r20 ;contador para el codigo de notas
;empezamos con el contador en 0 pues vamos a leer la instruccion 0
;nos situamos al inicio de donde guardamos el codigo de notas
ldi ZH,high(2*guardar_codigo_notas)
ldi ZL,low(2*guardar_codigo_notas)
;leemos lo que está en Z 
lpm r16,Z+ ;low(codigo) -> o sea la duracion  
lpm r17,Z ;high(codigo) -> o sea la nota
;ahora situamos a Z en donde están las notas
ldi ZH,high(2*guardar_notas)
ldi ZL,low(2*guardar_notas)
add ZL,r17 ;nos situamos donde está la nota que queremos (hay que sumar el doble pues en la flash asi se guarda)
add ZL,r17
lpm r18,Z+ ;obtenemos la parte low nota que queremos
lpm r19,Z  ;obtenemos la parte high de la nota que queremos

out OCR1AH,r19
out OCR1AL,r18

bucle:
	
	cpi r20,0xFF
	brne bucle
	cli
	clr r23
	out OCR1AH,r23 ;apagamos el sonido :v
	out OCR1AL,r23	
	out DDRD,r23 ;apagamos el sonidito 
	ser r16
	out DDRB, r16
	ldi r16, 0b11100111
	out PORTB, r16
	rjmp bucle




Tico0_ON_COMPARE_MATCH:
	dec r16
	brne seguir_con_la_nota
	inc r20

	;inc r20 ;incrementamos el contador de codigo de notas
	;cpi r20,13
	;brne seguir_interrupcion
	;rjmp seguir_con_la_nota
	seguir_interrupcion:
	;nos situamos al inicio de donde guardamos el codigo de notas
	ldi ZH,high(2*guardar_codigo_notas)
	ldi ZL,low(2*guardar_codigo_notas)
	
	clr r16
	add ZL,r20 ;nos situamos donde está el codigo que queremos (hay que sumar el doble pues en la flash asi se guarda) ;terrible:hubo desborde en la suma
	adc ZH,r16
	add ZL,r20
	adc ZH,r16
	

	;leemos lo que está en Z 
	lpm r16,Z+ ;low(codigo) -> o sea la duracion  
	lpm r17,Z ;high(codigo) -> o sea la nota
	cpi r16,0xFF
	breq segunda_comparacion
	continua:	
	;ahora situamos a Z en donde están las notas
	ldi ZH,high(2*guardar_notas)
	ldi ZL,low(2*guardar_notas)
	add ZL,r17 ;nos situamos donde está la nota que queremos (hay que sumar el doble pues en la flash asi se guarda)
	add ZL,r17
	lpm r18,Z+ ;obtenemos la parte low nota que queremos
	lpm r19,Z  ;obtenemos la parte high de la nota que queremos

	out OCR1AH,r19
	out OCR1AL,r18

	seguir_con_la_nota:
reti


segunda_comparacion:
cpi r17,0xFF
brne continua
ldi r20,0xFF
rjmp seguir_con_la_nota
```

```
.equ do5 = 0x01DC
.equ si4 = 0x01F9
.equ la4 = 0x0237
.equ sol4 = 0x027C
.equ fa4 = 0x02CA
.equ mi4 = 0x02F5
.equ re4 = 0x0352
.equ do4 = 0x03BA
.equ si3 = 0x03F3
.equ la3 = 0x046F
.equ sol3 = 0x04FA
.equ fa3 = 0x0596
.equ mi3 = 0x05EB
.equ re3 = 0x06A5
.equ do3 = 0x0776
.equ si2 = 0x07E7



.cseg
 .org 0  rjmp start

 .org 0x26 rjmp semifusa_TiCo0

 .org 0x30

  freqs_en_flash:
   .dw do5
   .dw si4
   .dw la4
   .dw sol4
   .dw fa4
   .dw mi4
   .dw re4
   .dw do4
   .dw si3
   .dw la3
   .dw sol3
   .dw fa3
   .dw mi3
   .dw re3
   .dw do3
   .dw si2
   .dw 0

  song_in_flash:
   .dw  0xaaaa
   .dw  0xaaaa
   .dw  0xaaaa
   .dw  0xaaaa
   .dw  0xaaaa
   .dw  0xaaaa
   .dw  0xaaaa
   .dw  0xaaaa
   .dw  0xaaaa
   .dw  0xaaaa
   .dw  0



start:

 ldi  R16, high(ramend)
 out  SPH, R16
 ldi  R16, low(ramend)
 out  SPL, R16

 sei

 ; puerto B como salida
 ser  R16
 out  ddrB, R16

 ; puerto A como entrada
 com  R16
 out  ddrA, R16

 ; configurar OC1A como salida
 sbi  ddrD, 5

 ; apuntar Z a los datos en flash
 ldi  ZH,  high(2*freqs_en_flash)
 ldi  ZL,  low(2*freqs_en_flash)

 ; configurar TiCo1 en CTC con TOP=OCR1A y N=1
 ldi  R16, (0<<WGM11 | 0<<WGM10 | 0<<COM1A1 | 1<<COM1A0 | 0<<COM1B1 | 0<<COM1B0)
 out  TCCR1A, R16
 ldi  R16, (0<<WGM13 | 1<<WGM12 | 0<<CS12 | 0<<CS11 | 1<<CS10)
 out  TCCR1B, R16

 ;configuraciÃ³n del TiCo0 en modo CTC con N=64 y OC0 desconectado
 ldi R16, (1<<WGM01|0<<WGM00|0<<CS02|1<<CS01|1<<CS00)
 out TCCR0, R16
 ldi R16, 244
 out OCR0, R16

 ldi R16, (1<<OCIE0)
 out TIMSK, R16



 lpm  R16, Z+ ; low(do5)
 lpm  R17, Z+ ; high(do5)
 out  OCR1AH, R17 ; siempre se escribe primero el H
 out  OCR1AL, R16

 ldi  R18, 32 ; contador de semifusas

dormammu:
 rjmp dormammu


semifusa_TiCo0:
 dec  R18
 brne sigue_tu_camino_ninja

  cli
  ; configurar TiCo1 en CTC con TOP=OCR1A y N=1
  ldi  R16, (0<<WGM11 | 0<<WGM10 | 0<<COM1A1 | 1<<COM1A0 | 0<<COM1B1 | 0<<COM1B0)
  out  TCCR1A, R16
  ldi  R16, (0<<WGM13 | 1<<WGM12 | 0<<CS12 | 0<<CS11 | 0<<CS10)
  out  TCCR1B, R16

  ldi  R16, 0b11100111
  out  portB, R16

  cbi  ddrD, 5

 sigue_tu_camino_ninja:
reti
```

```
.equ do5 = 0x01DC
.equ si4 = 0x01F9
.equ la4 = 0x0237
.equ sol4 = 0x027C
.equ fa4 = 0x02CA
.equ mi4 = 0x02F5
.equ re4 = 0x0352
.equ do4 = 0x03BA
.equ si3 = 0x03F3
.equ la3 = 0x046F
.equ sol3 = 0x04FA
.equ fa3 = 0x0596
.equ mi3 = 0x05EB
.equ re3 = 0x06A5
.equ do3 = 0x0776
.equ si2 = 0x07E7



.cseg
 .org 0  rjmp start

 .org 0x26 rjmp semifusa_TiCo0

 .org 0x30

  freqs_en_flash:
   .dw do5
   .dw si4
   .dw la4
   .dw sol4
   .dw fa4
   .dw mi4
   .dw re4
   .dw do4
   .dw si3
   .dw la3
   .dw sol3
   .dw fa3
   .dw mi3
   .dw re3
   .dw do3
   .dw si2


start:

 ldi  R16, high(ramend)
 out  SPH, R16
 ldi  R16, low(ramend)
 out  SPL, R16

 sei

 ; puerto B como salida
 ser  R16
 out  ddrB, R16

 ; puerto A como entrada
 com  R16
 out  ddrA, R16

 ; configurar OC1A como salida
 sbi  ddrD, 5

 ; apuntar Z a los datos en flash
 ldi  ZH,  high(2freqs_en_flash)
 ldi  ZL,  low(2freqs_en_flash)

 ; configurar TiCo1 en CTC con TOP=OCR1A y N=1
 ldi  R16, (0<<WGM11 | 0<<WGM10 | 0<<COM1A1 | 1<<COM1A0 | 0<<COM1B1 | 0<<COM1B0)
 out  TCCR1A, R16
 ldi  R16, (0<<WGM13 | 1<<WGM12 | 0<<CS12 | 0<<CS11 | 1<<CS10)
 out  TCCR1B, R16

 lpm  R16, Z+ ; low(do5)
 lpm  R17, Z+ ; high(do5)
 out  OCR1AH, R17 ; siempre se escribe primero el H
 out  OCR1AL, R16

 lpm  R16, Z+ ; low(si4)
 lpm  R17, Z+ ; high(si4)
 out  OCR1AH, R17 ; siempre se escribe primero el H
 out  OCR1AL, R16

 ;configuración del TiCo0 en modo CTC con N=64 y OC0 desconectado
  ldi R16, (1<<WGM01|0<<WGM00|0<<CS02|1<<CS01|1<<CS00)
  out TCCR0, R16
  ldi R16, 244
  out OCR0, R16

  ldi R16, (1<<OCIE0)
  out TIMSK, R16


 dormammu:
 rjmp dormammu


 semifusa_TiCo0:
 inc R25
 reti
```

```
.equ do5 = 0x01DC
.equ si4 = 0x01F9
.equ la4 = 0x0237
.equ sol4 = 0x027C
.equ fa4 = 0x02CA
.equ mi4 = 0x02F5
.equ re4 = 0x0352
.equ do4 = 0x03BA
.equ si3 = 0x03F3
.equ la3 = 0x046F
.equ sol3 = 0x04FA
.equ fa3 = 0x0596
.equ mi3 = 0x05EB
.equ re3 = 0x06A5
.equ do3 = 0x0776
.equ si2 = 0x07E7

.cseg
 .org 0 rjmp start

 .org 0x30

  datos_en_flash:
   .dw do5
   .dw si4
   .dw la4
   .dw sol4
   .dw fa4
   .dw mi4
   .dw re4
   .dw do4
   .dw si3
   .dw la3
   .dw sol3
   .dw fa3
   .dw mi3
   .dw re3
   .dw do3
   .dw si2

start:

 ; configurar puerto B como salida
 ser  R16
 out  ddrB, R16

 ; configurar puerto A como entrada
 com  R16
 out  ddrA, R16

 ; configurar OC1A como salida
 sbi  ddrD, 5

 ; apuntar Z a los datos en flash
 ldi  ZH,  high(2datos_en_flash)
 ldi  ZL,  low(2datos_en_flash)

 ; configurar TiCo1 en modo CTC con TOP=OCR1A
 ldi  R16, (0<<WGM11 | 0<<WGM10 | 0<<COM1A1 | 1<<COM1A0 | 0<<COM1B1 | 0<<COM1B0)
 out  TCCR1A, R16
 ldi  R16, (0<<WGM13 | 1<<WGM12 | 0<<CS12 | 0<<CS11 | 1<<CS10)
 out  TCCR1B, R16

 lpm  R16, Z+
 lpm  R17, Z+
 out  OCR1AH, R17
 out  OCR1AL, R16


 dormammu:
 rjmp dormammu
```