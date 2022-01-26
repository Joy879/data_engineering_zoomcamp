### Question  3

            SELECT
              COUNT(1)
            FROM
              trips
            WHERE
              (tpep_pickup_datetime>='2021-01-15 00:00:00' AND
              tpep_pickup_datetime<'2021-01-16 00:00:00');
### Question 4
            SELECT
              CAST(tpep_pickup_datetime AS DATE) as "day",
              MAX(tip_amount) as "max_tip"
            FROM
              trips
            GROUP BY
              1
            ORDER BY
              "max_tip" DESC;
### Question 5
            SELECT
                CONCAT(zpu."Borough", '/', zpu."Zone") AS "pickup_loc",
                CONCAT(zdo."Borough", '/', zdo."Zone") AS "dropoff_loc",
                COUNT(1) AS "amount_of_trips"
            FROM
                trips t JOIN zones zpu
                    ON t."PULocationID" = zpu."LocationID"
                JOIN zones zdo
                    ON t."DOLocationID" = zdo."LocationID"
            WHERE
              t."PULocationID" = (
                SELECT
                  "LocationID"
                FROM
                  zones zpu
                WHERE
                  zpu."Zone" IN ('Central Park')
              )
            GROUP BY
              1, 2 
            ORDER BY
              "amount_of_trips" DESC
            ;
### Question 6
            SELECT
                CONCAT(zpu."Zone", '/', zdo."Zone") AS "zone_pair",
                AVG(t."total_amount") AS "total_amount_average"
            FROM
                trips t JOIN zones zpu
                    ON t."PULocationID" = zpu."LocationID"
                JOIN zones zdo
                    ON t."DOLocationID" = zdo."LocationID"
            GROUP BY
              1
            ORDER BY
              2 DESC
            ;
