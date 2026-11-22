# [JLC32 Comparative] OBV leadership · Guía operativa

Cómo se añade y se ajusta. Qué dice la fuente y cómo se lee, en la guía técnica.

| Campo | Valor |
|---|---|
| Título en TradingView | `[JLC32 Comparative] OBV leadership` |
| Nombre corto | `JLC32 OBV` |
| Script | Versión 0.3.0.0 (ver control de cambios) |

---

## Cómo se añade

1. Abre el gráfico normal del valor o del ETF que quieres mirar, en diario o en semanal. Nunca un ratio ni un spread: no tienen volumen real y el OBV no mide nada.
2. En Indicadores, busca el título o el nombre corto y añádelo.
3. Queda en un panel aparte, bajo el gráfico, con el OBV y su media. Si el símbolo no aporta volumen, aparece una etiqueta roja en la última barra.

## Ajustes

| Ajuste | Por defecto | Qué hace | Cuándo tocarlo |
|---|---|---|---|
| Suavizado OBV (SMA) | 20 | Periodo de la media simple del OBV, que ayuda a ver su tendencia (mínimo 1) | Para suavizar más o menos la línea; la fuente no fija plazo |
| Avisar si el símbolo no tiene volumen utilizable | Sí | Muestra una etiqueta roja en la última barra si el símbolo no aporta volumen | Quítalo si ya sabes que el símbolo tiene volumen y la etiqueta estorba |
| Marcar liderazgo y divergencia del OBV | Sí | Dibuja los triángulos de liderazgo y los círculos de divergencia | Quítalo para ver solo el OBV y su media; las alertas siguen activas |
| [Propuesta] Ventana de comparación (barras) | 20 | Barras sobre las que se busca el máximo o el mínimo del OBV y del precio (mínimo 2) | Es una propuesta del script: la fuente compara a ojo, sin plazo. Tiene explicación al pasar el ratón (tooltip) |

## Equivalencia en tiempo

| Ajuste | Valor | En diario | En semanal |
|---|---|---|---|
| Suavizado OBV (SMA) | 20 | 20 sesiones (cuatro semanas de mercado) | 20 semanas |
| [Propuesta] Ventana de comparación (barras) | 20 | 20 sesiones | 20 semanas |

El script usa el marco del gráfico; no fuerza ninguno.

## Colores y marcas

| Elemento | Color o forma | Qué indica |
|---|---|---|
| OBV | Línea marrón, grosor 2 | Volumen acumulado: suma el volumen si el cierre sube y lo resta si baja |
| OBV suavizado | Línea naranja ámbar, grosor 1 | Media simple del OBV |
| OBV lidera al alza [Propuesta] | Triángulo verde hacia arriba, abajo del panel | El OBV marca el máximo de la ventana y el precio no |
| OBV lidera a la baja [Propuesta] | Triángulo rojo hacia abajo, arriba del panel | El OBV marca el mínimo de la ventana y el precio no |
| Divergencia: precio arriba sin volumen [Propuesta] | Círculo naranja, arriba del panel | El precio marca el máximo de la ventana, el OBV no y está por debajo de donde estaba una ventana antes |
| Divergencia: precio abajo sin volumen [Propuesta] | Círculo azul, abajo del panel | El precio marca el mínimo de la ventana, el OBV no y está por encima de donde estaba una ventana antes |
| Etiqueta «Sin volumen utilizable» | Etiqueta roja, en la última barra | El símbolo no aporta volumen (ratio, spread, algún índice): el OBV no se puede interpretar |

Cada marca aparece solo en la primera barra en que se cumple la condición; no se repite mientras dura.

## Alertas

Cuatro, con estos nombres exactos. Se alerta el cambio, no el estado.

| Alerta | Salta cuando |
|---|---|
| `JLC32 OBV · lidera al alza` | el OBV marca el máximo de la ventana y el precio no |
| `JLC32 OBV · lidera a la baja` | el OBV marca el mínimo de la ventana y el precio no |
| `JLC32 OBV · divergencia, subida sin volumen` | el precio marca el máximo de la ventana, el OBV no y está por debajo de donde estaba una ventana antes |
| `JLC32 OBV · divergencia, caída sin volumen` | el precio marca el mínimo de la ventana, el OBV no y está por encima de donde estaba una ventana antes |

Las alertas no dependen del ajuste «Marcar liderazgo y divergencia del OBV»: saltan aunque los marcadores estén ocultos.

Para crearlas: botón de alerta, condición = este indicador, elegir la alerta de la lista. Recomendado `[Propuesta]`: una vez por cierre de vela.

## Marcos temporales

Diario o semanal, el marco con el que decidas. Cava señala que no suele trabajarse con volúmenes en gráficos mensuales; por eso en mensual no se recomienda. El script calcula sobre la barra en curso: durante su formación una marca puede aparecer y desaparecer, y al cierre queda fija.

---

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-21 | Primera versión, con la plantilla estándar. Describe el código 0.1.1.0: ajustes con su valor por defecto, equivalencia en tiempo, colores y marcas, alertas con su nombre exacto y marcos temporales |
| 0.2.0.0 | 2026-11-22 | Alineada con el código 0.3.0.0: versión del script, título (sin «(Murphy)») y nombres de alerta con su prefijo exacto |
