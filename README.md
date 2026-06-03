# ☕ Dashboard Ejecutivo Power BI — Urban Coffee

![Power BI](https://img.shields.io/badge/Power%20BI-Desktop-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-Medidas%20calculadas-0078D4?style=for-the-badge)
![Estado](https://img.shields.io/badge/Estado-Completado-4CAF50?style=for-the-badge)

> **Ejercicio Práctico — ADGG10: Visualización de Datos con Power BI**  
> Caso de negocio: cadena de cafeterías ficticia **Urban Coffee**

---

## 📋 Descripción del Proyecto

Dashboard ejecutivo desarrollado en **Microsoft Power BI Desktop** para analizar el rendimiento comercial de una cadena de cafeterías con locales en Madrid, Barcelona, Valencia y Sevilla.

El objetivo principal es facilitar la **toma de decisiones estratégicas** mediante KPIs visuales e interactivos, con versión optimizada para escritorio y dispositivos móviles.

---

## 📁 Estructura del Repositorio

```
powerbi-dashboard-urban-coffee/
│
├── 📊 Ejercicio_Práctico_Visualización_Power_BI_Miguel_Jericó.pbix
│       └── Archivo Power BI Desktop con el dashboard completo
│
├── 📄 docs/
│       └── Caso_Practico_Power_BI_Miguel_Jericó.pdf
│               └── Documentación técnica detallada paso a paso
│
└── 📖 README.md
```

---

## 🗂️ Modelo de Datos

El modelo estrella contiene **3 tablas relacionadas** con relaciones Muchos a Uno (*:1):

| Tabla | Campos principales | Registros |
|-------|-------------------|-----------|
| **Ventas** | ID_Venta, Fecha, ID_Producto, ID_Tienda, Cantidad, Precio_Unitario, Total_Venta | 150 |
| **Productos** | ID_Producto, Producto, Categoría (Café/Té/Repostería/Snacks), Coste | 10 |
| **Tiendas** | ID_Tienda, Ciudad, Tipo_Tienda (Centro Comercial/Calle/Oficina) | 4 |

**Relaciones:**
- `Ventas[ID_Producto]` → `Productos[ID_Producto]`
- `Ventas[ID_Tienda]` → `Tiendas[ID_Tienda]`

---

## 📐 Medidas DAX Implementadas

```dax
-- KPI 1: Ventas Totales
Ventas Totales = SUM(Ventas[Total_Venta])

-- KPI 2: Número de Pedidos
Pedidos = COUNT(Ventas[ID_Venta])

-- KPI 3: Ticket Medio
Ticket Medio = DIVIDE([Ventas Totales], [Pedidos])

-- KPI 4: Producto Más Vendido
Producto Top =
TOPN(
    1,
    VALUES(Productos[Producto]),
    [Ventas Totales]
)

-- KPI 5: Fecha del Último Dato (sin filtros)
FechaUltimoDato =
VAR _max = CALCULATE( MAX('Ventas'[Fecha]), REMOVEFILTERS() )
RETURN
IF(
    ISBLANK(_max),
    "Sin datos",
    "📅 Fecha del último dato: " & FORMAT(_max, "dd/MM/yyyy")
)
```

---

## 📊 Visualizaciones del Dashboard

| Visual | Tipo | Objetivo |
|--------|------|----------|
| 4 Tarjetas KPI | Tarjeta | Ventas Totales · Pedidos · Ticket Medio · Producto Top |
| Tendencia temporal | Gráfico de líneas | Evolución de ventas mensuales (ene–jun 2025) |
| Comparativa ciudades | Barras horizontales | Ventas totales por ciudad |
| Distribución categorías | Gráfico de anillos | % de ventas por categoría (Café/Té/Repostería/Snacks) |
| Detalle operativo | Tabla | Registros individuales de ventas con totales |

---

## 🎨 Paleta de Colores Corporativa

| Elemento | Color | HEX |
|----------|-------|-----|
| Barra de título | Marrón oscuro | `#3B1F0F` |
| Fondo del lienzo | Beige cálido | `#F6F2EC` |
| KPIs y números | Marrón medio | `#5B2E0F` |
| Barras del gráfico | Marrón caña | `#8B4A12` |
| Línea temporal | Ámbar | `#7A4315` |
| Categoría Café (anillo) | Marrón oscuro | `#3B1F0F` |
| Categoría Té (anillo) | Verde tierra | `#4E7D4A` |
| Categoría Repostería | Ámbar | `#7A4315` |
| Categoría Snacks | Dorado | `#9B7400` |

---

## 🔍 Interactividad

- **3 segmentadores** con filtrado cruzado: Ciudad · Categoría · Fecha (rango)
- Todos los gráficos se interconectan al seleccionar cualquier filtro
- Tabla ordenable por cualquier columna (por defecto: Fecha descendente)

---

## 📱 Versión Móvil

Vista optimizada mediante **Vista → Diseño para móviles** con:
- KPIs visibles en la parte superior
- Filtros en modo selección múltiple compacto
- Gráfico de barras + gráfico de anillos priorizados
- Textos y etiquetas reducidos al mínimo

---

## 📈 Resultados del Dashboard (datos de muestra)

| KPI | Valor |
|-----|-------|
| Ventas Totales | **1.736,90 €** |
| Número de Pedidos | **150** |
| Ticket Medio | **11,58 €** |
| Producto Top | **Sandwich** |
| Ciudad líder | **Barcelona (478,50 €)** |
| Categoría líder | **Café (44,05%)** |
| Período de datos | **Ene 2025 – Jun 2025** |

---

## 🛠️ Tecnologías Utilizadas

- **Microsoft Power BI Desktop**
- **DAX** (Data Analysis Expressions)
- **Power Query** (transformación de datos)
- **Excel** (fuente de datos: UrbanCoffee_Dataset_PowerBI.xlsx)

---

## 👤 Autor

**Miguel Jericó**  
Analista de Datos en formación | Ex-Supervisor de Operaciones  
📚 Programa de transición profesional hacia Data Analytics

---

*Proyecto realizado como ejercicio práctico del curso ADGG10 – Visualización de Datos con Power BI.*
