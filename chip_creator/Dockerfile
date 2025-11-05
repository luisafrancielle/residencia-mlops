FROM python:3.11-slim

# Geo deps + git + toolchain básico
RUN apt-get update && apt-get install -y \
    gdal-bin libgdal-dev git build-essential curl ca-certificates \
  && rm -rf /var/lib/apt/lists/*

WORKDIR /app

# Instalação do InstaGeo (apenas data+cpu) usando sintaxe PEP 508
RUN pip install --no-cache-dir \
  "InstaGeo[cpu,data] @ git+https://github.com/instadeepai/InstaGeo-E2E-Geospatial-ML.git"

# Dependências auxiliares
RUN pip install --no-cache-dir \
    gcsfs rasterio shapely pystac-client numpy xarray

RUN pip install --no-cache-dir geopandas

COPY app/ app/

CMD ["python", "-m", "app.main"]