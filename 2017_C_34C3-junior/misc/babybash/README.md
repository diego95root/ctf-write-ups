
**Título:** babybash | **Categoría:** Miscelanea | **Nivel:** fácil

**Autor:** vlo y blondbyte

> **Enunciado:**
>
> If you're a baby and know bash, try this:
> nc 35.189.118.225 1337

---

#### Resolución
Establezco conexión con el socket del servidor y me aparece un puntero a modo de shell:
```
root@blondbyte# nc 35.189.118.225 1337
baby>
```
Escribo `help` y me muestra un mensaje de bienvenida:
```
baby> help

    Welcome to babaybash!

    This is a challenge where you find yourself in a bash-jail.

    You want to execute /get_flag to get the flag!

    But the following characters are banned:
        - a-z
        - *
        - ?
        - .

    Good luck!

baby>
```
Pruebo a escribir `/get_flag` y no me deja:
```
baby> /get_flag
Invalid character. Try 'help'.
baby>
```
Parece ser que necesito codificar los caracteres para que la shell los decodifique como `/get_flag`. Tras varias pruebas y búsquedas, codifico en octal con alguna tool online y le paso el resultado:
```
baby> /$'\147\145\164_\146\154\141\147'
Usage: /get_flag gimme_FLAG_please
baby>
```
Me indica la forma de utilizar el comando, osea que pruebo a pasarselo tal cual:

```
baby> /$'\147\145\164_\146\154\141\147' gimme_FLAG_please
Invalid character. Try 'help'.
baby>
```
Al parecer sigo bajo las condiciones iniciales. Codifico en octal el texto `gimme_FLAG_please` a ver que pasa:
```
baby> /$'\147\145\164_\146\154\141\147' $'\147\151\155\155\145_FLAG_\160\154\145\141\163\145'
Good job!

Here's your flag: 34C3_LoOks_lik3_y0U_are_nO_b4by_4ft3r_4ll
```
Premio, la flag es: `34C3_LoOks_lik3_y0U_are_nO_b4by_4ft3r_4ll`
