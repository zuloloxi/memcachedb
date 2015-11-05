2008-02-21 Version 1.0.1-beta released

2008-02-21 Steve Chu <stvchu@gmail.com>
  * Bugfix: some private commands may cause seg fault

2008-02-20 Steve Chu <stvchu@gmail.com>
  * Bugfix: incr/decr command did not update length string

2008-02-18 Steve Chu <stvchu@gmail.com>
  * merge all read-only private command of replication into 'stats rep' that memcached client can read it. Original commands are still available. 'stats bdb' is also provided.
  * 'mdbtop.py', a new monitor tool is added for easy maintaining. See 'tools/mdbtop.py'

2008-02-14 Big Version 1.0.0-beta released

2008-02-01 Steve Chu <stvchu@gmail.com>
  * Almost entire code is rewritten based on Memcached 1.2.x.
  * More memcache protocol compatibility, now multiple get and flags are supported, also udp and unix socket is ready(not yet tested).
  * big performance improved due to memcached 1.2.x code base. Thread is used to resolve the blocked I/O.
  * use standard build tool, "./configure;make;make install" and done.
  * two new pravite command for replication to set/get priority. See "doc/replication.txt".

2007-01-21 Version 0.1.1 released

2008-01-21 Steve Chu <zhuxin@staff.sina.com.cn>
  * Bug fix: out string 'NOT STORED' breaks clients, it should be 'NOT\_STORED'!

2007-11-05 Version 0.1.0 released

2007-10-30 Cao Kai <caokai@staff.sina.com.cn>, Steve Chu <zhuxin@staff.sina.com.cn>
  * big replication code merged, let's ship it!
> using option "-R" to enable replication, two private command is added for replication: db\_ismaster, db\_whoismaster
  * code refactor for performance and readability

2007-10-23 Version 0.0.4 released

2007-10-22 Steve Chu <zhuxin@staff.sina.com.cn>
  * add a new struct db\_settings for all db related configures.
  * big code cleanup for performance.
  * "-L" option now uses a unit of kbytes.

2007-10-19 Cao Kai <caokai@staff.sina.com.cn>
  * add option "-C" and create a separate thread to do periodic checkpoint
  * add option "-D" and create a separate thread to do periodic deadlock detecting

2007-10-15 Novey Donar <xiaogang1@staff.sina.com.cn>
  * remove the item key in data.data, about 50% db file size reduced, but not compatible with previous versions, warning to use.

2007-10-08 Steve Chu <zhuxin@staff.sina.com.cn>
  * add option "-L" to allow to set transaction log buffer
  * add option "-N" to allow to set DB\_TXN\_NOSYNC flag, if someone wanted lots of performance improved, but warning to use, because it loses transaction's durability

2007-09-29 Version 0.0.3 released

2007-09-29 Steve Chu <zhuxin@staff.sina.com.cn>
  * add command "flush\_all" that will truncate a database, warning to use.
  * lots of code formated
  * Bugfix: Now using "-u" option can get proper db file mode

2007-09-21 Version 0.0.2 released

2007-09-20 Steve Chu <zhuxin@staff.sina.com.cn>
  * move some macro to memcachedb.h
  * rename chkpoint to db\_checkpoint, for consistency.
  * add new command "db\_archive" to remove log files that are no longer needed
  * README updated

2007-09-19 Steve Chu <zhuxin@staff.sina.com.cn>
  * enlarge incr value to unsigned int to conform memcache protocol, now supports max value of 4294967295.

2007-09-18 Version 0.0.1 released