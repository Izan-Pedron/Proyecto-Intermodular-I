<!--
  Práctica 3: Creación de un documento Markdown
  Módulo: Proyecto Intermodular I - 1º ASIR
  IES Dr. Lluís Simarro La Cabra (Xàtiva)
  Autor: Izan Pedron
  REQUISITO 4 DEL ENUNCIADO: este bloque es un comentario en Markdown.
  No se muestra al renderizar el documento, solo es visible en el código fuente.
-->

# Cómo empezar a jugar en CachyOS

![Portada: escritorio de CachyOS con un juego en marcha](img/00-portada.png)

**Izan Pedron**
*1º ASIR — IES Dr. Lluís Simarro La Cabra (Xàtiva)*

---

Durante años, "jugar en Linux" fue sinónimo de pelearse con configuraciones.
Hoy ya no: una distribución como **CachyOS** deja casi todo listo de fábrica.
Esta guía recorre, paso a paso, lo que hay que hacer en una instalación recién
estrenada para poder jugar el mismo día.

El objetivo no es ser exhaustivo, sino ***que funcione a la primera*** y
entender *por qué* funciona cada pieza, que es lo que de verdad ahorra tiempo
cuando algo se rompe.

## Índice

<!-- REQUISITO 5 (enlaces): estos son enlaces internos, apuntan a los encabezados del propio documento -->

1. [Antes de empezar](#1-antes-de-empezar)
2. [Instalar los controladores gráficos](#2-instalar-los-controladores-gráficos)
3. [El meta-paquete de juegos de CachyOS](#3-el-meta-paquete-de-juegos-de-cachyos)
4. [Steam y Proton](#4-steam-y-proton)
5. [Juegos de Epic y GOG con Heroic](#5-juegos-de-epic-y-gog-con-heroic)
6. [Comprobar la compatibilidad en ProtonDB](#6-comprobar-la-compatibilidad-en-protondb)
7. [Ajustes finos: MangoHud y GameMode](#7-ajustes-finos-mangohud-y-gamemode)
8. [Lo que no va a funcionar](#8-lo-que-no-va-a-funcionar)
9. [Chuleta de comandos](#9-chuleta-de-comandos)

---

## 1. Antes de empezar

CachyOS está basada en **Arch Linux**, así que hereda dos cosas importantes: el
repositorio es *rolling release* (siempre la última versión) y el sistema
asume que tú decides qué se instala.

Lo primero, siempre, es actualizar el sistema completo:

```bash
sudo pacman -Syu
```

### 1.1. Qué trae CachyOS ya hecho

Esto es lo que **no** hay que configurar, al contrario de lo que piden muchas
guías antiguas:

<!-- REQUISITO 3 (listas): esta es la lista NO ordenada, con guiones -->

- El **kernel optimizado** (`linux-cachyos`), ya compilado con el planificador
  BORE y ajustes pensados para baja latencia.
- El repositorio **multilib** activado, necesario para las librerías de 32 bits
  que aún usan muchos juegos.
- **Mesa** actualizado, el controlador libre que usan las gráficas AMD e Intel.
- La aplicación **CachyOS Hello**, el panel de bienvenida desde el que se
  instalan controladores y se cambian ajustes del sistema.

![Ventana de CachyOS Hello recién abierta](img/01-cachyos-hello.png)

---

## 2. Instalar los controladores gráficos

Aquí la respuesta depende de la gráfica:

<!-- REQUISITO 7 (tablas): tabla de 3 columnas x 4 filas de datos -->

| Gráfica | Controlador | ¿Hay que instalar algo? |
|---|---|---|
| AMD | Mesa (RADV) | No, viene incluido y es el recomendado |
| Intel | Mesa (ANV) | No, viene incluido |
| NVIDIA | `nvidia-open-dkms` | Sí, desde CachyOS Hello |
| Híbrida (portátil) | Mesa + NVIDIA | Sí, además hay que elegir qué GPU usa cada juego |

Para comprobar que la gráfica responde a **Vulkan**, que es la API que usan hoy
tanto los juegos nativos como Proton:

```bash
vulkaninfo --summary | grep deviceName
```

Si ese comando devuelve el nombre de tu tarjeta, el controlador está bien
instalado. Si no devuelve nada, no sigas: ningún juego arrancará.

![Salida del comando comprobando la GPU](img/02-controladores-gpu.png)

---

## 3. El meta-paquete de juegos de CachyOS

Un **meta-paquete** es un paquete que no contiene programas, solo una lista de
dependencias. Instalarlo arrastra todo lo demás de golpe, y es la gran ventaja
de CachyOS frente a montarlo a mano.

```bash
sudo pacman -S --needed cachyos-gaming-meta cachyos-gaming-applications
```

<!-- REQUISITO 3 (listas): esta es la lista ORDENADA, con números -->

Qué entra con esos dos paquetes:

1. **Steam**, con todas las librerías de 32 bits que necesita.
2. **Wine** en la versión de CachyOS, más las librerías de compatibilidad.
3. **Lutris** y **Heroic**, lanzadores para juegos de fuera de Steam.
4. **MangoHud**, el panel de rendimiento que se superpone al juego.
5. **GameMode**, que ajusta el gobernador de CPU mientras juegas.
6. **ProtonUp-Qt**, para instalar versiones de Proton que no están en Steam.

> El modificador `--needed` evita reinstalar lo que ya tengas. Es una costumbre
> sana en Arch: acelera la instalación y no toca paquetes que funcionan.

![Terminal instalando el meta-paquete de juegos](img/03-instalar-gaming-meta.png)

---

## 4. Steam y Proton

**Proton** es la capa de compatibilidad que Valve mantiene sobre Wine: traduce
las llamadas de Windows (y de DirectX a Vulkan) para que un juego pensado para
Windows se ejecute en Linux sin modificarlo.

Al abrir Steam por primera vez, inicia sesión y espera a que termine de
actualizarse.

![Steam abierto por primera vez](img/04-steam-primera-vez.png)

### 4.1. Activar Steam Play para todos los juegos

Por defecto, Steam solo usa Proton con los juegos que Valve ha verificado. Para
poder probar el resto hay que activarlo manualmente en
**Ajustes → Compatibilidad → Habilitar Steam Play para todos los títulos**.

![Ajustes de compatibilidad de Steam con Steam Play activado](img/05-activar-steam-play.png)

Tras cambiar esa opción Steam pide reiniciarse. A partir de ahí, cualquier juego
de la biblioteca se puede instalar y lanzar.

---

## 5. Juegos de Epic y GOG con Heroic

Steam no es la única tienda. **Heroic Games Launcher** es un lanzador libre que
inicia sesión en *Epic Games Store*, *GOG* y *Amazon Games*, descarga los juegos
y los ejecuta con Proton, igual que haría Steam.

Es, además, la forma más cómoda de reclamar los juegos gratuitos semanales de
Epic sin tener Windows.

![Biblioteca de juegos en Heroic](img/08-heroic-biblioteca.png)

---

## 6. Comprobar la compatibilidad en ProtonDB

Antes de comprar o instalar un juego grande, la consulta obligada es
[ProtonDB](https://www.protondb.com/), una base de datos donde los usuarios
reportan si un juego funciona y con qué ajustes.

<!-- REQUISITO 5 (enlaces): el enlace externo a ProtonDB está justo arriba -->

Usa un sistema de medallas:

| Medalla | Qué significa | Qué esperar |
|---|---|---|
| Platino | Funciona perfecto sin tocar nada | Instalar y jugar |
| Oro | Funciona perfecto con algún ajuste | Copiar el ajuste del comentario mejor valorado |
| Plata | Funciona con fallos menores | Jugable, pero con algún detalle gráfico o de audio |
| Bronce / Borked | Falla o no arranca | Mejor buscar alternativa |

![Ficha de un juego en ProtonDB](img/09-protondb-ficha.png)

### 6.1. Instalar Proton-GE

Cuando ProtonDB recomienda **Proton-GE** (una versión de la comunidad con
parches que Valve aún no ha incorporado), se instala con **ProtonUp-Qt**: abrir
el programa, elegir Steam, pulsar *Añadir versión* y seleccionar la última
`GE-Proton`. Después aparece en la lista de Proton de cada juego.

![ProtonUp-Qt instalando Proton-GE](img/10-protonup-qt.png)

---

## 7. Ajustes finos: MangoHud y GameMode

Las **opciones de lanzamiento** de Steam permiten colar comandos delante del
juego. Se abren con clic derecho sobre el juego → *Propiedades* → *General*.

La variable `%command%` representa el ejecutable del juego, así que lo que se
escriba a su izquierda se ejecuta *antes* y envuelve al juego:

```bash
# Panel de rendimiento (FPS, temperaturas, uso de CPU/GPU)
mangohud %command%

# Prioridad de CPU y gobernador en modo rendimiento
gamemoderun %command%

# Las dos cosas a la vez, que es lo habitual
gamemoderun mangohud %command%
```

![Ventana de opciones de lanzamiento de Steam](img/06-opciones-lanzamiento.png)

Con eso, al entrar al juego aparece el panel de MangoHud en una esquina.
Sirve para saber si una caída de FPS viene de la GPU, de la CPU o de la memoria,
en lugar de adivinarlo.

![Juego en marcha con el panel de MangoHud visible](img/07-juego-con-mangohud.png)

---

## 8. Lo que no va a funcionar

Conviene saberlo antes de perder una tarde:

- Los juegos con **anticheat a nivel de kernel** que el desarrollador no ha
  habilitado para Linux. *Valorant*, *Fortnite*, *Call of Duty* o *Apex Legends*
  no arrancan, y no es un fallo de la distribución: es una decisión del
  fabricante del juego.
- Algunos juegos con **DRM muy intrusivo** (Denuvo en ciertas versiones).
- Programas de *overlay* propios de Windows, como el panel de NVIDIA o algunos
  grabadores de pantalla.

### 8.1. Consejos de guías antiguas que ya no aplican

Esto es importante porque medio internet sigue repitiéndolo:

| Consejo antiguo | Situación en 2026 |
|---|---|
| Instalar **PlayOnLinux** | Abandonado; se usan Lutris, Heroic o Bottles |
| Usar el instalador `.run` de NVIDIA | Rompe el sistema en Arch; se instala por `pacman` |
| Compilar un kernel *gaming* a mano | El kernel de CachyOS ya viene optimizado |
| Activar manualmente **multilib** | Ya está activado en CachyOS |

---

## 9. Chuleta de comandos

```bash
sudo pacman -Syu                        # Actualizar todo el sistema
vulkaninfo --summary | grep deviceName  # Comprobar que la GPU responde a Vulkan
mangohud glxgears                       # Probar el panel sin abrir un juego
gamemoded -s                            # Ver si GameMode está activo
protontricks --gui                      # Toquetear el prefijo de un juego concreto
```

---

## Conclusión

Instalar los controladores, lanzar el meta-paquete de juegos y activar Steam
Play cubre el 90 % de los casos. El resto —Proton-GE, MangoHud, GameMode— son
mejoras que se añaden cuando un juego concreto lo pide, no requisitos previos.

La diferencia real de los últimos años no es que Linux se haya vuelto más
complicado, sino que **ya casi nunca hay que tocar nada**.

<!--
  REQUISITO 9 (párrafos y saltos de línea):
  los párrafos se separan dejando una línea en blanco entre ellos.
  Para forzar un salto de línea DENTRO del mismo párrafo se dejan
  dos espacios al final de la línea, como en el bloque de abajo.
-->

Documento realizado para la asignatura **Proyecto Intermodular I**.  
Curso 2026/2027 — 1º ASIR.  
IES Dr. Lluís Simarro La Cabra, Xàtiva.
