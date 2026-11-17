<!--
  Práctica 3: Creación de un documento Markdown
  Proyecto Intermodular I - 1º ASIR
  Autor: Izan Pedron
  Esto es un comentario de Markdown: no se ve al renderizar el documento.
-->

# Cómo empezar a jugar en CachyOS

**Izan Pedron** — *1º ASIR*

CachyOS es una distribución de Linux basada en Arch y pensada para jugar.
Esta guía explica los pasos básicos para dejarla lista en una tarde.

Antes jugar en Linux era complicado.
Hoy ***ya casi no hay que configurar nada***, y esta guía lo demuestra.

## 1. Qué trae CachyOS ya preparado

Estas cosas vienen hechas de fábrica, así que no hay que tocarlas:

- El **kernel** ya optimizado para juegos.
- Las **librerías de 32 bits** que necesitan los juegos antiguos.
- Los **controladores de AMD e Intel** ya instalados.

Si tienes una gráfica **NVIDIA**, el controlador se instala desde la aplicación
*CachyOS Hello*, que se abre al arrancar el sistema.

## 2. Instalar los programas de juegos

En Arch, un *meta-paquete* es un paquete que no trae programas, solo una lista
de lo que hay que instalar. CachyOS tiene uno para juegos, y con un solo
comando lo deja todo listo:

```bash
sudo pacman -S --needed cachyos-gaming-meta cachyos-gaming-applications
```

![Terminal instalando los programas de juegos](img/01-instalar-juegos.png)

Con eso se instalan Steam, Wine, Heroic, MangoHud y GameMode.

## 3. Activar Proton en Steam

**Proton** es el programa de Valve que traduce las órdenes de Windows para que
un juego de Windows funcione en Linux. Steam lo trae incluido, pero hay que
activarlo a mano:

1. Abrir Steam e iniciar sesión.
2. Entrar en **Ajustes → Compatibilidad**.
3. Activar *Habilitar Steam Play para todos los títulos* y reiniciar Steam.

Desde ese momento, los juegos de la biblioteca se pueden instalar y jugar.

## 4. Ver los FPS mientras juegas

Steam permite escribir órdenes delante del juego en las **opciones de
lanzamiento** (clic derecho en el juego → *Propiedades*). La palabra
`%command%` representa el juego:

```bash
gamemoderun mangohud %command%
```

![Opciones de lanzamiento de Steam](img/02-opciones-lanzamiento.png)

`mangohud` muestra un panel con los FPS y la temperatura, y `gamemoderun`
pone la CPU en modo rendimiento mientras juegas.

![Juego con el panel de MangoHud](img/03-mangohud-en-juego.png)

## 5. Juegos que no son de Steam

**Heroic** es un programa que inicia sesión en Epic Games y GOG, descarga los
juegos y los ejecuta con Proton igual que Steam.

![Biblioteca de juegos en Heroic](img/04-heroic.png)

## 6. Saber si un juego funciona

Antes de instalar un juego conviene mirarlo en [ProtonDB](https://www.protondb.com/),
una web donde los usuarios cuentan si funciona y cómo. Usa medallas:

| Medalla | Qué significa | Qué hacer |
|---|---|---|
| Platino | Funciona perfecto | Instalar y jugar |
| Oro | Funciona con un ajuste | Copiar el ajuste que indican |
| Plata | Funciona con fallos pequeños | Se puede jugar igual |
| Borked | No funciona | Buscar otro juego |

### 6.1. Lo que no va a funcionar

Los juegos con *anticheat* que el fabricante no permite en Linux no arrancan,
como **Valorant**, **Fortnite** o **Call of Duty**. No es un fallo de CachyOS:
es una decisión de la empresa del juego.

<!-- Para separar párrafos se deja una línea en blanco; para cortar la línea
     dentro del mismo párrafo se dejan dos espacios al final, como aquí abajo. -->

Práctica de **Proyecto Intermodular I**.  
Curso 2026/2027 — 1º ASIR.
