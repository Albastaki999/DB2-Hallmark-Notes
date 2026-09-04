# LDAP and Winbind Commands

gather info about AD environment using winbind

```
cat /etc/samba/smb.conf
```

```
wbinfo --own-domain
```

```
wbinfo --trusted-domains
```

```
wbinfo --online-status
```

```
wbinfo --domain-info=HMK_MASTER
```

Inspect the given cert

```
openssl x509 \
-in /tmp/excelsior11.pem \
-noout \
-subject \
-issuer \
-dates
```

Check your cert's key size and algo

```
openssl x509 -in /tmp/excelsior11.pem -noout -text | \
egrep 'Public-Key|Signature Algorithm'
```

See what certificate DC1 actually presents on 636

```
openssl s_client \
-connect awsmasterdc1.master.hmkad.hallmark.com:636 \
-servername awsmasterdc1.master.hmkad.hallmark.com \
-showcerts </dev/null
```

Explicitly verify against our Hallmark CA

```
openssl s_client \
-connect awsmasterdc1.master.hmkad.hallmark.com:636 \
-servername awsmasterdc1.master.hmkad.hallmark.com \
-CAfile /tmp/excelsior11.pem \
-verify_return_error </dev/null
```

Test LDAP over TLS

```
LDAPTLS_CACERT=/tmp/excelsior11.pem \
LDAPTLS_REQCERT=demand \
ldapsearch -x \
-H ldaps://awsmasterdc1.master.hmkad.hallmark.com:636 \
-s base \
-b "" \
defaultNamingContext dnsHostName
```
