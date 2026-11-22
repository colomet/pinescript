# [JLC41 Trend] Traffic light: monthly MACD + weekly MACD + weekly stochastic {60/40} · Guía operativa

Cómo se añade y se ajusta. Qué dice la fuente y cómo se lee, en la guía técnica.

| Campo | Valor |
|---|---|
| Título en TradingView | `[JLC41 Trend] Traffic light: monthly MACD + weekly MACD + weekly stochastic {60/40}` |
| Nombre corto | `JLC41 Trend light` |
| Script | Versión 0.3.0.0 (ver control de cambios) |

---

## Cómo se añade

1. Abre el gráfico diario del valor o índice que quieres evaluar. El script lee por su cuenta los marcos semanal y mensual: no hace falta cambiar de temporalidad.
2. En Indicadores, busca el título o el nombre corto y añádelo.
3. Se dibuja sobre el gráfico de precio: una tabla en la esquina elegida y el fondo coloreado cuando hay sentido de tendencia.
4. Si la tabla marca INDEFINIDO no es un fallo: las tres condiciones de la fuente no concuerdan y no hay sentido que decidir.

## Ajustes

| Ajuste | Por defecto | Qué hace | Cuándo tocarlo |
|---|---|---|---|
| Leer solo barras semanales/mensuales cerradas | Sí | Con «Sí» usa la última barra semanal y mensual ya cerrada, y el estado no cambia después. Con «No» usa la barra en curso | Déjalo en «Sí» para decidir o registrar. Ponlo en «No» solo para anticipar: la barra en curso puede cambiar hasta su cierre |
| MACD rápido | 12 | Periodo de la media exponencial rápida del MACD (mínimo 1) | Solo si cambias el MACD de la fuente (12, 26 y 9) |
| MACD lento | 26 | Periodo de la media exponencial lenta del MACD (mínimo 1) | Igual que el anterior |
| MACD señal | 9 | Periodo de la línea de señal del MACD (mínimo 1) | Igual que el anterior |
| Estocástico %K (n) | 14 | Barras semanales del rango máximo-mínimo con que se calcula el %K (mínimo 1) | Solo si quieres otro plazo: la fuente trabaja con 14 |
| Mostrar tabla de estado | Sí | Dibuja la tabla con el estado y las tres condiciones | Quítalo si solo quieres el fondo coloreado |
| Colorear el fondo según el estado | Sí | Pinta el fondo de verde con ALCISTA y de rojo con BAJISTA; con INDEFINIDO no pinta | Quítalo si el fondo estorba y te basta la tabla |
| Posición de la tabla | Superior derecha | Esquina de la tabla: Superior derecha, Superior izquierda, Inferior derecha o Inferior izquierda | Cámbiala si tapa el precio u otra tabla |

Los marcos (mensual y semanal) y los umbrales (60, 40 y cero) los fija la fuente y no se ajustan.

## Equivalencia en tiempo

| Ajuste | Valor | En diario | En semanal |
|---|---|---|---|
| MACD rápido | 12 | 12 semanas en el MACD semanal y 12 meses en el mensual | Igual |
| MACD lento | 26 | 26 semanas y 26 meses | Igual |
| MACD señal | 9 | 9 semanas y 9 meses | Igual |
| Estocástico %K (n) | 14 | 14 semanas | Igual |

El script pide sus propios marcos, mensual y semanal, con independencia del gráfico: los valores significan lo mismo en el gráfico diario y en el semanal.

## Colores y marcas

| Elemento | Color o forma | Qué indica |
|---|---|---|
| Fondo del gráfico | Verde muy tenue | Estado ALCISTA |
| Fondo del gráfico | Rojo muy tenue | Estado BAJISTA |
| Fondo del gráfico | Sin color | Estado INDEFINIDO, o fondo desactivado en los ajustes |
| Tabla, fila «TENDENCIA» | Fondo verde (ALCISTA), rojo (BAJISTA) o gris (INDEFINIDO) | Estado del semáforo y, a la derecha, cuántas de las tres condiciones apuntan al alza (↑) y a la baja (↓) |
| Tabla, fila «MACD mensual» | Texto «cortado al alza» o «cortado a la baja»; casilla verde ↑ o roja ↓ | La línea rápida del MACD mensual está por encima o por debajo de su línea de señal |
| Tabla, fila «MACD semanal» | Valor del MACD semanal con «(>0)» o «(<0)»; casilla verde ↑ o roja ↓ | La línea rápida del MACD semanal está por encima o por debajo de cero |
| Tabla, fila «Estocástico %K sem.» | Valor con «(>60)», «(<40)» o «(40-60)»; casilla verde ↑, roja ↓ o gris – | El %K semanal está por encima de 60, por debajo de 40 o entre ambos niveles |
| Tabla, última fila | Texto gris | «Barras cerradas» o «Barra en curso», y la referencia de la fuente (*El arte de especular*, I.5.3, p. 37) |

La tabla muestra el estado de la última barra; el fondo coloreado recoge todo el histórico.

## Alertas

Tres, con estos nombres exactos. Se alerta el cambio, no el estado.

| Alerta | Salta cuando |
|---|---|
| `JLC41 Semáforo · pasa a ALCISTA` | Las tres condiciones se alinean al alza: MACD mensual cortado al alza, MACD semanal sobre cero y %K semanal sobre 60 |
| `JLC41 Semáforo · pasa a BAJISTA` | Las tres condiciones se alinean a la baja: MACD mensual cortado a la baja, MACD semanal bajo cero y %K semanal bajo 40 |
| `JLC41 Semáforo · pasa a INDEFINIDO` | El estado deja de ser ALCISTA o BAJISTA: las tres condiciones han dejado de concordar |

Para crearlas: botón de alerta, condición = este indicador, elegir la alerta de la lista. Recomendado `[Propuesta]`: una vez por cierre de vela.

Con la lectura de barras cerradas activada, el estado solo puede cambiar en la primera barra de una semana o de un mes nuevos.

## Marcos temporales

Gráfico diario, como indica la cabecera del script. El semáforo lee por su cuenta el marco semanal y el mensual, que fija la fuente y no son ajustables. Con la lectura de barras cerradas activada no repinta: el estado no cambia a posteriori. Con ella desactivada se ve la barra en curso, útil para anticipar y no para registrar, porque puede cambiar hasta el cierre de la semana o del mes.

---

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-21 | Primera versión, con la plantilla estándar. Describe el código 0.1.1.0: ajustes con su valor por defecto, equivalencia en tiempo, colores y marcas, alertas con su nombre exacto y marcos temporales |
| 0.2.0.0 | 2026-11-22 | Alineada con el código 0.3.0.0: versión del script y título (sin «(Cava)»); nombres de alerta con su prefijo exacto |
