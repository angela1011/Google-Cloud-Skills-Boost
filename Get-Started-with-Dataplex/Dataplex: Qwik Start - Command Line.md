# Dataplex: Qwik Start - Command Line

## Enable the Dataplex API and set variables:

```bash
gcloud services enable dataplex.googleapis.com 
export PROJECT_ID=$(gcloud config get-value project)
export REGION=europe-west1
gcloud config set compute/region $REGION
```

## Create a lake:

```bash
gcloud dataplex lakes create ecommerce \
   --location=$REGION \
   --display-name="Ecommerce" \
   --description="Ecommerce Domain"
```

## Add a zone to your lake:

```bash
gcloud dataplex zones create orders-curated-zone \
    --location=$REGION \
    --lake=ecommerce \
    --display-name="Orders Curated Zone" \
    --resource-location-type=SINGLE_REGION \
    --type=CURATED \
    --discovery-enabled \
    --discovery-schedule="0 * * * *"
```

## Create a BigQuery dataset:

```bash
bq mk --location=$REGION --dataset orders 
```

## Attach the BigQuery dataset to the zone:

```bash
gcloud dataplex assets create orders-curated-dataset \
--location=$REGION \
--lake=ecommerce \
--zone=orders-curated-zone \
--display-name="Orders Curated Dataset" \
--resource-type=BIGQUERY_DATASET \
--resource-name=projects/$PROJECT_ID/datasets/orders \
--discovery-enabled 
```

## Detach an asset:

```bash
gcloud dataplex assets delete orders-curated-dataset --location=$REGION --zone=orders-curated-zone --lake=ecommerce 
```
If prompted to confirm, enter Y.

## Delete a zone:

```bash
gcloud dataplex zones delete orders-curated-zone --location=$REGION --lake=ecommerce
```
If prompted to confirm, enter Y.

## Delete the lake:

```bash
gcloud dataplex lakes delete ecommerce --location=$REGION
```

## Congratulation!
