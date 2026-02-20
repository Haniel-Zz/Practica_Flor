#  Generacion de Patron Circular en Blender mediante Python

<p align="center">
Automatizacion de la creacion de multiples circulos distribuidos en forma radial usando scripting en Blender
</p>


##  Introduccion

Blender permite generar geometria automaticamente mediante Python.

En esta practica se crea un **patron circular** compuesto por multiples circulos distribuidos alrededor de un punto central usando trigonometria.



##  Objetivo

* Crear patrones geometricos automaticamente
* Aplicar trigonometria en graficos 2D
* Utilizar ciclos para generar distribucion radial
* Automatizar la creacion de objetos en Blender



## Fundamento Teorico

Cada circulo se posiciona usando:

```
x = r * cos(angulo)
y = r * sin(angulo)
```

Esto permite distribuir los objetos uniformemente en 360°.

---

##  Requisitos

* Blender 5.0 o superior
* Espacio de trabajo **Scripting**



#  Procedimiento Paso a Paso


##  Paso 1: Limpiar la escena

![Image](https://docs.blender.org/manual/en/latest/_images/editors_3dview_startup-scene_labels.png)

![Image](https://i.sstatic.net/yiZ9P.png)

![Image](https://i.sstatic.net/bB9Wn.jpg)

![Image](https://i.sstatic.net/tH99S.jpg)

```python
bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()
```

---

##  Paso 2: Definir parametros

![Image](https://docs.blender.org/manual/en/latest/_images/render_freestyle_python_scripting-mode.png)

![Image](https://i.sstatic.net/6pVBt.jpg)

![Image](https://devtalk.blender.org/uploads/default/original/3X/f/9/f90567fed12d7fe362ee1d14ecde645bd02b633d.png)

![Image](https://d3a2gvihmbqfjo.cloudfront.net/bd/bd568dbb7e5b06404dffdb7fa5cccc25/bd568dbb7e5b06404dffdb7fa5cccc25.png)

```python
radio=3
angulo_actual=0
paso_angular=60
```



##  Paso 3: Crear circulo central

![Image](https://i.sstatic.net/k4Y9W.png)

![Image](https://docs.blender.org/manual/en/latest/_images/modeling_meshes_primitives_all.png)

![Image](https://blenderartists.org/uploads/default/original/4X/1/e/7/1e70096ed6f4ffaa587e59fc917322451cfe17e2.jpeg)

![Image](https://blenderartists.org/uploads/default/optimized/4X/6/b/c/6bcdd185d071f5cea252ef3645489f9aaf920f00_2_1024x610.png)

```python
bpy.ops.mesh.primitive_circle_add(radius=radio, location=(0,0,0), vertices=64)
```



##  Paso 4: Generar distribucion radial

![Image](https://blenderartists.org/uploads/default/4a55894caa06bc358ba209c03d30880f6837ad41)

![Image](https://i.sstatic.net/4XaaN.png)

![Image](https://i.sstatic.net/cHm50.png)

![Image](https://i.sstatic.net/6SUf9.png)

```python
while angulo_actual<360:
    x=radio*math.cos(math.radians(angulo_actual))
    y=radio*math.sin(math.radians(angulo_actual))
    bpy.ops.mesh.primitive_circle_add(radius=radio, location=(x, y, 0), vertices=64)
    angulo_actual += paso_angular
```



#  Codigo Completo

```python
import bpy
import math

bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()

radio=3
angulo_actual=0
paso_angular=60

bpy.ops.mesh.primitive_circle_add(radius=radio, location=(0,0,0), vertices=64)

while angulo_actual<360:
    x=radio*math.cos(math.radians(angulo_actual))
    y=radio*math.sin(math.radians(angulo_actual))
    bpy.ops.mesh.primitive_circle_add(radius=radio, location=(x, y, 0), vertices=64)
    angulo_actual += paso_angular
```



#  Resultado Final

![Image](https://public.blenderkit.com/thumbnails/assets/5b76a412a44f41c695a382a052b3d9d5/files/thumbnail_b5e5d9d0-2321-48ae-aef3-f7530792b23d.jpg.256x256_q85.jpg.webp?webp_generated=1766444420)

![Image](https://blenderartists.org/uploads/default/optimized/4X/8/a/0/8a09b708d54b004c1d6657ec49e6954018ad8426_2_1024x604.jpeg)

![Image](https://i.sstatic.net/k4Y9W.png)

![Image](https://blenderartists.org/uploads/default/b193f6d372a8a580e347ff3490869e238ff6f7d0)

El script genera:

 Un circulo central
 Seis circulos adicionales
 Distribucion uniforme cada 60°



#  Personalizacion

Cambiar separacion angular:

```python
paso_angular=45
```

Cambiar tamaño:

```python
radio=5
```

---

#  Ejemplos

| Paso Angular | Cantidad |
| ------------ | -------- |
| 60°          | 6        |
| 45°          | 8        |
| 30°          | 12       |

---

#  Conclusiones

Este script demuestra como Blender puede automatizar la creacion de patrones geometricos utilizando matematicas y programacion.

