# Haciendo la épica
## Instrucciones
- Existen instrucciones y directivas en assembler
- Los primeros 32 espacios de memoria del atmega son para los registros
- Las etiquetas no ocupan memoria 
- Un ejemplo puede ser: 
```
    .cseg
        ldi R20,    20
        asr R20
```
- Se guardan en direcciones de memoria
> Usar chatgpt para encontrar las instrucciones y verificarlas en el dataSheet
- Es importante visusalizar los registros para poder debugear el programa

## Recuperacion
- Enseñan el uso del simulide
- `.org` Establece el inicio de la direccion de memoria para empezar el programa. IMPORTANTE: Se multiplica por "2", debido a que la memoria de programa (memoria FLASH), a diferencia de la memoria de datos (RAM) es de 16 bits, osea 2 bytes.

### Puertos de entrada y salida
- Son 64 puertos de entrada y salida
- Los registros sirven para configurar los perifericos en el atmega
- Hay 3 registros por puertos: portA, ddrA, pinA
- Cada registro tiene 8 bits
- Estableces el registro como entrada o salida con ddrA
- Entrada es 0,     pinA
- Salida es 1,      portA

```
    LDI r16,    0b11111111 ;
    OUT ddrA,   r16    ; Meter un dato
    LDI r16,    25
    OUT portA,  r16
    IN  pinA    ; Leer datos 
```

- Puedes usar CLR para limpiar el registro, todo 0
- Puedes usar SER para tener todo el registro con 1
- Puedes usar COM para tener el complemento a 1
- Puedes usar INC para incrementar en 1 un registro
- Puedes usar DEC para decrementar en 1 un registro
- Puedes usar SBI para establecer el valor de un puerto en 1
- Puedes usar CBI para establecer el valor de un puerto en 0
- SBIS  Si es 1 skip
- SBIC  Si es 0 skip

### Conclusiones
. Basicamente esta clase es sobre instrucciones básicas en el atmega, también enseñan que las instrucciones ocupan memoria, sin embargo las etiquetas no. 

--- 

`Simple`
