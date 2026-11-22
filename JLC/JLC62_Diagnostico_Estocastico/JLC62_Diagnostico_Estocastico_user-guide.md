# [JLC62 Diagnostic] Stochastic: 14 {80/60/40/20} · Guía operativa

Cómo se añade y se ajusta. Qué dice la fuente y cómo se lee, en la guía técnica.

| Campo | Valor |
|---|---|
| Título en TradingView | `[JLC62 Diagnostic] Stochastic: 14 {80/60/40/20}` |
| Nombre corto | `JLC62 Stochastic` |
| Script | Versión 0.3.0.0 (ver control de cambios) |

---

## Cómo se añade

1. Abre el gráfico del valor o índice en el marco que quieras evaluar, semanal o diario. El script no fuerza ningún marco: usa el del gráfico.
2. En Indicadores, busca el título o el nombre corto y añádelo.
3. Queda en un panel aparte, bajo el gráfico: dos líneas (%K y %D), cuatro niveles horizontales (80, 60, 40 y 20) y una banda gris entre 20 y 80.

## Ajustes

| Ajuste | Por defecto | Qué hace | Cuándo tocarlo |
|---|---|---|---|
| Período %K (n) | 14 | Número de barras del rango (máximo y mínimo) con el que se compara el cierre (mínimo 1) | 14 es el periodo habitual de la fuente (Hartle). La fuente admite probar otros: Lane usaba 3 y el más popular es 5 |
| Período %D (suma, no SMA) | 3 | Número de barras de las sumas con las que se calcula %D (mínimo 1). %D no es la media simple de %K: es el cociente de la suma de los últimos (cierre − mínimo) entre la suma de los últimos (máximo − mínimo) | 3 es el periodo de la fuente. Subirlo allana más %D; la fuente deja experimentar con otros periodos |

Los niveles 80, 60, 40 y 20 son fijos y no se ajustan.

## Equivalencia en tiempo

| Ajuste | Valor | En diario | En semanal |
|---|---|---|---|
| Período %K (n) | 14 | 14 sesiones | 14 semanas |
| Período %D (suma, no SMA) | 3 | 3 sesiones | 3 semanas |

El script usa el marco del gráfico; no fuerza ninguno.

## Colores y marcas

| Elemento | Color o forma | Qué indica |
|---|---|---|
| %K | Línea azul, grosor 2 | Línea rápida: la más sensible, sin suavizar |
| %D | Línea naranja, grosor 1 | Versión allanada de %K: la más lenta |
| Nivel 80 | Línea gris continua | Sobrecompra |
| Nivel 60 | Línea gris discontinua | Con %K semanal por encima, apoya la tendencia alcista |
| Nivel 40 | Línea gris discontinua | Con %K semanal por debajo, apoya la tendencia bajista |
| Nivel 20 | Línea gris continua | Sobreventa |
| Banda gris muy tenue, de 20 a 80 | Relleno | Zona entre sobreventa y sobrecompra |

El script no dibuja marcas de señal.

## Alertas

Este indicador no define alertas: solo dibuja las dos líneas y los niveles.

## Marcos temporales

El del gráfico, diario o semanal según lo que evalúes. Los niveles 60 y 40 solo sirven como filtro de tendencia con el gráfico semanal; en diario, úsalos como sobrecompra y sobreventa relajadas `[Elaboración]`. Las líneas se mueven mientras se forma la barra y quedan fijas al cierre.

---

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-21 | Primera versión, con la plantilla estándar. Describe el código 0.1.1.0: ajustes con su valor por defecto, equivalencia en tiempo, colores, ausencia de alertas y marcos temporales |
| 0.2.0.0 | 2026-11-22 | Alineada con el código 0.3.0.0: versión del script y título (sin «(Cava)») |
