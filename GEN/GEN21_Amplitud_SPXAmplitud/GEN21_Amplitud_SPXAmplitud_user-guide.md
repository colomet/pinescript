# [GEN21 Breadth] SPX vs S5FI/S5TH: divergence {50d/200d} · Guía operativa

Cómo se añade y se ajusta. Qué dice la fuente y cómo se lee, en la guía técnica.

| Campo | Valor |
|---|---|
| Título en TradingView | `[GEN21 Breadth] SPX vs S5FI/S5TH: divergence {50d/200d}` |
| Nombre corto | `GEN21 Breadth` |
| Script | Versión 0.1.1.0 |

---

## Cómo se añade

1. En un gráfico diario o semanal, abre **Indicadores** y busca `GEN21 Breadth`.
2. Añádelo: se dibuja en un panel aparte, debajo del gráfico.
3. Funciona sobre cualquier gráfico; no hace falta tener el S&P 500 abierto.

## Ajustes

| Ajuste | Por defecto | Qué hace | Cuándo tocarlo |
|---|---|---|---|
| Índice de referencia | `SP:SPX` | Índice con el que se compara la amplitud | Si tu plan no sirve ese símbolo |
| % sobre media de 50 sesiones | `INDEX:S5FI` | Línea azul | Si el ticker cambia |
| % sobre media de 200 sesiones | `INDEX:S5TH` | Línea naranja | Si el ticker cambia |
| Nivel alto (%) | 70 | Línea superior | Para otra convención |
| Nivel neutro (%) | 50 | Línea central | Rara vez |
| Nivel bajo (%) | 30 | Línea inferior | Para otra convención |
| Marcar divergencias índice / amplitud | Sí | Dibuja los círculos. No afecta a las alertas | Si quieres el panel limpio |
| Ventana de comparación (velas) | 20 | Qué es «máximo reciente» del índice y a cuántas velas atrás se compara la amplitud | Más velas: menos avisos; menos velas: más avisos |

Los niveles 30 / 50 / 70 son convención técnica, no una regla de Cava.

Cada ajuste lleva su explicación al pasar el ratón (tooltip). Los ajustes están en tres grupos, «Símbolos», «Niveles [Aportado]» y «Divergencia [Propuesta]»; el grupo «Información» trae un resumen de solo lectura.

## Equivalencia en tiempo

| Ajuste | Valor | En diario | En semanal |
|---|---|---|---|
| Ventana de comparación | 20 velas | Unas 4 semanas | Unos 5 meses |

## Colores y marcas

| Elemento | Color o forma | Qué indica |
|---|---|---|
| Línea azul | Azul | S5FI: % de valores sobre su media de 50 sesiones |
| Línea naranja | Naranja | S5TH: % de valores sobre su media de 200 sesiones |
| Líneas horizontales | Gris, discontinuas arriba y abajo, continua en el centro | Niveles alto, neutro y bajo; banda gris entre alto y bajo |
| Círculo rojo, arriba | Rojo | Divergencia bajista: el índice marca máximos y la amplitud cae |
| Círculo verde, abajo | Verde | Divergencia alcista: el índice marca mínimos y la amplitud mejora |

Solo se marca la primera vela de cada divergencia.

## Alertas

Cinco, con estos nombres exactos. Se alerta el cambio, no el estado.

| Alerta | Salta cuando |
|---|---|
| `GEN21 Amplitud · divergencia bajista` | el índice marca máximos de la ventana y la amplitud (S5FI o S5TH) ha caído respecto a hace N velas; solo la primera vela del episodio `[Propuesta]` |
| `GEN21 Amplitud · divergencia alcista` | el índice marca mínimos de la ventana y la amplitud (S5FI o S5TH) ha subido respecto a hace N velas; solo la primera vela del episodio `[Elaboración]` |
| `GEN21 Amplitud · S5FI pierde nivel bajo` | S5FI cruza a la baja el nivel bajo (30 por defecto) |
| `GEN21 Amplitud · S5FI supera nivel alto` | S5FI cruza al alza el nivel alto (70 por defecto) |
| `GEN21 Amplitud · S5TH pierde nivel neutro` | S5TH cruza a la baja el nivel neutro (50 por defecto) |

Para crearlas: botón de alerta, condición = este indicador, elegir la alerta de la lista. Recomendado `[Propuesta]`: una vez por cierre de vela. Las alertas de divergencia saltan aunque el ajuste «Marcar divergencias» esté desactivado.

## Marcos temporales

Diario y superiores. En intradía los datos de amplitud no existen y el panel sale vacío.

---

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-21 | Creación. Describe la versión 0.1.1.0 del script |
| 0.2.0.0 | 2026-11-21 | Adaptada a la plantilla estándar: título igual al del código, alertas con la condición de cada una, grupos de ajustes |
