# PowerShell

**Find all rthe disabled Users**

```zsh
Get-ADUser -Filter 'Enabled -eq $false' -Properties Enabled
```

**Enable a users**

```zsh
Enable-ADAccount -Identity $USERNAME
```

**Get users identity**

```zsh
Get-ADUser -Identity $USERNAME
```
