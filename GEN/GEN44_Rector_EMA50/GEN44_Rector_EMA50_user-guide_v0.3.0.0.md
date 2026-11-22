# [GEN44 Trend] EMA 50 + smoothing · Guía operativa

Cómo se añade y se ajusta. Qué dice la fuente y cómo se lee, en la guía técnica.

| Campo | Valor |
|---|---|
| Título en TradingView | `[GEN44 Trend] EMA 50 + smoothing` |
| Nombre corto | `GEN44 EMA 50` |
| Script | Versión 0.1.1.0, estable (archivo `GEN44_Rector_EMA50.pine`) |
| Probada en TradingView | Sí (Antonio, 22/11/2026) |
| Validada en conector | No (límite de cuota diaria) |

---

## Cómo se añade

1. Abre el gráfico del activo, en el marco con el que operes.
2. En Indicadores, busca el título o el nombre corto y añádelo.
3. Se dibuja sobre el precio: una línea azul con la EMA y, si activas el suavizado, una línea amarilla y, si eliges «SMA + Bandas de Bollinger», dos bandas verdes con relleno.

## Ajustes

Siete ajustes: tres sin grupo, tres en el grupo «Suavizado» y una ficha de solo lectura. Todos los ajustes llevan explicación al pasar el ratón (tooltip), salvo la ficha. El «Desplazamiento» y los tres ajustes de «Suavizado» no aparecen en la línea de estado del indicador, pero se cambian igual desde los ajustes.

### Sin grupo

| Ajuste | Por defecto | Qué hace | Cuándo tocarlo |
|---|---|---|---|
| Longitud | 50 | Velas con las que se calcula la EMA (mínimo 1). Menos velas, más rápida; más velas, más lenta | `[Aportado]`: 50 no tiene fuente confirmada. Cambiarlo da otra EMA |
| Fuente | cierre | Precio sobre el que se calcula la EMA | Solo si quieres la EMA sobre otra serie |
| Desplazamiento | 0 | Desplaza la línea de la EMA esas velas, de −500 a 500. No mueve la media de suavizado ni las bandas | Rara vez: viene de la plantilla de TradingView. Dirección (positivo = derecha): sin comprobar en pantalla |

### Suavizado

| Ajuste | Por defecto | Qué hace | Cuándo tocarlo |
|---|---|---|---|
| Tipo | Ninguna | Media que se calcula sobre la propia EMA: Ninguna, SMA, SMA + Bandas de Bollinger, EMA, SMMA (RMA), WMA o VWMA. Con «Ninguna» no se dibuja nada más | Solo si quieres suavizar la EMA o ver bandas a su alrededor |
| Longitud | 14 | Velas de la media de suavizado y, con «SMA + Bandas de Bollinger», de la desviación típica de las bandas. Con Tipo «Ninguna» se atenúa y se ignora | Solo con Tipo distinto de «Ninguna» |
| Multiplicador de bandas | 2,0 | Multiplicador de la desviación típica de la EMA, de 0,001 a 50, de 0,5 en 0,5. Solo con «SMA + Bandas de Bollinger»; con otro tipo se atenúa y se ignora. Más multiplicador, bandas más separadas | Solo con «SMA + Bandas de Bollinger» |

La «Ficha» es un resumen de solo lectura; no se puede cambiar.

## Equivalencia en tiempo

Son velas, no días. Con 5 sesiones por semana:

| Ajuste | Valor | En diario | En semanal |
|---|---|---|---|
| Longitud (EMA) | 50 | 50 sesiones, 10 semanas (algo más de 2 meses) | 50 semanas, casi 1 año |
| Longitud (Suavizado) | 14 | 14 sesiones, casi 3 semanas | 14 semanas, unos 3 meses |

## Colores y marcas

| Elemento | Color o forma | Qué indica |
|---|---|---|
| EMA | Línea azul | La EMA de 50 velas del cierre |
| Media sobre la EMA | Línea amarilla | La media de suavizado calculada sobre la EMA. Solo con Tipo distinto de «Ninguna» |
| Banda superior y Banda inferior | Líneas verdes | La media de suavizado más y menos la desviación típica de la EMA por el multiplicador. Solo con «SMA + Bandas de Bollinger» |
| Relleno de bandas | Relleno verde, transparencia 90 % | El espacio entre las dos bandas. Solo con «SMA + Bandas de Bollinger» |

Los colores van fijos en el código: no hay ajustes de color. No hay más marcas.

## Alertas

Este script no define alertas.

## Marcos temporales

El del gráfico: el script no fuerza ninguno, y las medias cuentan velas del marco en que se carga (ver «Equivalencia en tiempo»).

---

## Control de cambios

| Versión | Fecha | Cambios |
|---|---|---|
| 0.1.0.0 | 2026-11-21 | Creación para el código legado 0.1.0.0 (nombre GEN72, interfaz en inglés). Archivada |
| 0.2.0.0 | 2026-11-22 | Renombrada a GEN44. Describe el código 0.1.1.0: interfaz en castellano, título nuevo, tooltips, ficha |
| 0.3.0.0 | 2026-11-22 | Script declarado estable y probado en TradingView por Antonio; campos «Probada» y «Validada en conector»; pasa a la carpeta del repo en Drive |
