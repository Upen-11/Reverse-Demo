# Reverse-Demo
This is my first Git Repo.
<br>
Author-Upendra Son Tirkey
"Austin_bikeshare analysis"
WITH
  longest_used_bike AS (
    SELECT
      bike_id, 
      SUM(duration_minutes) AS trip_duration
    FROM 
      `bigquery-public-data.austin_bikeshare.bikeshare_trips`
    GROUP BY
      bike_id
  ),
  longest_bike_id AS (
    SELECT
      bike_id
    FROM
      longest_used_bike
    ORDER BY
      trip_duration DESC
    LIMIT 1
  )
SELECT
  trips.start_station_id, 
  COUNT(*) AS trip_ct
FROM
  `bigquery-public-data.austin_bikeshare.bikeshare_trips` AS trips
JOIN
  longest_bike_id
ON
  trips.bike_id = longest_bike_id.bike_id
GROUP BY
  trips.start_station_id
ORDER BY
  trip_ct DESC;

"Second"
WITH
  longest_used_bike AS (
    SELECT
      bike_id, 
      SUM(duration_minutes) AS trip_duration
    FROM 
      `bigquery-public-data.austin_bikeshare.bikeshare_trips`
    GROUP BY
      bike_id
    ORDER BY
      trip_duration DESC
    LIMIT 1
  )
SELECT
  trips.start_station_id, 
  COUNT(*) AS trip_ct
FROM
  longest_used_bike AS longest
INNER JOIN
  `bigquery-public-data.austin_bikeshare.bikeshare_trips` AS trips
ON 
  longest.bike_id = trips.bike_id
GROUP BY
  trips.start_station_id
ORDER BY
  trip_ct DESC
LIMIT 1;
"This is SQL function which help to understand or create temprory table along with joins"
