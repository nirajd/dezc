# dezc

1. Run docker with entrypoint bash
```sh
docker run --rm -it --entrypoint=/bin/bash python:3.13
python --version
pip --version #25.3
```

2. name is postgres or db port is 5432 (within the network in which both containers are running)

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
docker build -t taxi_ingest:v002 .
docker run -it \
  --network=weekone_default \
  taxi_ingest:v002 \
    --pg-user=postgres \
    --pg-pass=postgres \
    --pg-host=postgres \
    --pg-port=5432 \
    --pg-db=ny_taxi \
    --target-table=green_taxi_trips_2025_11 \
    --year=2025 \
    --month=11 \
    --chunksize=100000
```
```sql
select count(*) from green_taxi_data
where lpep_pickup_datetime between '2025-11-01' and '2025-12-01'
and trip_distance<=1; -- 8,007
```

4.
```sql
select lpep_pickup_datetime from green_taxi_data
where trip_distance<100
order by trip_distance desc
limit 1; -- 2025-11-14
```

5.
```sql
select 
  z."Zone", sum(t.total_amount)
from green_taxi_data as t
join taxi_zone_lookup as z on t."PULocationID" = z."LocationID"
where lpep_pickup_datetime between '2025-11-18' and '2025-11-19'
group by 1
order by 2 desc
limit 1; -- East Harlem North
```

6.
```
select 
  zd."Zone", t.tip_amount
from green_taxi_data as t
join taxi_zone_lookup as zp on t."PULocationID" = zp."LocationID" and zp."Zone"='East Harlem North'
join taxi_zone_lookup as zd on t."DOLocationID" = zd."LocationID"
where lpep_pickup_datetime between '2025-11-01' and '2025-12-01'
order by 2 desc
limit 1; -- Yorkville West

7. 