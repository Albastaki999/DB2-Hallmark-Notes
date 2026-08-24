## Ldap Important Commands

1. Query RootDSE

   ```
   ldapsearch -x \
   -H ldap://awsmasterdc1.master.hmkad.hallmark.com:389 \
   -s base \
   -b "" \
   defaultNamingContext \
   dnsHostName
   ```

2. Search for an AD User

   ```
   ldapsearch -x \
   -H ldap://awsmasterdc1.master.hmkad.hallmark.com:389 \
   -b "DC=master,DC=hmkad,DC=hallmark,DC=com" \
   "(sAMAccountName=PYF522)" \
   dn sAMAccountName
   ```

3. Trigger password prompt

   ```
   ldapsearch -x \
   -H ldap://awsmasterdc1.master.hmkad.hallmark.com:389 \
   -D 'CN=LDAP_Connect,OU=@ServiceAccounts,OU=MEDIUM,OU=@ADMIN,DC=master,DC=hmkad,DC=hallmark,DC=com' \
   -W \
   -b 'DC=master,DC=hmkad,DC=hallmark,DC=com' \
   '(sAMAccountName=PYF522)' \
   dn sAMAccountName
   ```

4. Which groups user belongs to

   ```
   ldapsearch -x \
   -H ldap://awsmasterdc1.master.hmkad.hallmark.com:389 \
   -D 'CN=LDAP_Connect,OU=@ServiceAccounts,OU=MEDIUM,OU=@ADMIN,DC=master,DC=hmkad,DC=hallmark,DC=com' \
   -W \
   -b 'DC=master,DC=hmkad,DC=hallmark,DC=com' \
   '(sAMAccountName=PYF522)' \
   memberOf
   ```

5. Show several useful attributes

   ```
   ldapsearch -x \
   -H ldap://awsmasterdc1.master.hmkad.hallmark.com:389 \
   -D 'CN=LDAP_Connect,OU=@ServiceAccounts,OU=MEDIUM,OU=@ADMIN,DC=master,DC=hmkad,DC=hallmark,DC=com' \
   -W \
   -b 'DC=master,DC=hmkad,DC=hallmark,DC=com' \
   '(sAMAccountName=PYF522)' \
   dn \
   sAMAccountName \
   userPrincipalName \
   msDS-PrincipalName \
   memberOf
   ```

6. Find a group in AD

   ```
   ldapsearch -x \
   -H ldap://awsmasterdc1.master.hmkad.hallmark.com:389 \
   -D 'CN=LDAP_Connect,OU=@ServiceAccounts,OU=MEDIUM,OU=@ADMIN,DC=master,DC=hmkad,DC=hallmark,DC=com' \
   -W \
   -b 'DC=master,DC=hmkad,DC=hallmark,DC=com' \
   '(cn=DB2IADM2)' \
   dn cn
   ```

7. Find whether a user exists in AD

   ```
   ldapsearch -x \
   -H ldap://awsmasterdc1.master.hmkad.hallmark.com:389 \
   -D 'CN=LDAP_Connect,OU=@ServiceAccounts,OU=MEDIUM,OU=@ADMIN,DC=master,DC=hmkad,DC=hallmark,DC=com' \
   -W \
   -b 'DC=master,DC=hmkad,DC=hallmark,DC=com' \
   '(sAMAccountName=db2inst2)' \
   dn sAMAccountName
   ```

8. Wildcard search
   ```
   ldapsearch -x \
   -H ldap://awsmasterdc1.master.hmkad.hallmark.com:389 \
   -D '...' \
   -W \
   -b 'DC=master,DC=hmkad,DC=hallmark,DC=com' \
   '(sAMAccountName=PYF*)' \
   sAMAccountName
   ```

### Flags to remember

- `-x` &rarr; Simple LDAP authentication
- `-H` &rarr; LDAP server URL (WHERE am I connecting?)
- `-D` &rarr; Bind DN / login identity (WHO am I logging in as?)
- `-W` &rarr; Ask for password interactively (Ask me for its password)
- `-b` &rarr; Search Base DN (WHERE in AD should I search?)

### LDAPS / Certificate Commands

1.  Check whether 636 speaks TLS:

    ```
    openssl s_client \
    -connect awsmasterdc1.master.hmkad.hallmark.com:636 \
    -servername awsmasterdc1.master.hmkad.hallmark.com
    ```

    **This tells you things like
    Did TCP connection succeed?**
    - Did TLS handshake happen?
    - Which certificate was presented?
    - Who issued it?
    - Which TLS version/cipher was negotiated?

2.  Check with supplied CA Certificate

    ```
    openssl s_client \
    -connect awsmasterdc1.master.hmkad.hallmark.com:636 \
    -servername awsmasterdc1.master.hmkad.hallmark.com \
    -CAfile /tmp/excelsior11.pem
    ```

3.  Strict `ldapsearch` over LDAPS
    ```
    LDAPTLS_CACERT=/tmp/excelsior11.pem \
    LDAPTLS_REQCERT=demand \
    ldapsearch -x \
    -H ldaps://awsmasterdc1.master.hmkad.hallmark.com:636 \
    -s base \
    -b "" \
    defaultNamingContext
    ```

### 5 Main Commands

1. Discover LDAP Base DN (Distinguished Name):

   ```
    ldapsearch -x -H ldap://SERVER:389 -s base -b "" defaultNamingContext
   ```

2. Search User

   ```
   ldapsearch -x -H ldap://SERVER:389 -D 'BIND_DN' -W \
   -b 'BASE_DN' '(sAMAccountName=USER)' dn sAMAccountName
   ```

3. Search User's AD groups

   ```
   ldapsearch -x -H ldap://SERVER:389 -D 'BIND_DN' -W \
   -b 'BASE_DN' '(sAMAccountName=USER)' memberOf
   ```

4. Check DB2 Group retrieval

```
db2 "SELECT * FROM TABLE (SYSPROC.AUTH_LIST_GROUPS_FOR_AUTHID('HMK_MASTER\PYF522')) AS T"
```

5. Check Authentication parameters in config:

```
db2 get dbm cfg | egrep -i 'SRVCON_PW_PLUGIN|GROUP_PLUGIN|AUTHENTICATION|SRVCON_AUTH'
```

6. Check db2 grant:

```
db2 "SELECT GRANTEE, GRANTEETYPE, CONNECTAUTH FROM SYSCAT.DBAUTH where GRANTEE = 'DB2DB_ACCESS'"
```
