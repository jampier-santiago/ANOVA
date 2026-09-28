# Análisis Estadístico de Siniestralidad por Línea de Negocio (Caso Quan)

## Propósito

Este proyecto aplica pruebas estadísticas (paramétricas y no paramétricas) para determinar si existen
diferencias significativas en el monto de siniestralidad (`monto_siniestro`) entre las cuatro líneas de
negocio de Quan (movilidad, mascotas, salud, hogar), y entre dos tipos de reclamo dentro de movilidad
(daños propios vs. responsabilidad civil). El objetivo es aportar insumos para decisiones de reservas
técnicas y priorización operativa por línea de negocio.

## Estructura del proyecto

```
data/siniestros_quan_simulado.csv       # dataset simulado
notebooks/analisis_siniestralidad_quan.ipynb
README.md
.gitignore
```

## Datos

`data/siniestros_quan_simulado.csv` — **conjunto de datos simulado** (2000 registros), generado con la
estructura organizacional real de Quan pero calibrado a benchmarks públicos reales de severidad de
siniestros por ramo (no son registros reales de producción, por confidencialidad). Variables:
`linea_negocio`, `tipo_reclamo`, `monto_siniestro`, `antiguedad_poliza_meses`, `mes_siniestro`.
Las fuentes de calibración utilizadas para simular los montos se documentan en el informe académico.

## Librerías utilizadas

- pandas, numpy — manipulación y simulación de datos
- matplotlib, seaborn — visualización
- scipy.stats — pruebas de normalidad (Shapiro-Wilk), homogeneidad de varianzas (Levene), t de Welch,
  U de Mann-Whitney, Kruskal-Wallis, correlación de Pearson/Spearman
- statsmodels — ANOVA de un factor y prueba post-hoc de Tukey HSD

## Cómo ejecutar

Todos los comandos se ejecutan desde la raíz del proyecto.

1. Crear el entorno virtual e instalar dependencias:
   ```bash
   python3 -m venv .venv
   source .venv/bin/activate      # Windows: .venv\Scripts\activate
   pip install pandas numpy matplotlib seaborn scipy statsmodels jupyter
   ```
2. Ejecutar el notebook completo desde la terminal:
   ```bash
   jupyter nbconvert --to notebook --execute --inplace notebooks/analisis_siniestralidad_quan.ipynb
   ```
   O abrirlo en Jupyter (`jupyter notebook notebooks/analisis_siniestralidad_quan.ipynb`) y ejecutar
   todas las celdas en orden (Kernel → Restart & Run All).

## Estructura del notebook

1. Carga y preparación de datos
2. Análisis exploratorio (histograma, boxplots por línea y tipo de reclamo, dispersión, gráfico de área)
3. Verificación de supuestos (normalidad, homogeneidad de varianzas)
4. Comparación de dos grupos: tipo de reclamo en movilidad (t de Welch y U de Mann-Whitney)
5. Comparación de múltiples grupos: línea de negocio (ANOVA y Kruskal-Wallis, con post-hoc Tukey)
6. Síntesis de resultados
