squid2radius
============

squid2radius analyzes your squid `access.log` file, and reports usage information to a RADIUS server using `Accounting-Request` as defined in RFC 2866.

After analyzing is finished, it calls squid to rotate your log file so that no lines will be counted more than once.

Installation
------------

### Clone Git repo

```bash
git clone git://github.com/billzhong/squid2radius.git
```

Usage
-----

```
usage: squid2radius.py [-h] [-p RADIUS_ACCT_PORT]
                       [--radius-nasid RADIUS_NASID] [--squid-path SQUID_PATH]
                       [--exclude-pattern EXCLUDE_PATTERN]
                       logfile_path radius_server radius_secret
```

For instance, run like this if you have access log file at `/var/log/squid/access.log`, RADIUS server running at `localhost` with secret set to `testing123`:

```bash
sudo python squid2radius.py /var/log/squid/access.log localhost testing123
```

It is certainly a good idea to make a cron job for this.

You should also read [SquidFaq/SquidLogs](http://wiki.squid-cache.org/SquidFaq/SquidLogs#access.log) to make sure your log files are in reasonable sizes.

### --exclude-pattern

If for some reason you need to prevent usage information of certain user from being sent to the RADIUS server, there is an argument for that!  Use `--exclude-pattern="(girl|boy)friend"` and squid2radius won't send usage of either your `girlfriend` or `boyfriend` to the RADIUS server.

Note
----

The script assumes that you are using the default [Squid native access.log format](http://wiki.squid-cache.org/Features/LogFormat#squid) on first ten columns of your log file.  If you need custom columns, add them after the default ones.

