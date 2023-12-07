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

- El código esta en miro