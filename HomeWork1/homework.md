# Data-Engineering_zoomcamp
##### My Rep for Homework and notes for the zoomcamp

###  Homework 1 
1. Run docker with the python:3.12.8 image in an interactive mode, use the entrypoint bash.
to run this version of docker we will use the following command : 
    ```bash
    docker run -it python:3.12.8 bash
    ```
    we will get pip version using command :
    ```bash
    pip --version
    ```
    the answer will be  24.3.1
2. Given the following docker-compose.yaml, what is the hostname and port that pgadmin should use to connect to the postgres database?
 
        the answer should be  db:5432
    as docker-compose file uses service name for inter-container communication , container name
    is used to stop or run the container and not as a hostname for it .


3.   During the period of October 1st 2019 (inclusive) and    November 1st 2019 (exclusive), how many trips happened up to 1 mile
   ```sql
   SELECT COUNT(*)
    FROM green_taxi AS gt
    WHERE gt.lpep_pickup_datetime >= '2019-10-01 00:00:00'
    AND gt.lpep_pickup_datetime < '2019-11-01 00:00:00'
    AND gt.trip_distance <= 1;
   ```

4. Which was the pick up day with the longest trip distance?
    ```sql
    SELECT MAX(gt.trip_distance) as max_trip , gt.lpep_pickup_datetime
    FROM green_taxi as gt
    GROUP BY gt.lpep_pickup_datetime
    ORDER BY "max_trip" DESC
    LIMIT 1
    ```
    the answer is 2019-10-31

5. Biggest pickup zones 
    ```sql
    SELECT gt."PULocationID",
       SUM(gt.total_amount) AS total_amount_sum
    FROM green_taxi AS gt
    WHERE DATE(gt.lpep_pickup_datetime) = '2019-10-18'
    GROUP BY gt."PULocationID"
    HAVING SUM(gt.total_amount) > 13000
    ORDER BY total_amount_sum DESC;
    ```
    the answer is going to be East Harlem North, East Harlem South, Morningside Heights

6. Largest tip 
   ```sql
   SELECT gt."DOLocationID"
    FROM green_taxi AS gt,
        zones as zpu
    WHERE DATE(gt.lpep_pickup_datetime) >= '2019-10-01'
        AND
        DATE(gt.lpep_pickup_datetime) < '2019-11-01'
        AND
        gt."PULocationID" = zpu."LocationID"
        AND 
        zpu."Zone" = 'East Harlem North'
    ORDER BY gt.tip_amount DESC;
   ```
   the answer is going to be JFK Airport

7. the answer will be 
   terraform init, terraform apply -auto-approve, terraform destroy