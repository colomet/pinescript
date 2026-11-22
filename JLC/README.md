# JLC

Scripts que aplican reglas de José Luis Cava. Cada uno cita en su cabecera el capítulo y la página de donde sale la regla.

Las normas de nombres, versiones y licencia están en el [README principal](../README.md).

## Scripts

| Script | Versión | Qué hace | Guías |
|---|---|---|---|
| [JLC11_Sentimiento_VIX](JLC11_Sentimiento_VIX/) | 0.3.0.0 | VIX frente a su media de 10 sesiones, con bandas del −5 %, +5 % y +12 %. | [uso](JLC11_Sentimiento_VIX/JLC11_Sentimiento_VIX_user-guide.md) · [técnica](JLC11_Sentimiento_VIX/JLC11_Sentimiento_VIX_technical-guide.md) |
| [JLC12_Sentimiento_PutCall](JLC12_Sentimiento_PutCall/) | 0.3.0.0 | Ratio put/call del CBOE con bandas de Bollinger (media de 20 sesiones, desviación 2) para señalar extremos de miedo. | [uso](JLC12_Sentimiento_PutCall/JLC12_Sentimiento_PutCall_user-guide.md) · [técnica](JLC12_Sentimiento_PutCall/JLC12_Sentimiento_PutCall_technical-guide.md) |
| [JLC31_Comparativa_MurphySMAMACD](JLC31_Comparativa_MurphySMAMACD/) | 0.3.0.0 | Medias de 10 y 40 semanas y MACD semanal sobre el ratio de dos valores. | [uso](JLC31_Comparativa_MurphySMAMACD/JLC31_Comparativa_MurphySMAMACD_user-guide.md) · [técnica](JLC31_Comparativa_MurphySMAMACD/JLC31_Comparativa_MurphySMAMACD_technical-guide.md) |
| [JLC32_Comparativa_OBVLiderazgo](JLC32_Comparativa_OBVLiderazgo/) | 0.3.0.0 | OBV (volumen acumulado) de un valor, para ver si el volumen confirma al precio. | [uso](JLC32_Comparativa_OBVLiderazgo/JLC32_Comparativa_OBVLiderazgo_user-guide.md) · [técnica](JLC32_Comparativa_OBVLiderazgo/JLC32_Comparativa_OBVLiderazgo_technical-guide.md) |
| [JLC41_Rector_Semaforo](JLC41_Rector_Semaforo/) | 0.3.0.0 | Semáforo de tendencia con el MACD mensual, el MACD semanal y el estocástico semanal. | [uso](JLC41_Rector_Semaforo/JLC41_Rector_Semaforo_user-guide.md) · [técnica](JLC41_Rector_Semaforo/JLC41_Rector_Semaforo_technical-guide.md) |
| [JLC42_Rector_Tablero](JLC42_Rector_Tablero/) | 0.3.0.0 | Tablero con los indicadores del método en los tres marcos (mensual, semanal y diario), sin dibujar nada sobre el precio. | [uso](JLC42_Rector_Tablero/JLC42_Rector_Tablero_user-guide.md) · [técnica](JLC42_Rector_Tablero/JLC42_Rector_Tablero_technical-guide.md) |
| [JLC51_Regimen_ADXDI](JLC51_Regimen_ADXDI/) | 0.3.0.0 | ADX y DI de 14 períodos: fuerza de la tendencia (no su dirección), con los niveles 40, 30 y 20. | [uso](JLC51_Regimen_ADXDI/JLC51_Regimen_ADXDI_user-guide.md) · [técnica](JLC51_Regimen_ADXDI/JLC51_Regimen_ADXDI_technical-guide.md) |
| [JLC61_Diagnostico_PrecioEMA20](JLC61_Diagnostico_PrecioEMA20/) | 0.3.0.0 | Media exponencial de 20 y máximos y mínimos aislados sobre el gráfico de precio. | [uso](JLC61_Diagnostico_PrecioEMA20/JLC61_Diagnostico_PrecioEMA20_user-guide.md) · [técnica](JLC61_Diagnostico_PrecioEMA20/JLC61_Diagnostico_PrecioEMA20_technical-guide.md) |
| [JLC62_Diagnostico_Estocastico](JLC62_Diagnostico_Estocastico/) | 0.3.0.0 | Estocástico de 14 períodos, con las líneas %K y %D y los niveles 80, 60, 40 y 20. | [uso](JLC62_Diagnostico_Estocastico/JLC62_Diagnostico_Estocastico_user-guide.md) · [técnica](JLC62_Diagnostico_Estocastico/JLC62_Diagnostico_Estocastico_technical-guide.md) |
| [JLC63_Diagnostico_CCI](JLC63_Diagnostico_CCI/) | 0.3.0.0 | CCI de 14 períodos, con umbral de ±50 para entrar y 0 para cancelar. | [uso](JLC63_Diagnostico_CCI/JLC63_Diagnostico_CCI_user-guide.md) · [técnica](JLC63_Diagnostico_CCI/JLC63_Diagnostico_CCI_technical-guide.md) |
| [JLC71_Gestion_Stops](JLC71_Gestion_Stops/) | 0.3.0.0 | Tres reglas de salida: stop bajo el soporte, stop bajo la media de 20 y cierre por invalidación del MACD. | [uso](JLC71_Gestion_Stops/JLC71_Gestion_Stops_user-guide.md) · [técnica](JLC71_Gestion_Stops/JLC71_Gestion_Stops_technical-guide.md) |
| [JLC81_Pack_Precio](JLC81_Pack_Precio/) | 0.3.0.0 | Medias, medias desplazadas y pivotes sobre el precio, en un solo indicador. | [uso](JLC81_Pack_Precio/JLC81_Pack_Precio_user-guide.md) · [técnica](JLC81_Pack_Precio/JLC81_Pack_Precio_technical-guide.md) |
| [JLC82_Pack_Momento](JLC82_Pack_Momento/) | 0.3.0.0 | Estocástico, ADX/DI y CCI en un solo panel. | [uso](JLC82_Pack_Momento/JLC82_Pack_Momento_user-guide.md) · [técnica](JLC82_Pack_Momento/JLC82_Pack_Momento_technical-guide.md) |
| [JLC91_Backtest_Sistemas](JLC91_Backtest_Sistemas/) | 0.3.0.0 | Backtest (strategy) de dos sistemas del libro: EMA 55 con MACD diario y retroceso a la EMA 20 con ADX. | [uso](JLC91_Backtest_Sistemas/JLC91_Backtest_Sistemas_user-guide.md) · [técnica](JLC91_Backtest_Sistemas/JLC91_Backtest_Sistemas_technical-guide.md) |

La versión vigente de cada script está en la cabecera del código y su historial, en el [CHANGELOG](../CHANGELOG.md).

## Estado de pruebas

Los 14 scripts se han probado en TradingView y funcionan sin errores de código. Falta verificar su funcionamiento (que las señales sean las que dice la regla); hasta entonces están en fase de pruebas.

## Qué es de la regla y qué no

Lo que no viene de la regla del libro lleva una marca en el código. La lista de marcas está en el [README principal](../README.md), en la sección «Marcas que aparecen en el código».

## Qué falta

- Guías: las de uso y las técnicas están escritas para los 14 scripts, pero las de algunos pueden no reflejar todavía la última versión del código. [Por confirmar]
- Verificación funcional de las señales, pendiente.
