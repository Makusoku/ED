# Haciendo la épica parte 3
## TICOS
- Timer Counter
- Son perifericos de Atmega, osea son registros
- Para esta parte es importante leer el DataSheet
- Tenemos tres ticos
- Tico 0 y 2 son de 8 bits, el Tico1 es de 16 bits
- La cuenta esta en TCNTn, donde n es 0, 1 o 2
- Como el registro es de 8 bits, el tico 1 entra en 2 registros (TCNT1H, TCNT1L)
- Tenemos un registro de control: TCCRn
- Existen mas registros, lee :v

- Hay 4 modos, pero los principales son normal y ctc
- En normal, el contador cuenta hasta 255 
- El bit clock select (N), es importante
- El preescalador N, 
```
    ;configurar tico0
    ;modo:      normal
    ;patita:    desconectada
    ;clock:     interno y directo (1MHz)
    
    .cseg
        .org    0
        ldi     r16,    0b00000001
        out     TCCR,   r16

        dorm: 
            nop
            nop
        rjmp    dorm
```

```
.cseg
    .org    0
    ldi        r16,    (0 << WGM01 | 0 << WGM00 | 0 << COM01 | 0 << COM00  | 1 << CS02 | 0 << CS01 | 1 << CS00 )
    out        tccr0,    r16
    ser        r16
    out        ddra,    r16
    clr        r16
    out        porta,    r16

    ga:
        in        r16,    tcnt0
        cpi        r16,    255
        breq    mostrar
    rjmp    ga

    mostrar:
        com        r17
        clr        r16
        out        porta,    r17
        out        tcnt0,    r16
    rjmp    ga
```

