# GEN82 · Pack Estocástico + RSI (Pablo Gil) · Guía técnica

Versión del documento: 0.2.0.0 · 22/11/2026
Código: GEN82_Pack_EstocasticoRSI_PGI.pine (= v0.1.1.0) · Pine v6
Probada en TradingView: sí (Antonio, 22/11/2026)
Validada en conector: no (límite de cuota diaria)

## Ficha

Título: `[GEN82 Pack] Stochastic and RSI` · shorttitle `GEN82 Stoch+RSI`
Tipo: indicador en panel inferior (`overlay = false`, `precision = 2`)
Categorías: estocástico = Diagnostic; RSI = Diagnostic (pack, N105)
Datos: gráfico actual, cualquier marco temporal; sin `request.*`; sin símbolos externos
Alertas: ninguna
Licencia: MPL 2.0 (SPDX-License-Identifier: MPL-2.0) · © colomet 2026

## Cálculo

Estocástico:
- `stochRaw = ta.stoch(close, high, low, longitud)` con longitud 18
- `stochK = ta.sma(stochRaw, 9)`
- `stochD = ta.sma(stochK, 5)`
RSI: `rsiValue = ta.rsi(fuente, 14)`, fuente por defecto `close`.
Todo igual que el origen [Verificado: comparado línea a línea con el pegado].

## Ajustes (inputs)

| Grupo | Ajuste | Por defecto | Límites |
|---|---|---|---|
| Estocástico | %K longitud | 18 | 1–500 |
| Estocástico | %K suavizado | 9 | 1–200 |
| Estocástico | %D suavizado | 5 | 1–200 |
| RSI | Periodo RSI | 14 | 1–500 |
| RSI | Fuente RSI | close | — |
| Aspecto | Color %K / %D / RSI | #1E88E5 / #FF6D00 / #7B1FA2 | — |
| Info | Resumen (ficha, solo lectura) | — | — |

El origen no tenía límites en los enteros; se añaden `minval`/`maxval`.

## Dibujo

Plots: «Estocástico %K», «Estocástico %D», «RSI» (línea, grosor 1).
Niveles (`hline`, fijos): 80 estocástico alto (rojo, discontinua) · 70 RSI alto (morado, punteada) · 50 centro (gris, continua) · 30 RSI bajo (morado, punteada) · 20 estocástico bajo (verde, discontinua).
Títulos sin cifras fijas: los parámetros son ajustables (N14).

## Diferencias con el origen

- Título sin autor; shorttitle nuevo
- About de 8 campos en lugar de la cabecera larga; el texto de uso va a la guía operativa
- Texto corregido: sobreventa del estocástico en 20 (el origen decía 25 en el texto y 20 en la línea)
- Límites en los ajustes, constantes con nombre, colores ajustables, ficha de solo lectura
- SPDX y año en la cabecera
- Cálculo: sin cambios

## Relación con otros scripts

GEN81 (RSI + MACD): también dibuja un RSI 14; aquí comparte panel con el estocástico (T10 de pendientes).
JLC62 (estocástico de Cava): según el pendientes anterior, el de Cava es 14 sin suavizar; el de aquí es 18-9-5, por tanto no son el mismo [Por confirmar: no he vuelto a abrir JLC62 ni el libro en esta tarea; T7].

## Límites y control de cambios

- Sin validar en el conector de TradingView (cuota diaria agotada); sí probada por Antonio en TradingView
- Atribución de los parámetros a Pablo Gil: la da el origen pegado, sin enlace a su publicación [Por confirmar, T4]
- Los niveles 80/20/70/30/50 son los usuales; ninguna fuente los fija en este script
- Cambios futuros: nueva versión W.X.Y.Z y nueva línea en la bitácora; nada se sobrescribe
