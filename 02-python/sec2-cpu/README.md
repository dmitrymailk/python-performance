### запустить профилировку кода для подсчета расстояний и сохранить трейс в файл
```bash
python -m cProfile -o distance_cache.prof distance_cache.py
```
### визуализировать трейс в браузере, покажет только функции и общее их время выполнения. не построчно.
```bash
snakeviz distance_cache.prof
```

### запустить профилирование с подключенным построчным профилированием. не нужно ждать пока скрипт полностью завершит свою работу, так как это может занять многие часы.
```bash
kernprof -l lprofile_distance_cache.py
```

### посмотреть на результаты построчного профилирования
```bash
python -m line_profiler lprofile_distance_cache.py.lprof
```
```console
Timer unit: 1e-06 s

Total time: 63.3593 s
File: lprofile_distance_cache.py
Function: get_distance at line 16

Line #      Hits         Time  Per Hit   % Time  Line Contents
==============================================================
    16                                           @profile
    17                                           def get_distance(p1, p2):
    18  13526214    2592135.5      0.2      4.1      lat1, lon1 = p1
    19  13526214    2658497.7      0.2      4.2      lat2, lon2 = p2
    20                                           
    21  13526214    4854446.2      0.4      7.7      lat_dist = math.radians(lat2 - lat1)
    22  13526214    4006110.5      0.3      6.3      lon_dist = math.radians(lon2 - lon1)
    23  13526213    1977153.8      0.1      3.1      a = (
    24  13526214    8365147.9      0.6     13.2          math.sin(lat_dist / 2) * math.sin(lat_dist / 2) +
    25  27052428   12059034.4      0.4     19.0          math.cos(math.radians(lat1)) * math.cos(math.radians(lat2)) *
    26  27052427    8902982.7      0.3     14.1          math.sin(lon_dist / 2) * math.sin(lon_dist / 2)
    27                                               )
    28  13526213   10508028.0      0.8     16.6      c = 2 * math.atan2(math.sqrt(a), math.sqrt(1 - a))
    29  13526213    2116592.7      0.2      3.3      earth_radius = 6371
    30  13526213    2895057.4      0.2      4.6      dist = earth_radius * c
    31                                           
    32  13526213    2424157.3      0.2      3.8      return dist
```