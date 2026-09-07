# RappiPlus: análisis de datos para decisiones de negocio

Proyecto final de análisis de datos enfocado en evaluar el desempeño de RappiPlus mediante Python, SQL y Power BI.

## Objetivo

Transformar datos crudos en insights accionables para responder preguntas clave de negocio:

- ¿Podemos confiar en los datos?
- ¿El negocio es rentable?
- ¿En qué etapa se pierden los usuarios?
- ¿Los usuarios regresan?
- ¿La nueva interfaz de checkout genera un impacto?
- ¿Cómo comunicar los resultados a stakeholders?

## Herramientas utilizadas

- Python
- Pandas
- Matplotlib
- SciPy
- SQL y SQLAlchemy
- Power BI

## Proceso de análisis

### 1. Calidad de datos

Se validaron fechas, valores numéricos, duplicados, consistencia de montos y variables categóricas.

Durante la limpieza se identificaron y eliminaron:

- Registros duplicados.
- Cantidades negativas o inválidas.
- Pedidos atípicos de 10,000 y 20,000 unidades que distorsionaban los KPIs.
- Registros sin costo disponible para el análisis de rentabilidad.

### 2. Rentabilidad del negocio

Se integraron pedidos, catálogo de productos y gasto de marketing para calcular los principales indicadores.

| KPI | Resultado |
|---|---:|
| Revenue total | \$9.61 millones |
| Costo total | \$3.83 millones |
| Gasto total de marketing | \$2.87 millones |
| Profit total | \$2.91 millones |
| Margen de profit | 30.3% |

El producto con más unidades vendidas fue **Vacuum-Pro-Black**, con 6,284 unidades.

### 3. Funnel de conversión

Se construyó un funnel secuencial basado en usuarios únicos y el orden temporal de sus eventos.

| Etapa | Usuarios | Conversión acumulada |
|---|---:|---:|
| First visit | 7,796 | 100.00% |
| Select item | 6,728 | 86.30% |
| Add to cart | 4,983 | 63.92% |
| Begin checkout | 2,663 | 34.16% |
| Add payment info | 919 | 11.79% |
| Purchase | 258 | 3.31% |

Los principales puntos de abandono se encuentran entre `add_to_cart` y `begin_checkout`, así como en la transición final de pago a compra.

### 4. Retención por cohortes

Se analizaron cohortes mensuales según la fecha de registro y se calculó la actividad de cada usuario durante las primeras tres semanas.

La retención se mantuvo aproximadamente entre 40% y 43% durante las primeras semanas posteriores al registro.

### 5. Experimento A/B

Se evaluó el impacto de una nueva interfaz de checkout sobre la tasa de conversión.

- Grupo control: 15.69%
- Grupo tratamiento: 16.29%
- p-value: 0.4319
- Nivel de significancia: 0.05

No se encontró evidencia estadísticamente significativa para concluir que la nueva interfaz mejore la conversión.

### 6. Dashboard en Power BI

El dashboard incluye:

- Overview ejecutivo con KPIs de revenue, profit, marketing, ticket promedio y productos promedio.
- Tendencia mensual de revenue y profit.
- Análisis por categoría, producto y canal de marketing.
- Vista de detalle con drill-through por producto.

## Recomendaciones

1. Investigar la experiencia de checkout y pago, especialmente en las etapas con mayor abandono.
2. Implementar estrategias de recuperación para usuarios que agregan productos al carrito sin iniciar checkout.
3. Mantener inventario y promoción de los productos con mayor demanda.
4. No implementar la nueva interfaz de checkout basándose únicamente en el experimento actual.
5. Incorporar validaciones automáticas para evitar duplicados y cantidades atípicas.
6. Medir conversiones e ingresos por canal antes de redistribuir el presupuesto de marketing.

## Estructura sugerida del repositorio

```text
├── notebooks/
│   └── rappiplus_bussines_analysis.ipynb
├── data/
│   ├── orders_clean.csv
│   ├── catalog_clean.csv
│   └── marketing_clean.csv
├── dashboard/
│   └── rappiplus_dashboard.pbix
├── images/
│   └── dashboard_preview.png
└── README.md
```

> Nota: no se incluyen credenciales de bases de datos en este repositorio.
