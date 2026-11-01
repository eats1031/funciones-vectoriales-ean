# Generador de Funciones Vectoriales y Análisis de Dominio

Proyecto de **Cálculo Multivariado** · **Universidad EAN** · Bogotá D.C., 2026

**Integrantes:** Julian Ladino, Karen Ovalle y Edwin Tejada

**App en línea:** https://eats1031.github.io/funciones-vectoriales-ean/  
**Código fuente:** https://github.com/eats1031/funciones-vectoriales-ean

Aplicación web que permite escribir una función vectorial
**r(t) = ⟨x(t), y(t), z(t)⟩**, calcular automáticamente su dominio y verla graficada en 2D o 3D.

---

## ¿Qué hace?

| Apartado | Descripción |
|---|---|
| **Entradas** | Selector ℝ² / ℝ³, componentes x(t), y(t), z(t), intervalo del parámetro con extremos abiertos `( )` o cerrados `[ ]` y 20 ejemplos rápidos. |
| **1 · Función vectorial** | Muestra r(t) en notación formal (vector, forma i/j/k y ecuaciones paramétricas) y una ficha con punto inicial, punto final y si la curva es cerrada. |
| **2 · Dominio paso a paso** | Detecta raíces de índice par, logaritmos, divisiones, tan/sec/cot/csc y funciones inversas; explica la regla de cada restricción, calcula el dominio de cada componente y lo intersecta con el intervalo. Resultado en notación de intervalos y de conjuntos. |
| **3 · Gráfica interactiva** | Plotly.js: rotación, zoom, flechas de orientación, extremos incluidos ● y excluidos ○, vector posición y vector tangente en un punto t₀ con animación. |

### Cómo se calcula el dominio

```
Dom(r) = Dom(x) ∩ Dom(y) ∩ Dom(z) ∩ I
```

- Expresiones racionales → raíces exactas de polinomios.
- sen/cos(at + b) → familias periódicas exactas (p. ej. t ≠ π/2 + kπ, k ∈ ℤ).
- Otras expresiones → análisis numérico con reconocimiento de constantes exactas (π/2, √2, ln 2…). Si un valor solo puede aproximarse, la app lo indica.

---

## Ejecutar localmente

No requiere instalación ni servidor.

1. Descarga o clona este repositorio:
   ```bash
   git clone https://github.com/eats1031/funciones-vectoriales-ean.git
   ```
2. Abre `index.html` con doble clic (Chrome, Edge, Firefox o Safari).

> Necesita conexión a internet al abrirse, porque las librerías se cargan desde CDN.

## Despliegue web (GitHub Pages)

1. En el repositorio: **Settings → Pages**.
2. En *Build and deployment*: **Source = Deploy from a branch**, **Branch = `main`**, carpeta **`/ (root)`** → **Save**.
3. En uno o dos minutos la app queda publicada en:
   `https://eats1031.github.io/funciones-vectoriales-ean/`

---

## Tecnologías

- HTML, CSS y JavaScript en un solo archivo (`index.html`), sin compilación.
- [Plotly.js 2.35.2](https://plotly.com/javascript/) para las gráficas 2D/3D.
- [math.js 15.2.0](https://mathjs.org/) para interpretar las fórmulas.
- [KaTeX 0.16.22](https://katex.org/) para la notación matemática.

## Arquitectura del código

El script está organizado por capas (Clean Architecture en un solo archivo):

1. **Núcleo:** utilidades numéricas, reconocimiento de constantes, álgebra de intervalos y polinomios.
2. **Expresiones:** parser → AST canónico → compilador con semántica real y generador de LaTeX.
3. **Análisis:** extracción de restricciones y resolución exacta, periódica o numérica.
4. **Aplicación:** casos de uso (construir el modelo, analizar el dominio, muestrear la curva).
5. **Presentación:** portada, vistas KaTeX, gráfica Plotly y controlador de la interfaz.

## Sintaxis admitida

| Escribe | Significa |
|---|---|
| `2t`, `t sin(t)` | Multiplicación implícita |
| `pi`, `e` | π y e |
| `sin`, `sen`, `cos`, `tan`, `sec`, `csc`, `cot` | Trigonométricas |
| `arcsin`, `arccos`, `arctan` | Trigonométricas inversas |
| `ln(t)` · `log(t)` · `log(t, b)` | Logaritmo natural · base 10 · base b |
| `sqrt(t)`, `cbrt(t)`, `t^(1/3)` | Raíces (las de índice impar admiten t < 0) |
| `exp(t)`, `abs(t)` o `|t|` | Exponencial y valor absoluto |
