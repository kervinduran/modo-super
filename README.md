# Modo Súper

**Modo Súper**: es una experiencia distinta porque tienes opciones para disfrutar según tus compras en
Súper Market Retail. Esto, nace del análisis de causa raíz de un caso académico
*Super Market Retail* (Maestría en Ciencia de Datos), como respuesta al
hallazgo de que la caída de ventas se explica por una caída de **frecuencia
de compra**, no por abandono de clientes, y de que cada categoría tiene una
ventana de consumo propia y verificable en los datos.

**Todo el prototipo vive en un único archivo: [`index.html`](./index.html).**
Sin build, sin dependencias, sin servidor: se abre con doble clic.

## La idea

Cada categoría desbloquea una experiencia distinta, pensada para el momento
real en que se consume:

| Modo | Categoría | Qué hace | Ventana real confirmada en los datos |
|---|---|---|---|
| 🍷 Modo Previa | Licores | Cartas con retos sociales para el grupo antes de salir | Viernes-sábado, 17:00-21:00 |
| 🥘 Modo Cocina | Canasta Básica | Recetas que estiran el presupuesto con lo que ya compraste | Sábado-domingo, mediodía |
| 🍿 Modo Noche | Snacks | Recomendación de película/serie para acompañar el snack | Ver nota de diseño abajo |
| ☕ Modo Antojo | Panadería | Con qué acompañar (café, té, etc.) | Todos los días, 20:00-23:00 |

Desde la pantalla principal, cada tarjeta lleva directo a su Modo.

## Por qué es un solo archivo

La primera versión de este prototipo tenía 10 archivos (5 páginas HTML +
CSS + JS + 4 JSON de contenido). Esta versión une todo en `index.html`:

- El **CSS** vive en un `<style>` al inicio.
- El **contenido de cada Modo** (antes en `data/*.json`) vive como objetos
  JavaScript en un `const DATA = {...}`.
- La **navegación** entre Modos es un router de una sola página basado en el
  *hash* de la URL (`#previa`, `#cocina`, `#noche`, `#antojo`), así que
  también se puede compartir un enlace directo a un Modo específico.

Ventaja práctica: como no depende de `fetch()` para cargar `.json` externos,
el archivo funciona abriéndolo directo desde el disco
(`file:///.../index.html`), sin necesidad de levantar un servidor local.

## Nota de diseño pendiente: Modo Noche

Los datos simulados del caso ubican el pico real de compra de **Snacks**
entre semana, en la pausa laboral (13:00-15:00) - no en la noche. "Modo
Noche" es la versión más atractiva de la idea, pero asume un segundo momento
de consumo que el estudio no midió. La alternativa fiel a los datos sería
**"Modo Break"**: contenido más corto (un video de 2 minutos, no una
película entera), pensado para la pausa del mediodía. El bloque a editar es
`DATA.noche` y la sección `#view-noche` dentro de `index.html`.

## Cómo probarlo 

Ábrelo directo, no requiere nada más:

```bash
open index.html        # macOS
xdg-open index.html    # Linux
start index.html       # Windows
```

## Qué sigue (si se convierte en algo real)

- **Identificación del cliente**: hoy el prototipo es de navegación libre;
  la causa raíz del análisis original exige poder reconocer al mismo
  cliente entre visitas (por ejemplo, al vincularlo a un número de
  WhatsApp o a una tarjeta de puntos) antes de personalizar cualquier Modo.
- **Registro de interacción**: qué Modo abre cada cliente es una señal de
  comportamiento nueva, más fina que la categoría comprada - se podría sumar
  al modelo de afinidad/RFM del análisis original.
- **Contenido dinámico real**: hoy el contenido es estático y de ejemplo; en
  producción saldría de una base editable (o incluso generado) y podría
  variar según el ticket real de compra.

---

*Prototipo académico - Maestría en Ciencia de Datos, curso Fundamentos de
Estrategia de Negocios para Ciencias de Datos. El contenido de cada Modo es
un ejemplo y no representa productos ni promociones reales de ninguna cadena
de supermercados existente.*
