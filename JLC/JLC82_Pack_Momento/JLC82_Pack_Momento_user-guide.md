# [JLC82 Pack] Momentum: stochastic + ADX/DI + CCI · Guía operativa

Cómo se añade y se ajusta. Qué dice la fuente y cómo se lee, en la guía técnica.

| Campo | Valor |
|---|---|
| Título en TradingView | `[JLC82 Pack] Momentum: stochastic + ADX/DI + CCI` |
| Nombre corto | `JLC82 Momentum` |
| Script | Versión 0.3.0.0 (ver control de cambios) |

---

## Cómo se añade

1. Abre el gráfico del valor en el marco con el que operes. El script no fuerza ningún marco: usa el del gráfico.
2. En Indicadores, busca el título o el nombre corto y añádelo.
3. Se dibuja en un panel aparte, no sobre el precio. Reúne tres osciladores: el estocástico (%K y %D), el ADX con las líneas +DI y -DI, y el CCI. Comparten panel y las líneas de referencia de 80, 60, 40, 30 y 20.
4. Cada oscilador se enciende y se apaga por separado, así que el pack sirve también como cualquier pareja de los tres. Vienen los tres encendidos.
5. El estocástico y el ADX usan su escala natural, de 0 a 100. El CCI no tiene techo ni suelo: para que quepa en el panel se dibuja reescalado, y la altura de su línea no es comparable con la de `JLC63 CCI`. Para leer niveles de CCI con precisión, usa ese indicador; para ver si coinciden los tres, este.

## Ajustes

Tres grupos en el diálogo del indicador: «Estocástico (EA V)», «ADX / DI (EA VIII)» y «CCI (EA VII)». Los niveles 80, 60, 40, 30 y 20, la constante del CCI (0,015), el rango de Elder (de 4 a 12 puntos), los colores y los grosores son fijos: no se ajustan. Solo el ajuste de la escala del CCI tiene descripción emergente.

| Ajuste | Por defecto | Qué hace | Cuándo tocarlo |
|---|---|---|---|
| Mostrar estocástico | Sí | Muestra %K (azul) y %D (naranja) | Apágalo si no lo usas. Las alertas del estocástico siguen activas aunque las líneas estén ocultas |
| Período %K (n) | 14 | Barras del rango del que se toman el máximo y el mínimo (mínimo 1) | 14 es el habitual de la fuente. Lane recomendó 3 o 5 para el corto plazo |
| Período %D (suma, no SMA) | 3 | Barras de las dos sumas con las que se calcula %D (mínimo 1). No es la media de %K | La fuente deja experimentar con otros períodos |
| Mostrar ADX y DI | Sí | Muestra el ADX (verde), el +DI (azul) y el -DI (rojo), y las marcas del ADX | Apágalo si no lo usas. Las alertas del ADX siguen activas |
| Período ADX/DI (n) | 14 | Rige los DI y el ADX a la vez (mínimo 1) | 14 es el de Cava, siguiendo a Wilder. Elder recomienda 13, y en semanal puede convenir 7 |
| [Propuesta] Caducidad de la condición previa (barras) | 60 | Barras que puede esperar la condición previa de la mejor señal del ADX antes de descartarse (mínimo 1) | `[Propuesta]`: la fuente dice «cierto tiempo» sin cifra. Con menos barras la señal es más exigente |
| Desarmar si el ADX supera 30 sin disparar | Sí | Si el ADX pasa de 30 sin que haya disparado la señal, la condición previa se descarta | Apágalo para que la condición previa dure hasta que caduque o dispare |
| Mostrar CCI (reescalado) | Sí | Muestra el CCI reescalado, sus tres líneas de referencia y las marcas del CCI | Apágalo si no lo usas. Las alertas del CCI siguen activas |
| Período CCI (n) | 14 | Barras de la media y de la desviación del CCI (mínimo 1) | Cava trabaja siempre con 14 |
| Umbral sobrecompra/sobreventa (±) | 50 | Nivel del CCI real cuyo cruce da la entrada: +umbral para la larga y -umbral para la corta (mínimo 1) | Cava usa 50 y pasa a 100 cuando a simple vista es más significativo |
| [Aportado] Escala de reescalado visual del CCI | 200 | Solo afecta al dibujo (mínimo 10, paso 10): el CCI se dibuja como 50 + 50 · CCI / escala. Las señales usan el CCI real | Súbela si la línea sale de la banda 0-100; bájala si quieres que ocupe más altura. Con 200, el umbral de 50 queda en 62,5 |
| Tendencia dominante (filtra señales del CCI) | Ambas | Alcista deja solo las marcas y alertas de larga del CCI; Bajista, solo las marcas de corta; Ambas, las dos | Fíjala a mano con la tendencia que marque `JLC41 Trend light`. No afecta al estocástico ni al ADX |

## Equivalencia en tiempo

| Ajuste | Valor | En diario | En semanal |
|---|---|---|---|
| Período %K (n) | 14 | 14 sesiones | 14 semanas |
| Período %D (suma, no SMA) | 3 | 3 sesiones | 3 semanas |
| Período ADX/DI (n) | 14 | 14 sesiones | 14 semanas |
| [Propuesta] Caducidad de la condición previa (barras) | 60 | 60 sesiones, unos tres meses | 60 semanas, algo más de un año |
| Período CCI (n) | 14 | 14 sesiones | 14 semanas |

El umbral y la escala del CCI se miden en puntos del CCI, no en tiempo. Los niveles 80, 60, 40, 30 y 20 son del panel y no cambian con el marco.

## Colores y marcas

| Elemento | Color o forma | Qué indica |
|---|---|---|
| %K | Línea azul, grosor 2 | Posición del cierre dentro del rango de 14 barras: la línea rápida del estocástico |
| %D | Línea naranja, grosor 1 | La línea lenta: razón de sumas de 3 barras, no media de %K |
| ADX | Línea verde, grosor 2 | Fuerza de la tendencia, no su sentido |
| +DI | Línea azul semitransparente, grosor 1 | Fuerza de los movimientos al alza |
| -DI | Línea roja semitransparente, grosor 1 | Fuerza de los movimientos a la baja |
| CCI (reescalado) | Línea morada, grosor 2 | El CCI real dibujado como 50 + 50 · CCI / escala |
| CCI +umbral | Línea morada muy clara, en escalón | Dónde se dibuja el +umbral del CCI (62,5 con los valores por defecto) |
| CCI −umbral | Línea morada muy clara, en escalón | Dónde se dibuja el -umbral del CCI (37,5 con los valores por defecto) |
| CCI cero | Línea morada aún más clara, en escalón | Dónde se dibuja el cero del CCI (50) |
| ADX · mejor señal de compra (VIII.6.2) | Triángulo verde hacia arriba, abajo del panel, pequeño | Se cumple la mejor señal de compra del ADX |
| ADX · mejor señal de venta (VIII.6.2) | Triángulo rojo hacia abajo, arriba del panel, pequeño | Se cumple la mejor señal de venta del ADX |
| ADX · giro de Elder (4-12 pts) | Círculo naranja, abajo del panel, diminuto | El ADX, tras caer bajo los DI, sube de 4 a 12 puntos desde su mínimo |
| CCI · entrada larga | Triángulo morado hacia arriba, arriba del panel, diminuto | El CCI real cruza al alza el +umbral, con la tendencia en Alcista o Ambas y sin larga abierta |
| CCI · cancela larga | Aspa morada clara, arriba del panel, diminuta | Con una larga abierta, el CCI real pierde el nivel 0 |
| CCI · entrada corta | Triángulo morado hacia abajo, abajo del panel, diminuto | El CCI real cruza a la baja el -umbral, con la tendencia en Bajista o Ambas y sin corta abierta |
| CCI · cancela corta | Aspa morada clara, abajo del panel, diminuta | Con una corta abierta, el CCI real supera el nivel 0 |

Líneas fijas del panel, con su etiqueta: 80 (gris continua, «sobrecompra»), 60 y 40 (grises discontinuas, «tendencia alcista» y «tendencia bajista»), 30 (gris punteada más clara, «ADX tendencia fuerte») y 20 (gris continua, «sobreventa / ADX bajo»). El tramo entre 80 y 20 va sombreado.

El script lleva la cuenta de las posiciones del CCI: solo cancela lo que antes ha entrado y no repite la entrada mientras la posición sigue abierta.

## Alertas

Siete, con estos nombres exactos. Se alerta el cambio, no el estado.

| Alerta | Salta cuando |
|---|---|
| `JLC82 ADX · mejor señal de compra` | Con la condición previa armada (ADX bajo 20 y bajo los dos DI), el ADX cruza al alza el -DI, el +DI está sobre el -DI y sube, y el -DI baja |
| `JLC82 ADX · mejor señal de venta` | Lo simétrico: el ADX cruza al alza el +DI, el -DI está sobre el +DI y sube, y el +DI baja |
| `JLC82 ADX · giro de Elder` | El ADX, que estaba bajo los dos DI, sube desde su mínimo y cruza los 4 puntos sin pasar de 12 |
| `JLC82 CCI · entrada larga` | El CCI real cruza al alza el umbral, con la tendencia en Alcista o Ambas y sin larga abierta |
| `JLC82 CCI · cancela larga` | Con una larga abierta, el CCI real cruza a la baja el nivel 0 |
| `JLC82 Estocástico · sale de sobrecompra` | %K cruza a la baja el nivel 80 |
| `JLC82 Estocástico · sale de sobreventa` | %K cruza al alza el nivel 20 |

Para crearlas: botón de alerta, condición = este indicador, elegir la alerta de la lista. Cada una lleva su mensaje explicativo. Recomendado `[Propuesta]`: una vez por cierre de vela.

Ninguna depende de los interruptores de mostrar: saltan aunque las líneas o las marcas estén ocultas. Las dos del CCI dependen del ajuste de tendencia: con Bajista no salta ninguna. No hay alertas para la entrada corta ni para la cancelación corta del CCI, aunque el panel dibuja las cuatro marcas. Las del estocástico siguen la línea %K y no miran %D.

Mientras la barra se forma, el cruce puede deshacerse; «una vez por cierre de vela» solo avisa si la barra termina cruzada.

## Marcos temporales

El del gráfico. El script no fuerza ningún marco ni pide datos de otros. La fuente aplica el estocástico sobre todo al gráfico diario, y también al intradiario, semanal y mensual; usa el CCI de 14 períodos en semanal, diario o intradiario; y trabaja el ADX con 14, con 7 como posible alternativa en semanal. Las líneas de 60 y 40 son las del filtro de tendencia con el estocástico semanal: en otro marco no cumplen ese papel. El script no espera al cierre de la barra: mientras se forma, las líneas y las marcas pueden cambiar; al cerrar, quedan fijas.

---

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-21 | Primera versión, con la plantilla estándar. Describe el código 0.1.2.0: ajustes con su valor por defecto, equivalencia en tiempo, colores y marcas, alertas y marcos temporales |
| 0.2.0.0 | 2026-11-22 | Alineada con el código 0.3.0.0: versión del script y título (sin «(Cava)») |
