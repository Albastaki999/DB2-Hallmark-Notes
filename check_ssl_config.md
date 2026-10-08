Assuming that \
client &rarr; `db2inst2` \
server &rarr; `db2inst1`

Check SSL configuration

```
db2 get dbm cfg | grep -i SSL
```

On client side check whether these key db and stash files even exist or not

```
ls -l /home/db2inst2/ssl/db2ssl.kdb /home/db2inst2/ssl/db2ssl.sth
```

Check actual ssl files available

```
ls -l /home/db2inst2/sqllib/security/ssl/
```

```
find /home/db2inst2 \
  -type f \
  \( -name "*.kdb" -o -name "*.sth" -o -name "*.p12" \) \
  -ls 2>/dev/null
```

Check if GSKit can open the available correct .p12

```
gsk8capicmd_64 -cert -list \
  -db /home/db2inst2/sqllib/security/ssl/rockdb2d01.cloud.hallmark.com.p12 \
  -stashed \
  -type pkcs12
```

We do have a backup file containing the old dbm cfg for ssl: `dbmcfgssl_before.out`

```
cat /home/db2inst2/sqllib/security/ssl/dbmcfgssl_before.out
```

Change to old ssl config
db2 update dbm cfg using \
 SSL_CLNT_KEYDB /home/db2inst1/sqllib/security/ssl/rockdb2d01.cloud.hallmark.com.p12 \
 SSL_CLNT_STASH /home/db2inst1/sqllib/security/ssl/rockdb2d01.cloud.hallmark.com.sth
