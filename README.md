# ☕ Dashboard Ejecutivo Power BI — Urban Coffee

![Power BI](https://img.shields.io/badge/Power%20BI-Desktop-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-Medidas%20calculadas-0078D4?style=for-the-badge)
![Estado](https://img.shields.io/badge/Estado-Completado-4CAF50?style=for-the-badge)
![Tipo](https://img.shields.io/badge/Práctica-Visualización%20de%20Datos-FF6B6B?style=for-the-badge)

> **Ejercicio Práctico — Visualización de Datos con Power BI (ADGG10)**  
> Caso de negocio: cadena de cafeterías ficticia **Urban Coffee**

---

## 📥 Descarga

[![Descargar .pbix](https://img.shields.io/badge/⬇️%20Descargar%20Dashboard-Power%20BI%20(.pbix)-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](https://github.com/migueljerico/powerbi-dashboard-urban-coffee/raw/main/Ejercicio_Practico_Visualizacion_Power_BI_Miguel_Jerico.pbix)

[![Ver Release v1.0](https://img.shields.io/badge/📦%20Release-v1.0-0078D4?style=for-the-badge&logo=github&logoColor=white)](https://github.com/migueljerico/powerbi-dashboard-urban-coffee/releases/tag/v1.0)

> Requiere **Microsoft Power BI Desktop** (descarga gratuita en [powerbi.microsoft.com](https://powerbi.microsoft.com/es-es/desktop/))

---

## 📋 Descripción del Proyecto

Dashboard ejecutivo desarrollado en **Microsoft Power BI Desktop** para analizar el rendimiento comercial de una cadena de cafeterías con locales en Madrid, Barcelona, Valencia y Sevilla.

El objetivo principal es facilitar la **toma de decisiones estratégicas** mediante KPIs visuales e interactivos, con versión optimizada para escritorio y dispositivos móviles.

---

## 📁 Estructura del Repositorio

```
powerbi-dashboard-urban-coffee/
│
├── 📊 Ejercicio_Practico_Visualizacion_Power_BI_Miguel_Jerico.pbix
│       └── Archivo Power BI Desktop con el dashboard completo
│
├── 📁 docs/
│       └── 📄 Caso_Practico_Power_BI_Miguel_Jerico.pdf
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
| Tendencia temporal | Gráfico de líneas | Evolución de ventas mensuales |
| Comparativa ciudades | Barras horizontales | Ventas totales por ciudad |
| Distribución categorías | Gráfico de anillos | % de ventas por categoría |
| Detalle operativo | Tabla | Registros individuales con totales |

---

## 🎨 Paleta de Colores Corporativa

| Elemento | Color | HEX |
|----------|-------|-----|
| Barra de título | Marrón oscuro | `#3B1F0F` |
| Fondo del lienzo | Beige cálido | `#F6F2EC` |
| KPIs y números | Marrón medio | `#5B2E0F` |
| Barras del gráfico | Marrón caña | `#8B4A12` |
| Línea temporal | Ámbar | `#7A4315` |
| Categoría Café | Marrón oscuro | `#3B1F0F` |
| Categoría Té | Verde tierra | `#4E7D4A` |
| Categoría Repostería | Ámbar | `#7A4315` |
| Categoría Snacks | Dorado | `#9B7400` |

---

## 🔍 Interactividad

- **3 segmentadores** con filtrado cruzado: Ciudad · Categoría · Fecha (rango)
- Todos los gráficos se interconectan al seleccionar cualquier filtro
- Tabla ordenable por cualquier columna (por defecto: Fecha descendente)

---

## 📱 Versión Móvil

Vista optimizada mediante **Vista → Diseño para móviles** con KPIs en parte superior, filtros compactos y visualizaciones priorizadas.

---

## 📈 Resultados del Dashboard

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

## 🧰 Tecnologías utilizadas

| Herramienta | Uso |
|---|---|
| **Microsoft Power BI Desktop** | Creación del dashboard ejecutivo |
| **DAX** | Medidas calculadas y KPIs |
| **Power Query** | Transformación y limpieza de datos |
| **Excel** | Fuente de datos (UrbanCoffee_Dataset_PowerBI.xlsx) |

---

## 📚 Contexto formativo

Este ejercicio forma parte del programa de formación en **Análisis de Datos**, dentro del módulo **ADGG10 — Visualización de Datos con Power BI**. El objetivo es desarrollar competencias en modelado de datos (modelo estrella), escritura de medidas DAX y diseño de dashboards ejecutivos interactivos con versión móvil.

**Ejercicio relacionado:** [Dashboard en Data Studio — Urban Coffee](https://github.com/migueljerico/data-studio-dashboard-urban-coffee) — mismo caso de negocio, herramienta Google BI.

---

<p align="center">
  <sub>Desarrollado por <a href="https://github.com/migueljerico">@migueljerico</a> · 2026</sub>
</p>
