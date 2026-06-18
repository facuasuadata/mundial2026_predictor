# ⚽ Predictor de Partidos — Copa del Mundo 2026

> Modelo estadístico basado en distribución de Poisson y Rankings FIFA (junio 2026)  
> **48 selecciones clasificadas · Grupos oficiales del sorteo de diciembre 2025**

---

## 📌 Descripción

Herramienta interactiva que estima probabilidades de resultados para cualquier enfrentamiento del Mundial 2026 (USA · México · Canadá). A partir de los puntos FIFA de cada selección, el modelo calcula los goles esperados (λ) mediante una función exponencial, y aplica la distribución de Poisson para obtener la probabilidad de cada marcador posible.

---

## 🧠 Metodología

### Distribución de Poisson

$$P(X = k) = \frac{e^{-\lambda} \cdot \lambda^k}{k!}$$

Se modela la cantidad de goles de cada equipo como una variable aleatoria independiente con distribución de Poisson, donde λ representa los goles esperados.

### Cálculo de λ (goles esperados)

$$\lambda_A = 1.35 \cdot e^{\frac{pts_A - pts_B}{pts_{max}} \cdot 1.5}$$

- **Base λ = 1.35**: promedio histórico de goles en partidos de Copa del Mundo
- La diferencia de puntos FIFA entre ambas selecciones ajusta el λ de forma simétrica
- Cuanto mayor la brecha de ranking, más se amplifica la ventaja del equipo mejor rankeado

### Matriz de probabilidades

Se construye una matriz (8×8) con la probabilidad conjunta de cada marcador `i-j`, donde `i, j ∈ {0, 1, ..., 7}`. A partir de ella se calculan:

- **Victoria local**: suma de la triangular inferior
- **Empate**: suma de la diagonal principal
- **Victoria visitante**: suma de la triangular superior

---

## 📊 Outputs del modelo

Para cada partido seleccionado, el modelo genera una visualización de 4 paneles:

| Panel | Contenido |
|---|---|
| Probabilidades | Barras horizontales: % victoria A / empate / victoria B |
| Top 5 marcadores | Los 5 resultados exactos más probables |
| Distribución Poisson | Histograma de goles esperados por equipo |
| Heatmap | Mapa de calor con probabilidad de cada marcador exacto (hasta 6-6) |

---

## 🗂️ Estructura del proyecto

```
mundial2026_predictor/
│
├── mundial2026_predictor.ipynb   # Notebook principal con modelo y app interactiva
└── README.md
```

Los gráficos de cada partido se guardan automáticamente como `.png` en el directorio de trabajo al presionar el botón de cálculo.

---

## 🚀 Cómo usar

### 1. Clonar el repositorio

```bash
git clone https://github.com/facuasudata/mundial2026_predictor.git
cd mundial2026_predictor
```

### 2. Instalar dependencias

```bash
pip install numpy scipy matplotlib ipywidgets
```

### 3. Ejecutar el notebook

Abrir `mundial2026_predictor.ipynb` en Jupyter Lab o Jupyter Notebook y ejecutar todas las celdas. La app interactiva aparece en la última celda: seleccioná dos equipos y presioná **⚽ Calcular probabilidades**.

> También podés ejecutarlo directamente en Google Colab sin instalar nada:
>
[![Abrir en Colab](https://colab.research.google.com/assets/colab-badge.svg)]
https://colab.research.google.com/github/facuasuadata/mundial2026_predictor/blob/main/mundial2026_predictor.ipynb
---

## 🌍 Cobertura

48 selecciones clasificadas, organizadas en 12 grupos (A–L):

| Confederación | Selecciones |
|---|---|
| UEFA | España, Francia, Inglaterra, Portugal, Países Bajos, Bélgica, Alemania, Suiza, Austria, Noruega, Turquía, Croacia, Suecia, República Checa, Escocia, Bosnia y Herzegovina |
| CONMEBOL | Argentina, Brasil, Colombia, Uruguay, Ecuador, Paraguay |
| CONCACAF | Estados Unidos, México, Canadá, Panamá, Haití, Curazao |
| CAF | Marruecos, Senegal, Túnez, Argelia, Egipto, Costa de Marfil, RD Congo, Ghana, Cabo Verde, Sudáfrica |
| AFC | Japón, Corea del Sur, Irán, Australia, Arabia Saudita, Qatar, Uzbekistán, Irak, Jordania |
| OFC | Nueva Zelanda |

Rankings y puntos FIFA actualizados al **11 de junio de 2026**.

---

## 🛠️ Tecnologías

![Python](https://img.shields.io/badge/Python-3.10-blue?logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-1.x-013243?logo=numpy)
![SciPy](https://img.shields.io/badge/SciPy-1.x-8CAAE6?logo=scipy)
![Matplotlib](https://img.shields.io/badge/Matplotlib-3.x-11557c)
![ipywidgets](https://img.shields.io/badge/ipywidgets-interactivo-green)

---

## ⚠️ Limitaciones del modelo

- El modelo es puramente estadístico y no considera lesiones, sanciones, condiciones climáticas ni historial head-to-head entre selecciones.
- Asume independencia entre los goles de ambos equipos (simplificación estándar del modelo de Poisson aplicado al fútbol).
- Los rankings FIFA tienen limitaciones propias para reflejar el rendimiento real en competencias de eliminación directa.

---

## 👤 Autor

**facuasudata** · Proyecto de portfolio de Data Science  
[GitHub](https://github.com/facuasudata)

---

*Rankings FIFA/Coca-Cola Men's World Ranking — 11 de junio de 2026 · Grupos oficiales del sorteo de diciembre 2025*
