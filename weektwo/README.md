1. yellow_tripdata_2020-12.csv - 134.5MB
2. "{{inputs.taxi}}_tripdata_{{inputs.year}}-{{inputs.month}}.csv" -  inputs taxi is set to green, year is set to 2020, and month is set to 04
→ green_tripdata_2020-04.csv
3.  SELECT count(*) FROM `projectid.zoomcamp.yellow_tripdata` WHERE filename like '%2020%';   24648499
4. SELECT count(*) FROM `projectid.zoomcamp.yellow_tripdata` WHERE filename like '%2020%'; 1734051
5. SELECT count(*) FROM `projectid.zoomcamp.yellow_tripdata` WHERE filename like '%2021-03%'; 1925152
6. B