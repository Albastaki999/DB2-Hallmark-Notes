1. Terminate current connection

   ```
   db2 terminate
   ```

2. Check if any loads or backups are running first

```
db2 list utilities show detail
```

3. Stop the running instance

   ```
   db2stop
   ```

   or

   ```
   db2stop force
   ```

4. Update dbm cfg plugins

   ```
   db2 update dbm cfg using SRVCON_PW_PLUGIN IBMLDAPauthserver
   ```

   and

   ```
   db2 update dbm cfg using GROUP_PLUGIN IBMLDAPgroups
   ```

5. Restart
   ```
   db2start
   ```
