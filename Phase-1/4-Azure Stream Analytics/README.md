# Stream Analytics related example queries

## To read data from json file - Input.json
```
SELECT City,
    Coordinates.Latitude,
    Coordinates.Longitude
INTO streamoutput
FROM streaminput
```

## IOT Simulator
https://azure-samples.github.io/raspberry-pi-web-simulator/

## Windowing Function examples

### Normal Filter
```
SELECT *
INTO output
FROM input
HAVING Temperature > 27
```

### Tumbling Window
```
SELECT deviceid, AVG(humidity) as avg_humidity, AVG(temperature) as avg_temperature
INTO output
FROM input
GROUP BY deviceid, TumblingWindow(second, 20)
```

### Hopping Window
```
SELECT deviceid, AVG(humidity) as avg_humidity, AVG(temperature) as avg_temperature
INTO output
FROM input
GROUP BY deviceid, HoppingWindow(second, 20, 2)
```

### Sliding Window
```
SELECT deviceid, AVG(humidity) as avg_humidity, AVG(temperature) as avg_temperature
INTO output
FROM input
GROUP BY deviceid, SlidingWindow(second, 20)
```

### The Session Window
```
SELECT deviceid, AVG(humidity) as avg_humidity, AVG(temperature) as avg_temperature
INTO output
FROM input
GROUP BY deviceid, SessionWindow(second, 5, 20);
```

### Snapshot Window
```
SELECT deviceid, AVG(humidity) as avg_humidity, AVG(temperature) as avg_temperature
INTO output
FROM input
GROUP BY deviceid, System. Timestamp();
```

### Timestamp By
```
SELECT deviceid, AVG(humidity) as avg_humidity, AVG(temperature) as avg_temperature
INTO output
FROM input TIMESTAMP BY EntryTime
GROUP BY deviceid, HoppingWindow(second, 20, 2)
```