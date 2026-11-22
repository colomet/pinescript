# [JLC32 Comparative] OBV leadership · Guía técnica

Qué es el script, qué dice la fuente y cómo se lee lo que dibuja. La configuración, en la guía operativa.

| Campo | Valor |
|---|---|
| Procedencia | JLC (criterio de Murphy recogido por Cava en *Sistemas de especulación en bolsa*, apartado IX.2; en adelante SEB. El OBV se cita de *El arte de especular*, apartado IX.1.5; en adelante EA) |
| Script | Versión 0.3.0.0 (ver control de cambios) |

---

## Qué es

Dibuja el On Balance Volume (OBV) del símbolo del gráfico y su media simple, y marca dos situaciones: el OBV se adelanta al precio (liderazgo) o el precio se mueve sin que el volumen lo acompañe (divergencia). Se aplica sobre el gráfico normal de un valor o de un ETF, nunca sobre un ratio ni un spread. Es una lectura de confirmación: se mira después de haber elegido el activo.

## Qué dice la fuente

- **Murphy y el OBV (SEB IX.2, pp. 198-199 según la cabecera del script):** el script atribuye a este apartado que Murphy estudia el volumen con el OBV y compara la acción del precio con la del indicador: si el indicador lidera al precio, es una señal alcista. La comparación es visual, sin fórmula ni plazo.
- **Orden de trabajo (SEB IX.2, p. 198):** Murphy fija primero qué sector está más fuerte frente a los índices y a los demás sectores, y después pasa a identificar valores dentro de él. El script sigue ese orden: la fuerza relativa se lee en el gráfico del ratio (JLC31) y el volumen, en el gráfico normal del activo elegido.
- **Qué es el OBV (EA IX.1.5.1, pp. 255-256):** indicador de Joseph Granville. Cada día suma el volumen negociado si el precio cierra al alza y lo resta si cierra a la baja; si el cierre no cambia, el OBV tampoco. Se suele partir de un valor inicial alto para que no salga negativo.
- **Liderazgo (EA IX.1.5.1, p. 256):** Granville observó que el OBV sube o cae a menudo antes que el precio y por eso lo consideraba un indicador adelantado. Un nuevo máximo del OBV indica que los compradores han tomado el control y que es más probable que el precio siga subiendo; un nuevo mínimo, que lo han tomado los vendedores.
- **Divergencias (EA IX.1.5.1, p. 256):** cuando el OBV diverge del precio, la tendencia dominante se debilita. Precio en máximo sin que el OBV lo haga: divergencia bajista. Precio en mínimo sin que el OBV lo haga: divergencia alcista. Cuanto más tarda en formarse, más significativa es, y las pautas del OBV cerca de techos y suelos pesan más que sus niveles absolutos.
- **El volumen confirma y se anticipa (EA IX.1.5, p. 255; IX.1.2, p. 248):** los indicadores de volumen sirven para confirmar la fortaleza de la tendencia, y su falta de confirmación avisa de debilidad. Generalmente el volumen se anticipa al movimiento del precio.
- **Marco (EA IX.1.1, p. 237):** no suele trabajarse con volúmenes en gráficos mensuales.

**Cifras del script y su origen**

| Cifra | Valor | Origen |
|---|---|---|
| Acumulación del OBV | Suma o resta el volumen según el cierre | EA IX.1.5.1, pp. 255-256 |
| Valor inicial del OBV | 0 | El script parte de cero; la fuente propone un valor alto para evitar negativos (EA IX.1.5.1, p. 256). No cambia la lectura, que es de dirección y no de nivel |
| Media simple del OBV | 20 barras (ajustable) | `[Propuesta]`: ayuda de lectura; la fuente no fija plazo |
| Ventana de comparación | 20 barras (ajustable) | `[Propuesta]`: Murphy compara a ojo, sin plazo |
| Liderazgo | OBV en extremo de la ventana y precio no | `[Propuesta]`: método de detección sobre la idea de SEB IX.2 y EA IX.1.5.1, p. 256 |
| Divergencia | Precio en extremo de la ventana, OBV no y en sentido contrario al de hace una ventana | `[Propuesta]`: método de detección sobre EA IX.1.5.1, p. 256 |

## Qué se ve en el gráfico

| Elemento | Qué es | Cómo leerlo |
|---|---|---|
| OBV (marrón) | Volumen acumulado según el cierre | Importa su dirección frente a la del precio, no su valor |
| OBV suavizado (naranja ámbar) | Media simple del OBV | Ayuda a ver la tendencia del OBV `[Propuesta]` |
| Triángulo verde, abajo | El OBV marca el máximo de la ventana y el precio no | Liderazgo alcista `[Propuesta]` |
| Triángulo rojo, arriba | El OBV marca el mínimo de la ventana y el precio no | Liderazgo bajista `[Propuesta]` |
| Círculo naranja, arriba | Precio en máximo de la ventana, OBV no y por debajo de hace una ventana | Divergencia: la subida no tiene respaldo de volumen `[Propuesta]` |
| Círculo azul, abajo | Precio en mínimo de la ventana, OBV no y por encima de hace una ventana | Divergencia: la caída no tiene respaldo de volumen `[Propuesta]` |
| Etiqueta roja | El símbolo no aporta volumen utilizable | El OBV no es interpretable en ese símbolo |

## Cómo funciona, paso a paso

1. **Volumen disponible.** Una barra es «sin volumen» si el volumen no existe o vale cero. Con el aviso activado, la etiqueta roja sale en la última barra cuando está sin volumen.
2. **OBV.** Parte de cero. En cada barra suma el volumen si el cierre es mayor que el anterior, lo resta si es menor y no cambia si es igual.
3. **Media.** Media simple del OBV con el periodo de los ajustes.
4. **Extremos de la ventana.** El OBV está en máximo (o mínimo) si iguala el mayor (o menor) valor de las últimas N barras; solo se evalúa con volumen. El precio está en máximo (o mínimo) si su cierre iguala el mayor (o menor) de las últimas N barras.
5. **Liderazgo `[Propuesta]`.** Al alza: OBV en máximo y precio no. A la baja: OBV en mínimo y precio no.
6. **Divergencia `[Propuesta]`.** Subida sin volumen: precio en máximo, OBV no y por debajo del valor que tenía N barras antes. Caída sin volumen: precio en mínimo, OBV no y por encima del valor que tenía N barras antes.
7. **Marcas y alertas.** Cada condición se marca solo en la primera barra en que aparece. Las alertas usan las mismas condiciones y no dependen del ajuste que oculta los marcadores.
8. **Repintado.** El cálculo usa la barra en curso: durante su formación una marca puede aparecer y desaparecer; al cierre queda fija.

## Cómo leerlo en situaciones concretas

| Lectura | Significa | Qué no significa |
|---|---|---|
| Triángulo verde | Liderazgo alcista `[Propuesta]`: el OBV va por delante del precio, que para Murphy es señal alcista (según la cabecera del script) y para Granville es lo habitual en el OBV (EA p. 256) | No es una orden de compra ni dice cuánto tardará el precio en seguirlo |
| Triángulo rojo | Liderazgo bajista `[Propuesta]`: el OBV marca mínimo y, según EA p. 256, el control es de los vendedores | No es una orden de venta por sí solo |
| Círculo naranja | Divergencia bajista `[Propuesta]`: el precio sube sin respaldo de volumen (EA p. 256) | No anuncia un techo: indica que la tendencia se debilita |
| Círculo azul | Divergencia alcista `[Propuesta]`: el precio cae sin que el volumen acompañe (EA p. 256) | No anuncia un suelo |
| OBV y precio en la misma dirección | Confirmación: lo más probable es que la tendencia continúe (EA p. 256) | El script no marca nada: sin marca no hay lectura especial |
| Etiqueta roja | Sin volumen utilizable | No es «el volumen no confirma»: sin dato no hay lectura |
| Línea del OBV plana o vacía | Falta de datos de volumen | No es falta de confirmación |

## Cuándo usarlo y cuándo no

- **Sí:** sobre el gráfico normal de un valor o ETF elegido antes por fuerza relativa, en diario o semanal.
- **No:** sobre un símbolo ratio o spread, que no tiene volumen real y deja el OBV sin sentido; en gráficos mensuales (EA IX.1.1, p. 237).
- **Mal uso frecuente:** aplicarlo al gráfico del ratio; leer el nivel absoluto del OBV; confundir una línea plana con falta de confirmación; tratar un triángulo como orden de entrada.

## Qué NO dice

- No dice cuándo entrar ni qué comprar.
- El criterio mecánico de liderazgo y de divergencia y la ventana son `[Propuesta]`: la fuente compara a ojo, sin fórmula ni plazo.
- No incluye el Accumulation/Distribution de Williams (EA IX.1.5.2, pp. 256-257), otro indicador de volumen con otra fórmula. `[Hueco declarado]`

---

## Marcas de procedencia

Sin marca = regla de Cava con capítulo y página · `[Propuesta]` = cuantificación propia · `[Aportado]` = de terceros · `[Elaboración]` = extensión editorial · `[Hueco declarado]` = la fuente lo tiene y el código no.

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-15 | Primer borrador |
| 0.2.0.0 | 2026-11-21 | Adaptada a la plantilla estándar y al código 0.1.1.0. Citas contrastadas con EA (pp. 237-257) y SEB (p. 198) |
| 0.3.0.0 | 2026-11-22 | Alineada con el código 0.3.0.0: versión del script y título (sin «(Murphy)») |
