# Dino Runner en MakeCode Arcade (Python)

Este proyecto recrea el famoso juego del dinosaurio que aparece en Google Chrome cuando no hay conexión a Internet. Está desarrollado con [MakeCode Arcade](https://arcade.makecode.com/) usando **Python** y es ideal como proyecto educativo paso a paso para iniciarse en el desarrollo de videojuegos 2D.

---

## 🎓 Nivel educativo sugerido

- Estudiantes de secundaria o ciclos formativos.
- Recomendado para 3º o 4º ESO en clases de programación o TIC.

---

## 🚀 Objetivo del juego

Controlas a un dinosaurio que debe esquivar cactus (enemigos terrestres) y aviones (enemigos aéreos) saltando sobre ellos. A medida que tu puntuación aumenta, también lo hace la dificultad.

---

## ⚖️ Herramientas necesarias

- Navegador web
- [MakeCode Arcade Editor](https://arcade.makecode.com/)
- Modo Python activado

---

## ✍️ Tutorial paso a paso

### 1. Fondo y tilemap

1. Crea un nuevo proyecto en MakeCode Arcade y selecciona "Python".
2. Dibuja un **tilemap** con un suelo en la **fila 14**.
3. Usa un color de fondo que contraste.

```python
scene.set_background_color(9)
tiles.set_tilemap(tilemap("nivel"))
```

---

### 2. Crear y colocar el personaje (TRex)

1. Dibuja una secuencia de sprites llamada `kaijuMomWalk0` a `kaijuMomWalk5`.
2. Crea el sprite y añade gravedad.
3. Coloca el sprite sobre el suelo en la fila 14.

```python
TRex = sprites.create(assets.image("kaijuMomWalk0"), SpriteKind.player)
TRex.ay = 600
tiles.place_on_tile(TRex, tiles.get_tile_location(1, 14))
ground_y = TRex.bottom
```

---

### 3. Añadir animación de caminar

Utiliza `animation.run_image_animation` para reproducir la secuencia de sprites:

```python
animation.run_image_animation(
    TRex,
    [assets.image("kaijuMomWalk0"),
     assets.image("kaijuMomWalk1"),
     assets.image("kaijuMomWalk2"),
     assets.image("kaijuMomWalk3"),
     assets.image("kaijuMomWalk4"),
     assets.image("kaijuMomWalk5")],
    100,
    True
)
```

---

### 4. Salto con la tecla A

El personaje sólo puede saltar si está tocando el suelo:

```python
def on_a_pressed():
    if TRex.is_hitting_tile(CollisionDirection.BOTTOM):
        TRex.vy = -160
controller.A.on_event(ControllerButtonEvent.PRESSED, on_a_pressed)
```

---

### 5. Enemigos: cactus y aviones

Crea enemigos que se generen a intervalos y aumenten la dificultad:

```python
def spawn_enemy():
    global projectile, spawn_interval

    score = info.score()
    spawn_interval = max(1500 - score * 50, 500)

    if randint(0, 4) == 2:
        projectile = sprites.create_projectile_from_side(assets.image("plane0"), -100 - score * 2, 0)
        projectile.y = ground_y - 40
    else:
        projectile = sprites.create_projectile_from_side(assets.image("carRedLeft"), -120 - score * 2, 0)
        projectile.bottom = ground_y

    projectile.set_flag(SpriteFlag.AUTO_DESTROY, True)
    pause(spawn_interval)
    spawn_enemy()

spawn_enemy()
```

---

### 6. Colisiones y puntuación

- Cada vez que un enemigo se destruye solo, ganas puntos.
- Si chocas con uno, pierdes una vida.
- Si te quedas sin vidas, se acaba el juego.

```python
def on_on_destroyed(sprite2):
    info.change_score_by(1)
sprites.on_destroyed(SpriteKind.projectile, on_on_destroyed)

def on_on_overlap(sprite, otherSprite):
    info.change_life_by(-1)
    otherSprite.destroy()
    if info.life() <= 0:
        game.over(False)
sprites.on_overlap(SpriteKind.player, SpriteKind.projectile, on_on_overlap)
```

---

## 🌟 Ideas para expandir

- Añadir sonido (`music.play_sound()`).
- Guardar puntuación máxima (`info.high_score()`).
- Añadir nuevos tipos de enemigos con diferentes comportamientos.
- Incluir mejoras visuales con `effects`.

---

## 📄 Código completo

```python
scene.set_background_color(9)

projectile: Sprite = None
TRex: Sprite = None
ground_y = 0
spawn_interval = 1500  # milisegundos iniciales

# Crear el TRex
TRex = sprites.create(assets.image("kaijuMomWalk0"), SpriteKind.player)
TRex.ay = 600  # gravedad fuerte para que el salto sea más corto

# Animación de caminar
animation.run_image_animation(
    TRex,
    [assets.image("kaijuMomWalk0"),
     assets.image("kaijuMomWalk1"),
     assets.image("kaijuMomWalk2"),
     assets.image("kaijuMomWalk3"),
     assets.image("kaijuMomWalk4"),
     assets.image("kaijuMomWalk5")],
    100,
    True
)

# Tilemap y colocación
tiles.set_tilemap(tilemap("nivel"))
tiles.place_on_tile(TRex, tiles.get_tile_location(1, 14))
ground_y = TRex.bottom
scene.center_camera_at(TRex.x + 40, TRex.y)  # cámara fija

# Vida y puntuación
info.set_life(3)
info.set_score(0)

# Aumentar score cuando se destruye un enemigo
def on_on_destroyed(sprite2):
    info.change_score_by(1)
sprites.on_destroyed(SpriteKind.projectile, on_on_destroyed)

# Salto del TRex (más corto y rápido)
def on_a_pressed():
    if TRex.is_hitting_tile(CollisionDirection.BOTTOM):
        TRex.vy = -160
controller.A.on_event(ControllerButtonEvent.PRESSED, on_a_pressed)

# Colisión: pierdes una vida
def on_on_overlap(sprite, otherSprite):
    info.change_life_by(-1)
    otherSprite.destroy()
    if info.life() <= 0:
        game.over(False)
sprites.on_overlap(SpriteKind.player, SpriteKind.projectile, on_on_overlap)

# Generar enemigos (más rápidos y frecuentes al subir el score)
def spawn_enemy():
    global projectile, spawn_interval

    score = info.score()
    spawn_interval = max(1500 - score * 50, 500)

    if randint(0, 4) == 2:
        # Enemigo aéreo
        projectile = sprites.create_projectile_from_side(assets.image("plane0"), -100 - score * 2, 0)
        projectile.y = ground_y - 40
    else:
        # Cactus terrestre
        projectile = sprites.create_projectile_from_side(assets.image("carRedLeft"), -120 - score * 2, 0)
        projectile.bottom = ground_y

    projectile.set_flag(SpriteFlag.AUTO_DESTROY, True)

    # Siguiente aparición tras intervalo ajustado
    pause(spawn_interval)
    spawn_enemy()

# Iniciar generación de enemigos
spawn_enemy()
```
