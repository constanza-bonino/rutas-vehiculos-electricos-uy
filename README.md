# rutas-vehiculos-electricos-uy

Proyecto final de **Algoritmos Avanzados de Búsqueda y Optimización** (UCU): rutas de tiempo mínimo para vehículos eléctricos en Uruguay. Compara un enfoque exacto (**Dijkstra**) con uno heurístico (**voraz**).

## Cómo correrlo

1. Instalar las dependencias: `pip install -r requirements.txt`
2. Abrir `rutas_ve_uruguay.ipynb` en VS Code (o Jupyter) y correr las celdas en orden.

La primera vez, el notebook necesita internet para:

- bajar el mapa oficial de la red de carga (MIEM / UTE) y guardarlo en `datos/red_carga.kml`;
- pedir a OSRM (OpenStreetMap) las distancias y los tiempos por carretera, que se guardan en `datos/matriz_*.npz`.

Después funciona sin conexión. Si OSRM no responde, usa una aproximación en línea recta y lo avisa.

## Estructura

| Ruta | Contenido |
|---|---|
| `rutas_ve_uruguay.ipynb` | todo el proyecto, explicado paso a paso |
| `datos/` | datos descargados (se crea solo) |
| `resultados/` | tablas CSV y figuras PNG para el informe (se crea solo) |

## Modelo

- Grafo $G=(V,E)$ con $V=\{s,t\}\cup C$: origen, destino y puntos de carga.
- El vehículo sale con la batería llena y recarga al 100 % en cada parada.
- Hay arista $(i,j)$ si $\kappa\,d_{ij} \le B - b_{\min}$.
- Costo: $c_{ij} = \tau_{ij} + \kappa\,d_{ij}/P_j$ si $j$ es un cargador, y $\tau_{ij}$ si $j = t$.
- El vehículo es genérico: se definen su batería, su consumo y las potencias de carga que admite.
