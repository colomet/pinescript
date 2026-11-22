# [GEN21 Breadth] SPX vs S5FI/S5TH: divergence {50d/200d} · Guía técnica

Qué es, qué dice la fuente y cómo se lee. La configuración, en la guía operativa.

| Campo | Valor |
|---|---|
| Procedencia | GEN. Código propio; no procede de Cava |
| Script | Versión 0.1.1.0 |

---

## Qué es

Panel que dibuja dos líneas: el % de valores del S&P 500 que cotiza sobre su media de 50 sesiones (S5FI) y sobre su media de 200 (S5TH). Marca con un círculo cuando el índice y la amplitud se separan (divergencia).

Dice cuánta participación real hay detrás del movimiento del índice. No es el precio del S&P 500.

## Qué dice la fuente

S5FI y S5TH se usan por estar disponibles en TradingView, y los niveles 30 / 50 / 70 son convención técnica `[Aportado]`: no proceden de Cava. La detección de divergencia y su ventana son una mecanización propia `[Propuesta]` de una lectura a ojo.

Cava explica la idea de fondo en *El arte de especular* (EA), capítulo X, apartado X.1: si en una subida del índice se contrae el número de valores que lo acompañan, se forma una divergencia bajista que avisa de la debilidad de la tendencia alcista.

`[Hueco declarado]` Cava trata en el mismo capítulo otras medidas de amplitud que este script no implementa: la línea Avance/Descenso (EA X.1.1), el oscilador McClellan (X.1.2, pp. 271-272) y el índice Arms o TRIN (X.1.3, pp. 272-274).

## Qué se ve en el gráfico

| Elemento | Qué es | Cómo leerlo |
|---|---|---|
| Línea azul | S5FI, % sobre media de 50 sesiones | Participación a medio plazo |
| Línea naranja | S5TH, % sobre media de 200 sesiones | Participación a largo plazo |
| Niveles 70 / 50 / 30 | Referencias de convención [Aportado] | Por encima de 70: base amplia. Por debajo de 30: pocos valores acompañan |
| Círculo rojo (arriba) | Divergencia bajista [Propuesta] | El índice marca máximos de la ventana y la amplitud está por debajo de hace N velas |
| Círculo verde (abajo) | Divergencia alcista [Propuesta] | El índice marca mínimos de la ventana y la amplitud mejora |

## Cómo funciona, paso a paso

1. Lee tres símbolos en el marco del gráfico: el índice, S5FI y S5TH. Si falta alguno, no marca nada.
2. Divergencia bajista: el índice cierra en el máximo de la ventana **y** S5FI **o** S5TH está por debajo de hace N velas. Basta una de las dos series.
3. Divergencia alcista: simétrica. El índice en el mínimo de la ventana y S5FI **o** S5TH por encima de hace N velas [Elaboración].
4. Solo se marca la primera vela de cada divergencia.
5. Cinco alertas: las dos divergencias, S5FI cruza a la baja el nivel bajo, S5FI cruza al alza el nivel alto, S5TH cruza a la baja el nivel neutro.

## Cómo leerlo en situaciones concretas

1. **S5FI por encima de 70.** Subida con base amplia. Contexto sano, no señal de compra.
2. **S5FI por debajo de 30.** La mayoría de valores no acompaña: debilidad interna aunque el índice aguante.
3. **Círculo rojo.** El índice sube pero la participación se reduce. Es el aviso más útil del panel; puede tardar meses en reflejarse en el precio o no reflejarse nunca.
4. **Círculo verde.** El índice cae pero cada vez menos valores caen con él.
5. **S5TH pierde el 50.** Menos de la mitad del índice sobre su media de 200 sesiones.

## Cuándo usarlo y cuándo no

- **Sí:** una vez al día, antes de mirar ningún activo, para saber si el movimiento del índice tiene participación. En diario o superior.
- **No:** como señal de entrada o de salida. Como sustituto de las reglas de amplitud de Cava. En intradía (no hay datos).

## Qué NO dice

- No justifica los niveles 30 / 50 / 70 ni la ventana de 20 velas.
- No indica cuándo entrar o salir: es contexto.
- Con «S5FI **o** S5TH» puede dar más avisos que exigiendo las dos. Decisión de diseño, no probada.
- Una divergencia puede durar meses o no recogerse nunca. Se lee en directo: amplitud baja es debilidad, no oportunidad.

---

## Marcas de procedencia

Sin marca = regla de Cava con capítulo y página · `[Propuesta]` = cuantificación propia · `[Aportado]` = de terceros · `[Elaboración]` = extensión editorial · `[Hueco declarado]` = la fuente lo tiene y el código no.

---

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-15 | Borrador inicial |
| 0.2.0.0 | 2026-11-21 | Describe el script 0.1.1.0 |
| 0.3.0.0 | 2026-11-21 | Título igual al del código; capítulos y páginas de las medidas de amplitud de Cava contrastados con el libro |
