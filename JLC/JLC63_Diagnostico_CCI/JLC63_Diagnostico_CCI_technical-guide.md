# [JLC63 Diagnostic] CCI: 14 {threshold +/-50 in / 0 out} · Guía técnica

Qué es el script, qué dice la fuente y cómo se lee lo que dibuja. La configuración, en la guía operativa.

| Campo | Valor |
|---|---|
| Procedencia | JLC (sistema de señales con el CCI según Cava, capítulo VII de *El arte de especular*; en adelante EA) |
| Script | Versión 0.3.0.0 (ver control de cambios) |

---

## Qué es

Dibuja en un panel el Commodity Channel Index (CCI) de 14 periodos con el umbral de entrada en ±50, el nivel de cancelación en 0 y las señales del sistema de Cava: entrada larga y su cancelación, entrada corta y su cancelación. Las señales se filtran con la tendencia dominante, que el usuario fija a mano en un ajuste: el script no la calcula. Se aplica sobre el gráfico del valor en cualquier marco. Lee la zona de sobrecompra, en el sentido de la tendencia, como prueba de fuerza y no como señal de venta.

## Qué dice la fuente

- **Cálculo (EA VII.1, pp. 185-186):** el CCI mide cuánto se aleja el precio «significativo», la media del máximo, el mínimo y el cierre, de su media simple, dividido por una constante por la desviación media: la media simple de los valores absolutos de las desviaciones (p. 186). Lambert recomendó periodos de 5 a 20 días y Cava prefiere 14 (p. 186).
- **Constante (EA VII.1, pp. 185-186):** el libro imprime la constante 0,15 y explica que Lambert la eligió para que entre el 70 % y el 80 % de los valores caigan entre +100 y −100 (p. 186).
- **Interpretación tradicional (EA VII.2, pp. 186-187):** sobrecompra por encima de 50 o de 100 y sobreventa por debajo de −50 o −100, según el producto. Compra cuando, tras entrar en sobreventa, el CCI gira al alza y supera 0; venta cuando, tras entrar en sobrecompra, gira a la baja y pierde 0 (p. 187). La significación de 50 o de 100 depende del periodo: con 5 días el CCI alcanza 100 con más facilidad que con 14 (p. 187).
- **Sistema de Cava (EA VII.3.1, pp. 187-188):** trabaja siempre con 14 periodos, en semanal, diario o intradiario. Sobrecompra al superar 50 y sobreventa al perder −50, salvo que a simple vista sean más significativos el 100 y el −100 (p. 187). Las señales están condicionadas siempre al sentido de la tendencia: en alcista se siguen las de compra y en bajista las de venta (pp. 187-188). Con tendencia alcista, la señal de compra llega cuando el CCI supera 50 y entra en sobrecompra, lo que indica una tendencia fuerte porque ha empujado al indicador hasta ahí; el recorrido es mayor cuanto más fuerte es la tendencia (p. 188).
- **Cancelación de largas (EA VII.3.1, p. 188):** se usa como referencia el nivel 0: cuando el CCI gira a la baja y pierde el cero, es señal de cancelación de las posiciones largas abiertas. En el ejemplo del IBEX 35 semanal, tras una cancelación en diciembre de 2005 la tendencia seguía siendo alcista porque el MACD semanal estaba sobre cero, y se mantuvo la prioridad de las señales de compra.
- **Lado bajista (EA VII.3.1, pp. 190-191):** con tendencia bajista, la señal de venta llega cuando el CCI pierde −50 y entra en sobreventa, lo que indica una tendencia bajista fuerte (p. 190). Las posiciones cortas se cancelan cuando el CCI supera el nivel cero (p. 191).
- **Movimientos correctivos (EA VII.3.1, pp. 188 y 191):** dentro de una tendencia bajista, una señal de compra suele tener menos recorrido, y Cava aconseja usar entonces la sobrecompra para posiciones cortas, cuando el CCI, tras salir de la zona, pierde el cero (p. 188). Lo simétrico vale dentro de una tendencia alcista (p. 191).
- **Con otros indicadores (EA VII.3.1, p. 192):** Cava usa el CCI en sintonía con el resto de los indicadores; si otros confirman la señal, la confianza en ella aumenta notablemente.
- **Tendencia (EA I.5.3, p. 37):** Cava la define con tres condiciones: el MACD mensual cortado, la línea rápida del MACD semanal respecto a cero y la línea rápida del estocástico semanal respecto a 60 y a 40.

**Cifras del script y su origen**

| Cifra | Valor | Origen |
|---|---|---|
| Periodo | 14 | EA VII.1, p. 186; VII.3.1, p. 187 |
| Precio | (máximo + mínimo + cierre) ÷ 3 | EA VII.1, p. 185 |
| Desviación | Media de las desviaciones absolutas respecto a la media simple | EA VII.1, p. 186 |
| Constante | 0,015 | `[Elaboración]`: es el valor habitual de Lambert. EA VII.1, pp. 185-186, imprime 0,15 en la fórmula y en el texto |
| Umbral de entrada | ±50, ajustable a ±100 | EA VII.3.1, p. 187 |
| Nivel de cancelación | 0 | EA VII.3.1, p. 188 (largas) y p. 191 (cortas) |
| Filtro de tendencia | Ajuste manual: Alcista, Bajista o Ambas | `[Elaboración]`: la fuente condiciona las señales a la tendencia, pero no dice cómo se introduce |
| Cuenta de posiciones abiertas | Solo cancela lo que antes ha entrado y no repite la entrada | `[Elaboración]`: Cava presenta la cancelación como una secuencia, entrada y después pérdida del cero |
| Desviación cero | Si el precio no varía en todo el periodo, arrastra el último valor válido (0 en la primera barra) | `[Propuesta]` |

## Qué se ve en el gráfico

| Elemento | Qué es | Cómo leerlo |
|---|---|---|
| CCI (morada, grosor 2) | Distancia del precio a su media, en unidades de su desviación habitual | Sin techo ni suelo fijos: en movimientos fuertes puede pasar de 100 o de −100 |
| Nivel 0 (continua) | Nivel de cancelación | Perderlo (largas) o superarlo (cortas) cancela la posición |
| Umbrales +U y −U (discontinuas) | Sobrecompra y sobreventa | Por defecto ±50 |
| Banda gris tenue, entre −U y +U | Relleno | Zona sin señal de entrada |
| Triángulo verde, abajo | Entrada larga | El CCI cruza al alza el +U con tendencia Alcista o Ambas |
| Aspa verde clara, abajo | Cancelación de la larga | El CCI pierde el 0 con una larga abierta |
| Triángulo rojo, arriba | Entrada corta | El CCI cruza a la baja el −U con tendencia Bajista o Ambas |
| Aspa roja clara, arriba | Cancelación de la corta | El CCI supera el 0 con una corta abierta |

## Cómo funciona, paso a paso

1. **Precio y media.** Toma el precio significativo, (máximo + mínimo + cierre) ÷ 3, y su media simple de n barras.
2. **Desviación.** Calcula la media de las desviaciones absolutas respecto a esa media simple, con la función `ta.dev` de TradingView.
3. **CCI.** (precio − media) ÷ (0,015 × desviación). Si la desviación es 0, arrastra el último valor válido y, si no hay ninguno, vale 0. `[Propuesta]`
4. **Cruces.** Detecta el cruce al alza del +U, el cruce a la baja del −U, la pérdida del 0 y la superación del 0.
5. **Posiciones.** Lleva dos estados, largo y corto. Entrada larga: cruce al alza del +U, con tendencia Alcista o Ambas y sin larga abierta. Cancelación larga: con larga abierta, el CCI pierde el 0. Entrada corta: cruce a la baja del −U, con tendencia Bajista o Ambas y sin corta abierta. Cancelación corta: con corta abierta, el CCI supera el 0. `[Elaboración]`
6. **Barra en curso.** El código no espera al cierre de la barra: una marca puede aparecer y desaparecer mientras se forma y queda fija al cierre.

## Cómo leerlo en situaciones concretas

| Lectura | Significa | Qué no significa |
|---|---|---|
| Triángulo verde con la tendencia alcista | Señal de compra y de tendencia fuerte: el CCI ha entrado en sobrecompra (EA VII.3.1, p. 188) | Una señal de venta por sobrecompra: aquí es prueba de fuerza, la contraria de la lectura tradicional (EA VII.2, p. 187) |
| Aspa verde | El CCI pierde el 0: cancelación de la larga (EA VII.3.1, p. 188) | Que la tendencia alcista haya terminado: en el ejemplo de la fuente seguía vigente (EA VII.3.1, p. 188) |
| Triángulo rojo con la tendencia bajista | Señal de venta y de tendencia fuerte: el CCI ha entrado en sobreventa (EA VII.3.1, p. 190) | Una señal de compra por sobreventa |
| Aspa roja | El CCI supera el 0: cancelación de la corta (EA VII.3.1, p. 191) | Una señal de compra por sí sola |
| Triángulo con la tendencia en «Ambas» | Una señal del CCI sin filtro: el script no sabe si la tendencia la acompaña | Una señal válida para Cava: él condiciona siempre las señales al sentido de la tendencia (EA VII.3.1, pp. 187-188) |
| Triángulo verde con tendencia bajista | Un rebote dentro de una caída: menos recorrido (EA VII.3.1, p. 188) | Una señal a seguir |
| CCI entre −U y +U, sin posición abierta | Sin señal de entrada activa | Que no haya tendencia |

## Cuándo usarlo y cuándo no

- **Sí:** con la tendencia dominante ya conocida y fijada en el ajuste, para seguir las señales a favor de ella y cancelar con el cero (EA VII.3.1, pp. 187-188); en cualquier marco, con el mismo periodo (EA VII.3.1, p. 187).
- **No:** sin fijar la tendencia; contra la tendencia dominante, donde la señal tiene menos recorrido (EA VII.3.1, p. 188); solo, sin otros indicadores que la confirmen (EA VII.3.1, p. 192).
- **Mal uso frecuente** `[Elaboración]`: leer el cruce del +50 como sobrecompra a vender; operar sin fijar el ajuste de tendencia; pasar a ±100 por sistema, cuando Cava lo deja a la observación de cada activo (EA VII.3.1, p. 187).

## Qué NO dice

- No calcula la tendencia dominante: se fija a mano en el ajuste. La fuente la define con tres condiciones (EA I.5.3, p. 37).
- No genera alertas.
- Reglas de la fuente que el script no implementa. `[Hueco declarado]`
  - Interpretación tradicional: compra al girar al alza y superar 0 tras la sobreventa, y venta al perder 0 tras la sobrecompra (VII.2, p. 187).
  - Uso de la sobrecompra para cortas, y de la sobreventa para largas, en los movimientos correctivos contra la tendencia (VII.3.1, pp. 188 y 191).
  - Divergencias del CCI, alcistas y bajistas (VII.3.2, pp. 192-194).

---

## Marcas de procedencia

Sin marca = regla de Cava con capítulo y página · `[Propuesta]` = cuantificación propia · `[Aportado]` = de terceros · `[Elaboración]` = extensión editorial · `[Hueco declarado]` = la fuente lo tiene y el código no.

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-15 | Primer borrador |
| 0.2.0.0 | 2026-11-21 | Adaptada a la plantilla estándar y al código 0.1.1.0. Citas contrastadas con EA (pp. 37, 185-194) |
| 0.3.0.0 | 2026-11-22 | Alineada con el código 0.3.0.0: versión del script y título (sin «(Cava)») |
