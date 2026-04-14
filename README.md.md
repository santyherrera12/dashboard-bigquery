# Dashboard Analítico — Ventas de Videojuegos 🎮

Dashboard ejecutivo construido con **Google BigQuery + Power BI** que analiza ventas globales de videojuegos usando SQL analítico y visualizaciones interactivas.

---

## ¿Qué hace este proyecto?

Responde preguntas clave de negocio sobre la industria de videojuegos:

- ¿Cuáles son los juegos más vendidos de la historia?
- ¿Qué género domina el mercado global?
- ¿Qué publisher lidera en ventas totales?
- ¿Cómo varían las preferencias por región (NA, EU, Japón)?

---

## Stack tecnológico

| Herramienta | Uso |
|-------------|-----|
| Google BigQuery | Almacenamiento y consulta SQL en la nube |
| SQL | Queries analíticas (SUM, GROUP BY, ORDER BY, ROUND) |
| Power BI Desktop | Visualización y dashboard ejecutivo |
| CSV | Dataset de ventas de videojuegos |

---

## Estructura del proyecto

```
dashboard-bigquery/
├── dashboard-videogames.pbix   # Dashboard Power BI
└── vgsales.csv                 # Dataset de ventas
```

---

## Queries SQL ejecutadas en BigQuery

### Top 10 juegos más vendidos
```sql
SELECT Name, Platform, Genre, Publisher, Global_Sales
FROM `proyecto.videogames.vgsales`
ORDER BY Global_Sales DESC
LIMIT 10
```

### Ventas totales por género
```sql
SELECT 
  Genre,
  ROUND(SUM(Global_Sales), 2) AS total_ventas_millones,
  COUNT(*) AS cantidad_juegos
FROM `proyecto.videogames.vgsales`
GROUP BY Genre
ORDER BY total_ventas_millones DESC
```

### Top publishers por ventas
```sql
SELECT 
  Publisher,
  ROUND(SUM(Global_Sales), 2) AS total_ventas_millones,
  COUNT(*) AS cantidad_juegos
FROM `proyecto.videogames.vgsales`
GROUP BY Publisher
ORDER BY total_ventas_millones DESC
LIMIT 10
```

### Ventas por región
```sql
SELECT 
  Genre,
  ROUND(SUM(NA_Sales), 2) AS ventas_norteamerica,
  ROUND(SUM(EU_Sales), 2) AS ventas_europa,
  ROUND(SUM(JP_Sales), 2) AS ventas_japon
FROM `proyecto.videogames.vgsales`
GROUP BY Genre
ORDER BY ventas_norteamerica DESC
```

---

## Dashboard — Visualizaciones

El dashboard en Power BI incluye:

- **KPI** — Total ventas globales (949.79M) y total de juegos (50)
- **Barras horizontales** — Top 10 juegos más vendidos
- **Dona** — Distribución de ventas por género
- **Barras verticales** — Ventas por publisher

---

## Insights clave

- **Nintendo** domina con 648M en ventas — casi 8x más que el segundo publisher
- **Sports** es el género más vendido con 189M (20% del total)
- **Shooter** es muy popular en NA (79M) pero casi inexistente en Japón (1.2M)
- **Role-Playing** es el género más equilibrado entre regiones

---

## Cómo usar el dashboard

1. Descarga el archivo `dashboard-videogames.pbix`
2. Abre con **Power BI Desktop**
3. Los datos están importados — no necesitas conexión a BigQuery

---

## Autor

**Santiago Herrera Tafur**  
Ingeniero de Sistemas | Máster en Big Data  
[LinkedIn](https://www.linkedin.com/in/santiago-herrera-tafur-463887161) · [GitHub](https://github.com/santyherrera12)
