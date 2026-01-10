# dezc

1. Run docker with entrypoint bash
```sh
docker run --rm -it --entrypoint=/bin/bash python:3.13
python --version
pip --version #25.3
```

2. name is postgres port is 5432 (within the network in which both containers are running)

3. Run docker container
```sh
docker run -it \
  --network=weekone_default \
  taxi_ingest:v001 \
    --pg-user=postgres \
    --pg-pass=postgres \
    --pg-host=postgres \
    --pg-port=5432 \
    --pg-db=ny_taxi \
    --target-table=yellow_taxi_trips \
    --year=2021 \
    --month=1 \
    --chunksize=100000
```
```sh
docker run -it \
  --network=weekone_default \
  taxi_ingest:v001 \
    --pg-user=postgres \
    --pg-pass=postgres \
    --pg-host=postgres \
    --pg-port=5432 \
    --pg-db=ny_taxi \
    --target-table=yellow_taxi_trips_2021_2 \
    --year=2021 \
    --month=2 \
    --chunksize=100000
```