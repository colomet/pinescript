# GEN82 · Pack Estocástico + RSI (Pablo Gil) · Guía operativa

Versión del documento: 0.2.0.0 · 22/11/2026
Script: `[GEN82 Pack] Stochastic and RSI` v0.1.1.0 · probado en TradingView por Antonio

## Qué muestra

Dos indicadores en el mismo panel inferior:
- Estocástico: dos líneas, %K (azul) y %D (naranja). Mide dónde está el cierre dentro del rango máximo-mínimo de las últimas 18 velas, suavizado.
- RSI: una línea morada. Mide la fuerza de los movimientos recientes.
Líneas horizontales: 80 y 20 (estocástico), 70 y 30 (RSI), 50 (centro).
El script no da señales ni alertas. Solo dibuja.

## Cómo añadirlo

1. Pegar el código del `.pine` en el editor de Pine de TradingView y «Añadir al gráfico».
2. Aparece en un panel aparte bajo el precio, con el nombre «GEN82 Stoch+RSI».

## Ajustes

| Ajuste | Por defecto | Qué cambia |
|---|---|---|
| %K longitud | 18 | Velas del rango. Menos, más nervioso; más, más suave |
| %K suavizado | 9 | Media que suaviza %K. Con 1 no suaviza |
| %D suavizado | 5 | Media de %K que forma %D |
| Periodo RSI | 14 | Velas del RSI |
| Fuente RSI | close | Serie sobre la que se calcula el RSI |
| Color %K / %D / RSI | azul / naranja / morado | Solo aspecto |

Cada ajuste lleva una explicación al pasar el ratón. La tabla completa de ajustes con la hoja G4 queda pendiente (T6 de pendientes).

## Cómo se lee

Lectura del origen, sin contrastar con una fuente [Interpretación; T12 de pendientes]:
- RSI sobre 50 y %K cruza %D hacia arriba fuera de la zona baja: fuerza compradora
- RSI bajo 50 y %K cruza %D hacia abajo: debilidad o inicio de corrección
- Estocástico y RSI a la vez en zona alta: posible agotamiento del movimiento alcista
- Precio hace nuevos máximos y ni RSI ni estocástico los acompañan: posible divergencia bajista
Zonas: estocástico alto sobre 80 y bajo bajo 20; RSI alto sobre 70 y bajo bajo 30. El origen decía 25 en el texto; la línea era 20 y así se ha dejado.

## Límites

- Herramienta de análisis; no es una recomendación de inversión
- No pide símbolos externos; funciona en cualquier marco temporal
