**This benchmark is for memcachedb-0.1.x. To see latest benchmark, please check [Benchmark](Benchmark.md).**

memcachedb is very fast to get/set an object.

We do a simple testing on a Dell PowerEdge 2850 box that sets
200,000,000 records into memcachedb with a 16 bytes key and 10 bytes
value.

Simply start memcachedb with:
```
./memcachedb -d -r -u root -N
```

And here is testing case:

```
#include <stdio.h>
#include <string.h>
#include "memcache.h"

int main(int argc, char **argv){
   int ret = 0;
   char key[32] = {0};
   char val[32] = {0};
   int n = 0;
   time_t start;
   time_t end;
   struct memcache *mc = mc_new();
   mc_server_add4(mc, "127.0.0.1:21211");

   start = time(NULL);
   for (n=0; n<200000000; n++){
       sprintf(key, "%016d", n);
       sprintf(val, "%010d", n);
       ret = mc_set(mc, key, strlen(key), val, strlen(val), 0, 0);
   }
   end =  time(NULL);
   printf("time cost: %d second\n", end - start);

   mc_free(mc);
   return 0;
}
```

The total time cost is: 16572 second, the db file size is 7.7 GB.
It writes almost **12000** records per second and simultaneously does checkpoint
every 60 sec and deadlock detecting every 100 ms!!

When the **set** testing case is running, we start another testing
case(on same daemon):
```
#include <stdio.h>
#include <string.h>
#include "memcache.h"

int main(int argc, char **argv){
   char *ret = 0;
   char key[32] = {0};
   int n = 0;
   time_t start;
   time_t end;
   struct memcache *mc = mc_new();
   mc_server_add4(mc, "127.0.0.1:21211");

   start = time(NULL);
   for (n=0; n<1000000; n++){
       sprintf(key, "%016d", n);
       ret = mc_aget(mc, key, strlen(key));
       //printf("%s\n", ret);
       free(ret);
   }
   end =  time(NULL);
   printf("time cost: %d second\n", end - start);

   mc_free(mc);
   return 0;
}
```
The total time cost is: 103 second.
It reads **10000** records per second simultaneously with a heavy load
of 12000 per second writing!!