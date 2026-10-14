# Documentación del Proceso de Limpieza y Análisis de Datos

Este documento resume de forma breve las decisiones de limpieza, normalización y análisis exploratorio tomadas en el notebook de ventas.

---

## 1. Tratamiento de Valores Nulos (NaN)
Se identificaron inicialmente 3 registros con nulos en un dataset de 1503 filas:
- **Eliminación selectiva:** Se eliminaron las filas con índices `1500` y `1502` debido a que presentaban múltiples datos faltantes críticos que comprometían la integridad del registro.
- **Imputación:** Se rellenaron los valores nulos en las columnas de `descuento` y `descuento_porcentaje` con `0`, asumiendo que la ausencia de datos indica que no se aplicó ningún beneficio en esa venta.

## 2. Normalización y Conversión de Tipos de Datos
- **Columnas Monetarias:** Se limpiaron y normalizaron las columnas `precio_unitario`, `subtotal`, `descuento` y `TOTAL` eliminando los símbolos de moneda (`$`), los puntos de miles y reemplazando comas por puntos para transformarlas de texto (`object`) a decimales (`float64`).
- **Porcentajes:** La columna `descuento_porcentaje` se transformó de formato string (ej: `10%`) a un valor numérico decimal (ej: `0.10`).

## 3. Identificación de Outliers (Valores Atípicos)
Mediante el rango intercuartílico (IQR) se detectaron dos anomalías legítimas que decidimos preservar para no perder el historial real de ingresos:
- **Cantidad:** Un pedido mayorista de **500 unidades** realizado por la *Empresa Tech SRL*.
- **Demora de entrega:** Un envío de **85 días** en la provincia de Mendoza (posible incidente logístico).

## 4. Agrupaciones y Análisis Final
Se procesaron agrupaciones para entender el rendimiento del negocio:
- **Ventas por Marca:** Identifica cuáles son los fabricantes más demandados (ej. AMD, Intel, NVIDIA).
- **Ventas por Categoría:** Clasifica el volumen de ventas por tipo de producto, destacando los Procesadores y Tarjetas de Video como líderes de volumen.
- **Total por Provincia:** Sumariza la facturación total (`TOTAL`) por región geográfica, evidenciando que Buenos Aires lidera ampliamente los ingresos de la tienda.
