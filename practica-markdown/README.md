<!--
  Práctica 3: Creación de un documento Markdown
  Proyecto Intermodular I — 1º ASIR — Curso 2026/2027
  Autor: Izan Pedron
  Los comentarios como este no se ven al renderizar el documento.
-->

# Cómo empezar a jugar en CachyOS

**Izan Pedron** — *1º ASIR*

---

## 1. De qué va esta guía

**CachyOS** es una distribución de Linux basada en [Arch Linux](https://archlinux.org/)
y preparada para jugar. Esta guía explica los pasos básicos para dejarla lista.

> Antes, jugar en Linux era complicado.
> Hoy ***ya casi no hay que configurar nada***, y esta guía lo demuestra.

### 1.1. Lo que ya viene hecho

Estas cosas vienen de fábrica, así que no hay que tocarlas:

- El **kernel** ya optimizado para juegos.
- Las **librerías de 32 bits** que necesitan los juegos antiguos.
- Los **controladores de AMD e Intel** ya instalados.

Si la gráfica es **NVIDIA**, el controlador se instala desde la aplicación
*CachyOS Hello*, que se abre sola al arrancar el sistema.

---

## 2. Instalar los programas de juegos

En Arch, un *meta-paquete* es un paquete que no trae programas, solo una lista
de lo que hay que instalar. CachyOS tiene uno para juegos y con un solo comando
lo deja todo listo:

```bash
sudo pacman -S --needed cachyos-gaming-meta cachyos-gaming-applications
```

![Terminal instalando los programas de juegos](img/01-instalar-juegos.png)

Con eso se instalan **Steam**, **Wine**, **Heroic**, **MangoHud** y **GameMode**.

---

## 3. Activar Proton en Steam

**Proton** es el programa de Valve que traduce las órdenes de Windows para que
un juego de Windows funcione en Linux. Steam lo trae incluido, pero hay que
activarlo a mano:

1. Abrir Steam e iniciar sesión.
2. Entrar en **Ajustes → Compatibilidad**.
3. Activar *Habilitar Steam Play para todos los títulos*.
4. Reiniciar Steam.

Desde ese momento, los juegos de la biblioteca ya se pueden instalar y jugar.
Los juegos de **Epic Games** y **GOG** no están en Steam: para esos se usa
*Heroic*, que hace lo mismo pero con sus tiendas.

---

## 4. Ver los FPS mientras juegas

Steam permite escribir órdenes delante del juego en las **opciones de
lanzamiento** (clic derecho en el juego → *Propiedades*). La palabra
`%command%` representa el juego:

```bash
gamemoderun mangohud %command%
```

![Opciones de lanzamiento de Steam](img/02-opciones-lanzamiento.png)

Cada palabra hace una cosa:

- `mangohud` muestra un panel con los FPS y la temperatura.
- `gamemoderun` pone la CPU en modo rendimiento mientras juegas.

![Panel de MangoHud durante una partida](img/03-mangohud-en-juego.png)

---

## 5. Saber si un juego funciona

Antes de instalar un juego conviene mirarlo en [ProtonDB](https://www.protondb.com/),
una web donde los usuarios cuentan si funciona y cómo. Usa medallas:

| Medalla | Qué significa | Qué hacer |
|---|---|---|
| Platino | Funciona perfecto | Instalar y jugar |
| Oro | Funciona con un ajuste | Copiar el ajuste que indican |
| Plata | Funciona con fallos pequeños | Se puede jugar igual |
| Borked | No funciona | Buscar otro juego |

### 5.1. Lo que no va a funcionar

Los juegos con *anticheat* que el fabricante no permite en Linux no arrancan,
como **Valorant**, **Fortnite** o **Call of Duty**. No es un fallo de CachyOS:
es una decisión de la empresa del juego, así que no hay ajuste que lo arregle.

<!-- Entre párrafos se deja una línea en blanco. Para cortar la línea dentro
     del mismo párrafo se dejan dos espacios al final, como en el pie. -->

---

Práctica 3 — *Creación de un documento Markdown*.  
Proyecto Intermodular I — 1º ASIR — Curso 2026/2027.
