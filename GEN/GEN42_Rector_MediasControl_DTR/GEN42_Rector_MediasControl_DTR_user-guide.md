# [GEN42 Rector] Control SMAs: 6/70/200 (Trullas) · Guía operativa

Cómo se añade y se ajusta. Qué dice la fuente y cómo se lee, en la guía técnica.

| Campo | Valor |
|---|---|
| Título en TradingView | `[GEN42 Rector] Control SMAs: 6/70/200 (Trullas)` |
| Nombre corto | `GEN42 Control SMAs` |
| Script | Versión 0.1.0.0 (ver control de cambios) |

---

## Cómo se añade

1. Abre el gráfico del activo, en el marco con el que operes.
2. En Indicadores, busca el título o el nombre corto y añádelo.
3. Se dibuja sobre el precio, no en un panel aparte.

## Ajustes

Tres grupos: «Cálculo», «Aspecto» e «Info». Los tres ajustes de período llevan una explicación al pasar el ratón (tooltip).

| Ajuste | Por defecto | Qué hace | Cuándo tocarlo |
|---|---|---|---|
| Fuente | close (cierre) | Precio con el que se calculan las tres medias | Para calcularlas con un precio distinto del cierre |
| Media rápida (velas) | 6 | Velas de la media rápida (de 1 a 1000) | `[Aportado]`: 6 es el período de Trullás. Cambiarlo da otra media, no la suya |
| Media intermedia (velas) | 70 | Velas de la media intermedia (de 1 a 1000) | `[Aportado]`: 70 es el período de Trullás |
| Media lenta (velas) | 200 | Velas de la media lenta (de 1 a 1000) | `[Aportado]`: 200 es el período de Trullás |
| Rápida: color / grosor | #2962FF (azul) y grosor 1 | Color y grosor de la línea de la media rápida (grosor de 1 a 4) | A gusto: solo cambia el dibujo |
| Intermedia: color / grosor | #FF9800 (naranja) y grosor 1 | Color y grosor de la línea de la media intermedia (grosor de 1 a 4) | A gusto: solo cambia el dibujo |
| Lenta: color / grosor | #F23645 (rojo) y grosor 1 | Color y grosor de la línea de la media lenta (grosor de 1 a 4) | A gusto: solo cambia el dibujo |

El grupo «Info» trae un resumen de solo lectura, que no se puede cambiar.

## Equivalencia en tiempo

Son velas, no días. Con 5 sesiones por semana:

| Ajuste | Valor | En diario | En semanal |
|---|---|---|---|
| Media rápida (velas) | 6 | 6 sesiones, algo más de 1 semana | 6 semanas |
| Media intermedia (velas) | 70 | 70 sesiones, 14 semanas | 70 semanas, algo más de 1 año |
| Media lenta (velas) | 200 | 200 sesiones, 40 semanas | 200 semanas, unos 3,8 años |

Una media de N velas no tiene valor hasta que hay N velas cargadas: con menos, esa línea no se dibuja.

## Colores y marcas

| Elemento | Color o forma | Qué indica |
|---|---|---|
| SMA rápida | Línea azul, grosor 1 | Media simple de 6 velas |
| SMA intermedia | Línea naranja, grosor 1 | Media simple de 70 velas |
| SMA lenta | Línea roja, grosor 1 | Media simple de 200 velas |

Los colores y el grosor se cambian en el grupo «Aspecto». No hay más marcas.

## Alertas

Este script no define alertas.

## Marcos temporales

El del gráfico: el script no fuerza ninguno y las tres medias cuentan velas del marco en que se carga (ver «Equivalencia en tiempo»). El código original de Trullás no indica un marco.

---

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-14 | Creación |
| 0.2.0.0 | 2026-11-14 | Renombrada a GEN42; sin el «Qué es», que va en la guía técnica |
| 0.3.0.0 | 2026-11-14 | Ajustes del script 0.1.0.0: fuente, períodos, color y grosor |
| 0.3.1.0 | 2026-11-15 | Añadidos el rango de períodos (1 a 1000), el rango de grosor (1 a 4) y el grupo «Info», según el código 0.1.0.0 |
| 0.4.0.0 | 2026-11-21 | Rehecha con la plantilla estándar. Describe el código 0.1.0.0: ajustes con su valor por defecto, equivalencia en tiempo, colores y marcas, alertas y marcos temporales |
