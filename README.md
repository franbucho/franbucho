### Hi there 👋, My name is Fran
#### I am Developer specialized in automation, data management and visual integrations
I am of Venezuelan origin but I live in New York City, I am very interested in technology, dogs and 3D printing.

Skills: UiPath / Python / PowerBi / JS / HTML / CSS 

- 🔭 I’m currently working on PWC 
- 🌱 I’m currently learning IA Integration & Large Scale Project 
- 👯 I’m looking to collaborate on RPA AND CODE CHALLENGES 
- 🤔 I’m looking for help with Apache, Nginx Migration 
- 📫 How to reach me: franciscovillahermosa@gmail.com 
- 😄 Pronouns: DOG&PIZZA 
- ⚡ Fun fact: Pizza Profesional eater.. I have a doctorate in the movie Toy Story, founding member of Toy Story Latam Club
- [Personal Blog](https://techvilla.nicepage.io/?uid=83c16148-a0cf-4858-aeca-1f14ed5e44ad)
- [Twitter](https://twitter.com/franbucho)
- [LinkedIn](https://www.linkedin.com/in/fjvs-arg/)

![Banner](banner3.png)

import random
import time
import ascii_art

# Dimensiones del tablero
ancho = 20
alto = 10

# Posición inicial de la cabeza de la culebrita
cabeza_x = ancho // 2
cabeza_y = alto // 2

# Dirección inicial de la culebrita
direccion = "derecha"

# Lista de segmentos de la culebrita
segmentos = [(cabeza_x, cabeza_y)]

# Manzana
manzana_x = random.randint(0, ancho - 1)
manzana_y = random.randint(0, alto - 1)

# Bucle principal del juego
while True:

    # Borrar el tablero
    print("\033[2J")

    # Dibujar la culebrita
    for segmento in segmentos:
        print(ascii_art.pixel, end="")
        print(ascii_art.reset, end="")
    print()

    # Dibujar la manzana
    print(ascii_art.apple, end="")
    print(ascii_art.reset, end="")

    # Leer la entrada del usuario
    tecla = input()

    # Cambiar la dirección de la culebrita
    if tecla == "a":
        direccion = "izquierda"
    elif tecla == "d":
        direccion = "derecha"
    elif tecla == "w":
        direccion = "arriba"
    elif tecla == "s":
        direccion = "abajo"

    # Mover la cabeza de la culebrita
    if direccion == "izquierda":
        cabeza_x -= 1
    elif direccion == "derecha":
        cabeza_x += 1
    elif direccion == "arriba":
        cabeza_y -= 1
    elif direccion == "abajo":
        cabeza_y += 1

    # Si la cabeza de la culebrita choca con una pared, termina el juego
    if cabeza_x < 0 or cabeza_x >= ancho or cabeza_y < 0 or cabeza_y >= alto:
        break

    # Si la cabeza de la culebrita choca con un segmento de la culebrita, termina el juego
    if (cabeza_x, cabeza_y) in segmentos[1:]:
        break

    # Si la cabeza de la culebrita come la manzana, agregar un nuevo segmento
    if cabeza_x == manzana_x and cabeza_y == manzana_y:
        segmentos.append((cabeza_x, cabeza_y))
        manzana_x = random.randint(0, ancho - 1)
        manzana_y = random.randint(0, alto - 1)

    # Agregar la nueva posición de la cabeza a la lista de segmentos
    segmentos.insert(0, (cabeza_x, cabeza_y))

    # Eliminar el último segmento de la lista (si la culebrita no ha crecido)
    if len(segmentos) > 1:
        segmentos.pop()

    # Esperar un poco antes de continuar
    time.sleep(0.1)

# Mensaje de fin del juego
print("¡Fin del juego!")
print("Tu puntaje:", len(segmentos))

