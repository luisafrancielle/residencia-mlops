# residencia-mlops

Readme em construção: 

## Configurações do Job - salvando temporariamente aqui: 

STAC_URL = https://earth-search.aws.element84.com/v1 <br>
CLOUD_COVER_MAX = 40 <br>
TILE_SIZE = 256 <br>
MISSIONS = HLS,S2 <br>
OUTPUT_PREFIX =  gs://residencia-lu-instageo/chips/run-20251021-2030/ <br>
INPUT_URI = gs://residencia-lu-instageo/raw/aoi.geojson <br>

## Autenticar Docker e Artifact Registry**

```bash

gcloud auth configure-docker us-central1-docker.pkg.dev
```

## Comandos importantes**

```bash
# listar as imagens
gcloud artifacts docker images list \
  us-central1-docker.pkg.dev/residencia-lu/instageo-artifacts | grep chip-creator

# atualizar o job para usar a nova versão, no caso a v2:
gcloud run jobs update chip-creator \
  --region=us-central1 \
  --image=us-central1-docker.pkg.dev/residencia-lu/instageo-artifacts/chip-creator:v2
  
```

Depois:

```bash  
    gcloud run jobs execute chip-creator \
  --region=us-central1 \
  --update-env-vars=INPUT_URI=gs://residencia-lu-instageo/raw/aoi.geojson

```
