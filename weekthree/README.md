
```
CREATE OR REPLACE EXTERNAL TABLE `weekthree.yellow_tripdata`
OPTIONS (
  format = 'parquet',
  uris = ['gs://band_worn_lud_ride_9/yellow_tripdata_2024-*.parquet']
);

create or replace table `weekthree.yellow_tripdata_materialized` as
select * from `weekthree.yellow_tripdata`;
```


1. `select count(1) from weekthree.yellow_tripdata;` - 20,332,093
2.
```
select count(distinct PULocationID) from weekthree.yellow_tripdata_materialized; -- 155.12MB

select count(distinct PULocationID) from weekthree.yellow_tripdata; -- 0MB
```
3.
```
select PULocationID from `weekthree.yellow_tripdata_materialized` -- 155.12MB
select PULocationID, DOLocationID from `weekthree.yellow_tripdata_materialized`; -- 310.24MB
```
4.
```
select PULocationID, DOLocationID from `weekthree.yellow_tripdata_materialized`; --8,333
````

5.
```
create or replace table weekthree.yellow_tripdata_partitioned_c
partition by date(tpep_dropoff_datetime)
cluster by vendorID
as (select * from `weekthree.yellow_tripdata`);
```

6.
```
select distinct(vendorid) from weekthree.yellow_tripdata_materialized
where date(tpep_dropoff_datetime) between '2024-03-01' and '2024-03-15'; -- 310.24MB

select distinct(vendorid) from `weekthree.yellow_tripdata_partitioned_c`
where date(tpep_dropoff_datetime) between '2024-03-01' and '2024-03-15'; -- 26.84MB
```

7. GCP Bucket

8. No, may not be beneficial for very small datasets

9. 0B - Bigquery is smart enough.