# ICR-Dengue: Índice Compuesto de Riesgo de Mortalidad por Dengue

Aplicación web interactiva para explorar el **ICR-Dengue**, un índice compuesto
que estima el riesgo relativo de mortalidad por dengue en México, integrando
variables clínicas, ambientales y sociodemográficas a nivel estatal.

Este proyecto es resultado del trabajo de tesis de maestría del autor y dio
origen al artículo *"ICR-Dengue: índice compuesto de riesgo de mortalidad por
dengue en México"* (en revisión, BMC / Springer Nature) y a una revisión
sistemática relacionada (enviada a *Journal of Vector Borne Diseases*).

> **Estado del proyecto:** funcional y desplegado en producción en
> **[pagina-icr-dengue-8qrf2pd2gyalfjhadrsxuc.streamlit.app](https://pagina-icr-dengue-8qrf2pd2gyalfjhadrsxuc.streamlit.app/)**
> (Streamlit Community Cloud), y también puede ejecutarse localmente.

## ¿Qué hace la app?

- **Mapas interactivos de México** (Folium) coloreados por tasa de mortalidad
  y por ICR-Dengue promedio, por estado y por periodo (2020-2024, 2022-2024,
  2025), con vista modal a pantalla completa.
- **Filtros dinámicos** por año (con cuartiles calculados en tiempo real) y
  por variable clínica/ambiental, mediante radio buttons y multiselect.
- **Gráficas** (Plotly) de tasa de mortalidad e ICR-Dengue promedio por
  entidad y periodo.
- **Ficha descriptiva del ICR-Dengue**: qué variables lo componen y cómo se
  interpreta, alineada con la metodología del manuscrito.
- **Métricas nacionales** (tarjetas resumen) del ICR-Dengue promedio por
  periodo.

## Stack técnico

| Componente | Tecnología |
|---|---|
| Framework web | [Streamlit](https://streamlit.io/) |
| Datos geoespaciales | GeoPandas, Shapely, PyProj, `mexico_simple.gpkg` |
| Mapas | Folium + `streamlit-folium` |
| Gráficas | Plotly, Matplotlib |
| Procesamiento de datos | Pandas, NumPy, PyArrow (Parquet) |

## Pipeline de datos

`preparar_datos.py` procesa la base de datos original de defunciones
(`data/Base de datos principal defunciones.xlsx`) y genera los datasets
consolidados con el ICR-Dengue calculado (`dataset_con_irm*.csv`,
`datos_*.parquet`) que consume `streamlit_app.py`. Todas las variables son
agregadas/clínicas (edad, sexo, temperatura, precipitación, comorbilidades,
etc.) — no contienen identificadores personales.

## Configuración local

```bash
python -m venv venv
venv\Scripts\activate          # Windows
pip install -r requirements.txt

streamlit run streamlit_app.py
```

La app quedará disponible en `http://localhost:8501`.

## Despliegue

La app está desplegada en [Streamlit Community Cloud](https://streamlit.io/cloud):
**https://pagina-icr-dengue-8qrf2pd2gyalfjhadrsxuc.streamlit.app/**

Para desplegar tu propia copia:

1. Haz fork o clona este repositorio.
2. En [share.streamlit.io](https://share.streamlit.io): **New app** → conecta
   el repositorio → selecciona `streamlit_app.py` como archivo principal.
3. Streamlit Cloud instala automáticamente las dependencias de
   `requirements.txt` y despliega la app.
4. Cada `git push` a `main` actualiza automáticamente la versión desplegada.

## Autor

Miguel Alcaraz Vázquez — proyecto desarrollado como parte de la tesis de
maestría en Ingeniería para la Innovación y Desarrollo Tecnológico.
