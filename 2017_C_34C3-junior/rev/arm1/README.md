
**Título:** arm1 | **Categoría:** Reversing | **Nivel:** fácil

**Autor:** blondbyte

> **Enunciado:**
>
> Can you reverse engineer this code and get the flag?
>
> This code is ARM Thumb 2 code which runs on an STM32F103CBT6. You should not need such a controller to solve this challenge.
>
> There are 5 stages in total which share all the same code base, so you are able to compare code from the first stage with all the other stages to see what code is actually relevant.
>
> If you should need a datasheet, you can get it here (http://www.st.com/content/ccc/resource/technical/document/reference_manual/59/b9/ba/7f/11/af/43/d5/CD00171190.pdf/files/CD00171190.pdf/jcr:content/translations/en.CD00171190.pdf).
>
> In case you need to refresh your ARM assembly, check out Azeria's cool articles (https://azeria-labs.com/writing-arm-assembly-part-1/).
>
> [`arm_stage1.bin`](arm_stage1.bin)

---

#### Resolución
Cuidado que voy.. como no estés atento te la pierdes:
```
root@blondbyte# strings arm_stage1.bin
L"x2
x`9`
i!JC
pcS`

K[h
K[XCP
FpGThe flag is: 34C3_I_4dm1t_it_1_f0und_th!s_with_str1ngs
```
La flag es: `34C3_I_4dm1t_it_1_f0und_th!s_with_str1ngs`
