# [GEN71 Management] SMMA 150 exit line · Guía operativa

Cómo se añade y se ajusta. Qué dice la fuente y cómo se lee, en la guía técnica.

| Campo | Valor |
|---|---|
| Título en TradingView | `[GEN71 Management] SMMA 150 exit line` |
| Nombre corto | `GEN71 SMMA 150` |
| Script | Versión 0.1.1.0 (ver control de cambios) |

---

## Cómo se añade

1. Abre el gráfico del activo, en el marco con el que operes.
2. En Indicadores, busca el título o el nombre corto y añádelo.
3. Se dibuja sobre el precio, con una sola línea morada.

## Ajustes

Tres ajustes, sin grupos: dos con explicación al pasar el ratón (tooltip) y una ficha de solo lectura.

| Ajuste | Por defecto | Qué hace | Cuándo tocarlo |
|---|---|---|---|
| Longitud | 150 | Velas con las que se calcula la media (mínimo 1). Menos velas, más rápida; más velas, más lenta | `[Aportado]`: 150 es el periodo de la regla que cita el script. Cambiarlo da otra media, no la de esa regla |
| Fuente | cierre | Serie de precios sobre la que se calcula la media | Solo si quieres la media sobre otra serie. La regla que cita el script habla del precio; el script usa el cierre |
| Ficha | — | Resumen de solo lectura | No se puede cambiar |

## Equivalencia en tiempo

Son velas, no días. Con 5 sesiones por semana:

| Ajuste | Valor | En diario | En semanal |
|---|---|---|---|
| Longitud | 150 | 150 sesiones, unas 30 semanas (casi 7 meses) | 150 semanas, casi 3 años |

## Colores y marcas

| Elemento | Color o forma | Qué indica |
|---|---|---|
| SMMA | Línea morada (#673AB7), grosor 1 | La media móvil suavizada de 150 velas del cierre |

El color va fijo en el código: no hay ajuste de color. No hay más marcas.

## Alertas

Este script no define alertas.

## Marcos temporales

El del gráfico: el script no fuerza ninguno, y la media cuenta velas del marco en que se carga (ver «Equivalencia en tiempo»).

---

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-21 | Creación para el código legado 0.1.0.0 («[Aportado] Smoothed Moving Average 150d», interfaz en inglés). Archivada |
| 0.2.0.0 | 2026-11-22 | Describe el código 0.1.1.0: título `[GEN71 Management] SMMA 150 exit line`, ajustes en castellano con tooltip, ficha de solo lectura |
