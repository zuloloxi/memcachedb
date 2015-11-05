### Testing Environment ###

  * Box: Dell 2950III
  * OS: Linux CentOS 5
  * Version: memcachedb-1.0.0-beta
  * Client API: libmemcached

### Non-thread Edition ###

Started:
```
memcachedb -d -r -u root -H /data1/mdbtest/ -N -v
```

**Write**

key: 16 value: 100B, 8 concurrents, every process does 2,000,000 set

|No.|1|2|3|4|5|6|7|8|avg.|
|:--|:|:|:|:|:|:|:|:|:---|
|Cost(s)|807|835|840|853|859|857|865|868|848 |

```
2000000 * 8 / 848 = 18868 w/s
```

**Read**

key: 16 value: 100B, 8 concurrents, every process does 2,000,000 get

|No.|1|2|3|4|5|6|7|8|avg.|
|:--|:|:|:|:|:|:|:|:|:---|
|Cost(s)|354|354|359|358|357|364|363|365|360 |

```
2000000 * 8 / 360 = 44444 r/s
```

### Thread Edition(4 Threads) ###

Started:
```
memcachedb -d -r -u root -H /data1/mdbtest/ -N -t 4 -v
```

**Write**

key: 16 value: 100B, 8 concurrents, every process does 2,000,000 set

|No.|1|2|3|4|5|6|7|8|avg.|
|:--|:|:|:|:|:|:|:|:|:---|
|Cost(s)|663|669|680|680|684|683|687|686|679 |

```
2000000 * 8 / 679 = 23564 w/s
```

**Read**

key: 16 value: 100B, 8 concurrents, every process does 2,000,000 get

|No.|1|2|3|4|5|6|7|8|avg.|
|:--|:|:|:|:|:|:|:|:|:---|
|Cost(s)|245|249|250|248|248|249|251|250|249 |

```
2000000 * 8 / 249 = 64257 r/s
```