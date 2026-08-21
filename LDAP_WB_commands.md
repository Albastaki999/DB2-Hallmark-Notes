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