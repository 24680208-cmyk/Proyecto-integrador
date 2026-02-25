# Proyecto-integrador

# PROYECTO INTEGRADOR – UNIDAD 1
## Generación Procedural de Escenario con Animación de Cámara en Blender

---

# 📌 1. Introducción

El presente proyecto integrador tiene como finalidad aplicar los conocimientos adquiridos en la Unidad 1 sobre generación procedural, programación estructurada y automatización de entornos digitales.

Se desarrolló un escenario tridimensional dentro de Blender utilizando Python y la API `bpy`. El escenario consiste en un puente curvo generado completamente mediante código, sin modelado manual.

Como mejora adicional a la tarea base “Escenario Procedural”, se implementó una animación automática de cámara que recorre el camino generado, simulando un desplazamiento dinámico dentro del entorno virtual.

El proyecto demuestra cómo la programación permite controlar completamente una escena 3D: creación de objetos, materiales, iluminación y animación.

---

# 🎯 2. Objetivo General

Desarrollar un entorno tridimensional generado de forma procedural en Blender mediante programación en Python, integrando animación automatizada de cámara.

---

# 🎯 3. Objetivos Específicos

- Aplicar funciones matemáticas para generar trayectorias curvas.
- Automatizar la creación de geometría tridimensional.
- Implementar materiales dinámicos desde código.
- Controlar transformaciones espaciales (posición, rotación y escala).
- Generar animación mediante inserción de keyframes.
- Organizar el código en funciones reutilizables.

---

# 🧠 4. Fundamentación Teórica

---

## 🔹 4.1 Generación Procedural

La generación procedural consiste en crear contenido automáticamente mediante algoritmos matemáticos en lugar de diseñarlo manualmente.

En este proyecto se utilizan funciones trigonométricas para calcular posiciones sobre una trayectoria curva:

x = cos(ángulo) × radio  
y = sin(ángulo) × radio  

Estas fórmulas permiten posicionar objetos sobre una circunferencia, generando una curva suave y controlada.

Cada sección del puente se construye tomando como base estas coordenadas calculadas automáticamente.

---

## 🔹 4.2 Transformaciones en Blender

Todo objeto en Blender puede ser manipulado mediante tres transformaciones principales:

- **Location (Traslación)** → Define la posición en el espacio.
- **Rotation (Rotación)** → Orienta el objeto.
- **Scale (Escala)** → Modifica el tamaño.

En este proyecto:

- La posición se calcula con funciones trigonométricas.
- La rotación se ajusta según el ángulo de la curva.
- La escala se utiliza para dar forma al suelo y paredes.

---

## 🔹 4.3 Animación por Keyframes

La animación en Blender funciona mediante keyframes.

Un keyframe guarda el estado de un objeto en un frame específico.

En este proyecto se insertan keyframes para:

- Ubicación de la cámara
- Rotación de la cámara

Cada 10 frames se guarda una nueva posición, generando movimiento continuo.

---

# 🏗️ 5. Desarrollo del Proyecto

El proyecto está organizado en tres funciones principales:

---

# 🔹 5.1 Función crear_material()

Esta función permite crear materiales personalizados dinámicamente.

### ¿Qué hace?

1. Crea un nuevo material.
2. Asigna un color RGB.
3. Retorna el material para usarlo en otros objetos.

Esto permite reutilizar materiales sin repetir código.

---

# 🔹 5.2 Función generar_puente()

Es la función principal del proyecto.

### Paso 1: Limpieza de escena

Se eliminan todos los objetos existentes para comenzar desde cero.

---

### Paso 2: Creación de materiales

Se crean cuatro materiales:

- Pared oscura
- Pared con detalle alternado
- Suelo claro
- Soporte gris

---

### Paso 3: Definición de parámetros

Se definen variables que controlan la forma del puente:

- largo_pasillo → Número de segmentos
- radio_curva → Radio de la trayectoria
- ancho_pasillo → Anchura del puente
- altura_puente → Elevación del puente

Modificar estos valores cambia completamente el diseño.

---

### Paso 4: Generación mediante bucle

Se utiliza un ciclo `for` que recorre cada segmento del puente.

En cada iteración:

1. Se calcula el ángulo.
2. Se calcula la posición usando coseno y seno.
3. Se crea el suelo.
4. Se crean paredes laterales.
5. Se crea un soporte cilíndrico.
6. Se guarda la posición para animación.

Cada segmento está alineado con la curva gracias a la rotación calculada.

---

# 🔹 5.3 Función crear_animacion()

Esta función genera la animación automática.

### Procedimiento:

1. Define el frame inicial y final.
2. Crea una nueva cámara.
3. Recorre la lista de posiciones guardadas.
4. Inserta keyframes cada 10 frames.
5. Mantiene una inclinación constante de 75°.

Duración total:

frames = largo_pasillo × 10

Esto genera un recorrido progresivo a lo largo del puente.

---

# 💡 6. Funcionamiento General

Al ejecutar el script:

1. Se limpia la escena.
2. Se generan materiales.
3. Se construye el puente curvo.
4. Se agregan soportes.
5. Se inserta iluminación.
6. Se crea una cámara.
7. Se genera la animación automáticamente.

Todo el entorno se produce únicamente con código.

---

# 📸 7. Evidencia Visual



---

# 🎥 8. Video del Proyecto

Puedes colocar tu video de dos formas:


---
# 📊 9. Conclusión

Este proyecto demuestra que la programación permite automatizar la creación de entornos tridimensionales complejos.

La generación procedural reduce el trabajo manual y permite modificar el diseño simplemente cambiando parámetros.

La integración de animación agrega dinamismo y demuestra el control completo de la escena mediante scripting.

Se logra:

✔ Automatización total  
✔ Uso de matemáticas aplicadas  
✔ Organización modular  
✔ Animación funcional  
✔ Entorno 3D generado por código  

---

# 💻 10. Código Completo

```python
import bpy
import math

def crear_material(nombre, color_rgb):
    mat = bpy.data.materials.new(name=nombre)
    mat.diffuse_color = (*color_rgb, 1.0)
    return mat

def generar_puente():

    bpy.ops.object.select_all(action='SELECT')
    bpy.ops.object.delete()

    mat_pared_a = crear_material("ParedOscura", (0.1, 0.1, 0.1))
    mat_pared_b = crear_material("ParedDetalle", (0.8, 0.2, 0.0))
    mat_suelo = crear_material("Suelo", (0.8, 0.8, 0.8))
    mat_soporte = crear_material("Soporte", (0.2, 0.2, 0.2))

    largo_pasillo = 20
    radio_curva = 20
    ancho_pasillo = 4
    altura_puente = 3

    posiciones = []

    for i in range(largo_pasillo):

        angulo = i * 0.12

        x_centro = math.cos(angulo) * radio_curva
        y_centro = math.sin(angulo) * radio_curva

        rotacion = angulo

        posiciones.append((x_centro, y_centro, altura_puente + 2))

        bpy.ops.mesh.primitive_cube_add(size=2,
            location=(x_centro, y_centro, altura_puente))
        suelo = bpy.context.active_object
        suelo.scale.x = ancho_pasillo
        suelo.scale.y = 1
        suelo.scale.z = 0.2
        suelo.rotation_euler[2] = rotacion
        suelo.data.materials.append(mat_suelo)

        bpy.ops.mesh.primitive_cube_add(size=2,
            location=(x_centro - math.cos(angulo)*ancho_pasillo,
                      y_centro - math.sin(angulo)*ancho_pasillo,
                      altura_puente + 1))
        pared_izq = bpy.context.active_object
        pared_izq.rotation_euler[2] = rotacion

        if i % 2 == 0:
            pared_izq.data.materials.append(mat_pared_a)
        else:
            pared_izq.data.materials.append(mat_pared_b)
            pared_izq.scale.z = 1.5

        bpy.ops.mesh.primitive_cube_add(size=2,
            location=(x_centro + math.cos(angulo)*ancho_pasillo,
                      y_centro + math.sin(angulo)*ancho_pasillo,
                      altura_puente + 1))
        pared_der = bpy.context.active_object
        pared_der.rotation_euler[2] = rotacion
        pared_der.data.materials.append(mat_pared_a)

        bpy.ops.mesh.primitive_cylinder_add(radius=0.3,
            depth=altura_puente,
            location=(x_centro, y_centro, altura_puente/2))
        soporte = bpy.context.active_object
        soporte.data.materials.append(mat_soporte)

    bpy.ops.object.light_add(type='POINT', location=(0, 0, 15))
    luz = bpy.context.active_object
    luz.data.energy = 1500

    crear_animacion(posiciones)

def crear_animacion(posiciones):

    scene = bpy.context.scene
    scene.frame_start = 1
    scene.frame_end = len(posiciones) * 10

    cam_data = bpy.data.cameras.new("Camara")
    cam = bpy.data.objects.new("Camara", cam_data)
    bpy.context.collection.objects.link(cam)
    scene.camera = cam

    frame = 1

    for pos in posiciones:
        cam.location = pos
        cam.rotation_euler = (math.radians(75), 0, math.radians(45))
        cam.keyframe_insert(data_path="location", frame=frame)
        cam.keyframe_insert(data_path="rotation_euler", frame=frame)
        frame += 10

generar_puente()
