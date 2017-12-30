
**Título:** spi | **Categoría:** Miscelanea | **Nivel:** fácil

**Autor:** blondbyte

> **Enunciado:**
>
> I used to be a hero. Now I can't even handle this: Mitschnitt
>
> [`spi_zahlensender.ogg`](spi_zahlensender.ogg)

---

#### Resolución

Lo primero es comprobar con el comando `file` que el contenido del fichero adjunto es efectivamente de audio:
```
root@blondbyte# file spi_zahlensender.ogg
spi_zahlensender.ogg: Ogg data, Vorbis audio, mono, 44100 Hz, ~80000 bps, created by: Xiph.Org libVorbis I
```
Al reproducirlo se escucha una persona leyendo una secuencia de dígitos, en la que se aprecia que hay ligeros parones cada 2-3 dígitos.
```
76 83 48 116
76 105 52 103
76 83 48 116
76 83 52 103
76 105 48 117
76 83 65 116
76 83 48 116
76 105 65 116
76 105 48 117
76 83 52 103
76 83 48 116
76 83 48 103
76 83 52 117
76 83 65 117
76 83 52 117
73 67 48 117
76 83 52 116
76 105 65 116
76 83 48 117
73 67 48 116
76 83 48 116
73 67 48 117
76 83 52 116
76 105 65 116
76 83 48 116
76 83 65 116
76 105 52 116
73 67 52 116
76 105 52 78
67 103 61 61
```
Por el rango en el que se mueven las cifras pueden ser caracteres en ASCII (0-9/A-Z/a-z). Como dato curioso (e indiferente) que observo, al agrupar cada 4 cifras, la mayoría comienza por el valor 76.

Conversión de codificación ASCII a texto:
```
LS0tLi4gLS0tLS4gLi0uLSAtLS0tLiAtLi0uLS4gLS0tLS0gLS4uLSAuLS4uIC0uLS4tLiAtLS0uIC0tLS0tIC0uLS4tLiAtLS0tLSAtLi4tIC4tLi4NCg==
```
La cadena acaba con el símbolo '=', muy propio de la codificación Base64 (por cuestiones técnicas del propio algoritmo que no viene al caso explicar).

Conversión base64 a texto:

---.. ----. .-.- ----. -.-.-. ----- -..- .-.. -.-.-. ---. ----- -.-.-. ----- -..- .-..

Parece morse! Pero la conversión de morse a texto no da un resultado coherente en mi cabeza. Morse es un lenguaje de 2 símbolos..a ver si volteándolos sale algo.. Y efectivamente, el volteo queda:

...-- ....- -.-. ...-- .-.-.- ..... .--. -.-- .-.-.- ...- .... .-.-.- ..... .--. -.--

Y la conversión morse a texto nos da la flag:

34C3.5PY.VH.5PY
