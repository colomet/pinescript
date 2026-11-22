# [JLC42 Trend] Dashboard: MACD + stochastic + CCI + ADX/DI + EMA, monthly/weekly/daily · Guía operativa

Cómo se añade y se ajusta. Qué dice la fuente y cómo se lee, en la guía técnica.

| Campo | Valor |
|---|---|
| Título en TradingView | `[JLC42 Trend] Dashboard: MACD + stochastic + CCI + ADX/DI + EMA, monthly/weekly/daily` |
| Nombre corto | `JLC42 Dashboard` |
| Script | Versión 0.3.0.0 (ver control de cambios) |

---

## Cómo se añade

1. Abre el gráfico diario del valor o índice que quieres evaluar. El script pide por su cuenta los marcos mensual y semanal.
2. En Indicadores, busca el título o el nombre corto y añádelo.
3. No dibuja nada sobre el precio: solo una tabla de cuatro columnas (indicador, mensual, semanal y diario) en la esquina elegida.
4. Empieza por la fila TENDENCIA, la última. Si marca INDEFINIDO, el resto de la tabla es contexto y no un permiso para entrar.

## Ajustes

| Ajuste | Por defecto | Qué hace | Cuándo tocarlo |
|---|---|---|---|
| Leer solo barras cerradas de los marcos superiores | Sí | Con «Sí», las columnas mensual y semanal usan la última barra cerrada y no cambian después. Con «No» usan la barra en curso. La columna diaria usa siempre la barra en curso | Déjalo en «Sí» para registrar. Ponlo en «No» para ver el mes o la semana en curso, sabiendo que pueden cambiar hasta su cierre |
| MACD rápido | 12 | Periodo de la media exponencial rápida del MACD (mínimo 1) | Solo si cambias el MACD de la fuente (12, 26 y 9) |
| MACD lento | 26 | Periodo de la media exponencial lenta del MACD (mínimo 1) | Igual que el anterior |
| MACD señal | 9 | Periodo de la línea de señal del MACD (mínimo 1) | Igual que el anterior |
| Estocástico %K | 14 | Barras con las que se calcula el %K en cada marco (mínimo 1) | Solo si quieres otro plazo: la fuente trabaja con 14 |
| CCI | 14 | Periodo del CCI en cada marco (mínimo 1) | Solo si quieres otro plazo: la fuente prefiere 14 |
| CCI · umbral (±) | 50 | Nivel desde el que el CCI se marca «sobrec.» (por encima) o «sobrev.» (por debajo, en negativo) (mínimo 1) | Súbelo a 100 si en el valor que estudias ese nivel es más significativo que el 50; la fuente lo admite |
| ADX / DI | 14 | Periodo del ADX y de los DI en cada marco (mínimo 1) | Solo si quieres otro plazo: la fuente sigue a Wilder (14) |
| EMA corta | 20 | Periodo de la media exponencial corta con la que se compara el precio (mínimo 1) | Solo si quieres otra media |
| EMA larga | 55 | Periodo de la media exponencial larga con la que se compara el precio (mínimo 1) | Solo si quieres otra media |
| Posición | Superior derecha | Esquina de la tabla: Superior derecha, Superior izquierda, Inferior derecha o Inferior izquierda | Cámbiala si tapa el precio u otra tabla |
| Tamaño de texto | Pequeño | Tamaño del texto de la tabla: Diminuto, Pequeño o Normal | Auméntalo si no se lee; redúcelo si la tabla ocupa demasiado |
| Mostrar valores numéricos junto al estado | Sí | Añade el valor del estocástico, del CCI y del ADX junto a su estado | Quítalo si prefieres una tabla más limpia |

Los marcos (mensual, semanal y diario) y los niveles del estocástico (80, 60, 40 y 20) y del ADX (20, 30 y 40) los fija la fuente y no se ajustan.

## Equivalencia en tiempo

| Ajuste | Valor | En diario | En semanal |
|---|---|---|---|
| MACD rápido, lento y señal | 12 / 26 / 9 | Columna mensual: meses. Semanal: semanas. Diario: sesiones | Mensual y semanal igual; la columna diario pasa a contar semanas |
| Estocástico %K | 14 | 14 meses, 14 semanas y 14 sesiones | La columna diario cuenta 14 semanas |
| CCI | 14 | 14 meses, 14 semanas y 14 sesiones | La columna diario cuenta 14 semanas |
| ADX / DI | 14 | 14 meses, 14 semanas y 14 sesiones | La columna diario cuenta 14 semanas |
| EMA corta y larga | 20 / 55 | 20 y 55 meses, semanas y sesiones | La columna diario cuenta semanas |

La columna DIARIO se calcula sobre el marco del propio gráfico: solo es diaria si el gráfico es diario.

## Colores y marcas

| Elemento | Color o forma | Qué indica |
|---|---|---|
| Cabecera «CAVA / MENSUAL / SEMANAL / DIARIO» | Gris azulado oscuro | Los tres marcos |
| Celda verde, roja o gris | Verde = lectura al alza; rojo = lectura a la baja; gris = neutra o sin lectura | Se aplica a todas las filas salvo ADX |
| Fila «MACD corte» | Texto «alza», «baja» o «—» | La línea rápida del MACD está por encima de su señal, por debajo o igual |
| Fila «MACD vs 0» | Texto «>0», «<0» o «—» | La línea rápida del MACD está por encima de cero, por debajo o igual |
| Fila «Estoc. %K» | Mensual y semanal: «alto» (sobre 60), «bajo» (bajo 40) o «medio». Diario: «sobrec.» (sobre 80), «sobrev.» (bajo 20) o «medio». En los tres, verde sobre 60 y rojo bajo 40 | Posición del %K; con el ajuste de valores, se añade el número |
| Fila «CCI ±50» (el número sigue al ajuste) | «sobrec.» verde, «sobrev.» rojo o «neutro» gris | El CCI supera el umbral, cae bajo el umbral en negativo o queda entre ambos |
| Fila «ADX fuerza» | «muy fuerte» (sobre 40), «fuerte» (sobre 30), «media» (de 20 a 30) o «sin tend.» (bajo 20); fondo gris azulado oscuro si el ADX supera 30 y gris en los demás casos | Fuerza de la tendencia, no su dirección |
| Fila «DI dirección» | «+DI» verde, «-DI» rojo o «—» gris | Cuál de los dos DI domina |
| Fila «Precio vs EMA» | «sobre 20 / sobre 55», «bajo 20 / bajo 55» o mezcla; verde si está sobre las dos, rojo si está bajo las dos y gris en el resto | Posición del cierre frente a las dos medias (los números siguen a los ajustes) |
| Fila «TENDENCIA», estado | Verde ALCISTA, rojo BAJISTA o gris INDEFINIDO | Semáforo con las tres condiciones de la fuente (MACD mensual, MACD semanal y %K semanal) |
| Fila «TENDENCIA», texto gris «I.5.3 p.37» | Texto gris | Referencia de la fuente (*El arte de especular*, I.5.3, p. 37) |
| Fila «TENDENCIA», recuento «n↑ / n↓» | Verde si hay más lecturas al alza, rojo si hay más a la baja y gris si empatan | Cuántas de las seis lecturas del marco diario apuntan a cada lado |

Las seis lecturas del recuento son: MACD sobre su señal, MACD sobre cero, %K sobre 60, CCI sobre el umbral, +DI sobre -DI y precio sobre la EMA corta; a la baja, las contrarias. El ADX y la EMA larga no cuentan.

## Alertas

Cinco, con estos nombres exactos. Se alerta el cambio, no el estado.

| Alerta | Salta cuando |
|---|---|
| `JLC42 Tablero · TENDENCIA pasa a ALCISTA` | Las tres condiciones de la fila TENDENCIA se alinean al alza |
| `JLC42 Tablero · TENDENCIA pasa a BAJISTA` | Las tres condiciones se alinean a la baja |
| `JLC42 Tablero · TENDENCIA pasa a INDEFINIDO` | El estado deja de ser ALCISTA o BAJISTA: las tres condiciones han dejado de concordar |
| `JLC42 Tablero · 5 de 6 indicadores al alza` | Cinco o más de las seis lecturas del marco diario apuntan al alza, tras haber sido menos de cinco en la barra anterior |
| `JLC42 Tablero · 5 de 6 indicadores a la baja` | Cinco o más de las seis lecturas del marco diario apuntan a la baja, tras haber sido menos de cinco en la barra anterior |

Para crearlas: botón de alerta, condición = este indicador, elegir la alerta de la lista. Recomendado `[Propuesta]`: una vez por cierre de vela.

Con la lectura de barras cerradas activada, el estado de la fila TENDENCIA solo puede cambiar en la primera barra de una semana o de un mes nuevos. Las dos alertas de cinco de seis usan el marco diario y la barra en curso.

## Marcos temporales

Gráfico diario, como indica la cabecera del script. Las columnas MENSUAL y SEMANAL las pide el script por su cuenta y son fijas. La columna DIARIO se calcula sobre el marco del gráfico: en un gráfico semanal o mensual deja de ser diaria. Con la lectura de barras cerradas activada, las columnas mensual y semanal no repintan; la diaria sí cambia durante la sesión, hasta el cierre de la barra.

---

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-21 | Primera versión, con la plantilla estándar. Describe el código 0.1.1.0: ajustes con su valor por defecto, equivalencia en tiempo, colores y marcas, alertas con su nombre exacto y marcos temporales |
| 0.2.0.0 | 2026-11-22 | Alineada con el código 0.3.0.0: versión del script y título (sin «(Cava)»); nombres de alerta con su prefijo exacto |
