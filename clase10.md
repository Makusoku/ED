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

### Basicamente esta clase es sobre instrucciones básicas en el atmega, también enseñan que las instrucciones ocupan memoria, sin embargo las etiquetas no. 

`Simple`
