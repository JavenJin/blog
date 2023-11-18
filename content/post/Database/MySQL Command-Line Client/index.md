---
title: MySQL Command-Line Client
description: MySQL 命令行客户端
date: '2023-11-18'
categories:
    - Database
tags:
    - Database
---

# MySQL Command-Line Client

**mysql** is a simple SQL shell with input line editing capabilities. It supports interactive and noninteractive use. When used interactively, query results are presented in an ASCII-table format. When used noninteractively (for example, as a filter), the result is presented in tab-separated format. The output format can be changed using command options.

If you have problems due to insufficient memory for large result sets, use the `--quick` option. This forces **mysql** to retrieve results from the server a row at a time rather than retrieving the entire result set and buffering it in memory before displaying it. This is done by returning the result set using the `mysql_use_result()` C API function in the client/server library rather than `mysql_store_result()`.

> **Note:** Alternatively, MySQL Shell offers access to the X DevAPI. For details, see [MySQL Shell 8.0](https://dev.mysql.com/doc/mysql-shell/8.0/en/).

Using **mysql** is very easy. Invoke it from the prompt of your command interpreter as follows:

```terminal
mysql db_name
```

Or:

```terminal
mysql --user=user_name --password db_name
```

In this case, you'll need to enter your password in response to the prompt that **mysql** displays:

```terminal
Enter password: your_password
```

Then type an SQL statement, end it with ;, \g, or \G and press Enter.

Typing **Control+C** interrupts the current statement if there is one, or cancels any partial input line otherwise.

You can execute SQL statements in a script file (batch file) like this:

```terminal
mysql db_name < script.sql > output.tab
```

On Unix, the mysql client logs statements executed interactively to a history file. See [mysql Client Logging](https://dev.mysql.com/doc/refman/8.0/en/mysql-logging.html).

## mysql Client Options

**mysql** supports the following options, which can be specified on the command line or in the `[mysql]` and `[client]` groups of an option file. For information about option files used by MySQL programs, see [Using Option Files](https://dev.mysql.com/doc/refman/8.0/en/option-files.html).

|Option Name|Description|Introduced|Deprecated|
|:--|--|--|--|
|--auto-rehash|Enable automatic rehashing|||
|--auto-vertical-output|Enable automatic vertical result set display|||
|--batch|Do not use history file|||		
|--binary-as-hex|Display binary values in hexadecimal notation|||	
|--binary-mode|Disable \r\n - to - \n translation and treatment of \0 as end-of-query|||	
|--bind-address|Use specified network interface to connect to MySQL Server|||
|--character-sets-dir|Directory where character sets are installed|||
|--column-names|Write column names in results|||
|--column-type-info|Display result set metadata|||
|--comments|Whether to retain or strip comments in statements sent to the server|||
|--compress|Compress all information sent between client and server||8.0.18|
|--compression-algorithms|Permitted compression algorithms for connections to server|8.0.18||
|--connect-expired-password|Indicate to server that client can handle expired-password sandbox mode|||
|--connect-timeout|Number of seconds before connection timeout|||
|--database|The database to use|||
|--debug|Write debugging log; supported only if MySQL was built with debugging support|||
|--debug-check|Print debugging information when program exits|||
|--debug-info|Print debugging information, memory, and CPU statistics when program exits|||
|--default-auth|Authentication plugin to use|||
|--default-character-set|Specify default character set|||
|--defaults-extra-file|Read named option file in addition to usual option files|||
|--defaults-file|Read only named option file|||
|--defaults-group-suffix|Option group suffix value|||
|--delimiter|Set the statement delimiter|||
|--dns-srv-name|Use DNS SRV lookup for host information|8.0.22||
|--enable-cleartext-plugin|Enable cleartext authentication plugin|||
|--execute|Execute the statement and quit|||
|--fido-register-factor|Multifactor authentication factors for which registration must be done|8.0.27|8.0.35|
|--force|Continue even if an SQL error occurs|||
|--get-server-public-key|Request RSA public key from server|||
|--help|Display help message and exit|||
|--histignore|Patterns specifying which statements to ignore for logging|||
|--host|Host on which MySQL server is located|||
|--html|Produce HTML output|||
|--ignore-spaces|Ignore spaces after function names|||
|--init-command|SQL statement to execute after connecting|||
|--line-numbers|Write line numbers for errors|||
|--load-data-local-dir|Directory for files named in LOAD DATA LOCAL statements|8.0.21||
|--local-infile|Enable or disable for LOCAL capability for LOAD DATA|||
|--login-path|Read login path options from .mylogin.cnf|||
|--max-allowed-packet|Maximum packet length to send to or receive from server|||
|--max-join-size|The automatic limit for rows in a join when using --safe-updates|||
|--named-commands|Enable named mysql commands|||
|--net-buffer-length|Buffer size for TCP/IP and socket communication|||
|--network-namespace|Specify network namespace|8.0.22||
|--no-auto-rehash|Disable automatic rehashing|||
|--no-beep|Do not beep when errors occur|||
|--no-defaults|Read no option files|||
|--oci-config-file|Defines an alternate location for the Oracle Cloud Infrastructure CLI configuration file.|8.0.27||	
|--one-database|Ignore statements except those for the default database named on the command line|||
|--pager|Use the given command for paging query output|||
|--password|Password to use when connecting to server|||
|--password1|First multifactor authentication password to use when connecting to server|8.0.27||
|--password2|Second multifactor authentication password to use when connecting to server|8.0.27||
|--password3|Third multifactor authentication password to use when connecting to server|8.0.27||
|--pipe|Connect to server using named pipe (Windows only)|||
|--plugin-authentication-kerberos-client-mode|Permit GSSAPI pluggable authentication through the MIT Kerberos library on Windows|8.0.32||
|--plugin-dir|Directory where plugins are installed|||
|--port|TCP/IP port number for connection|||
|--print-defaults|Print default options|||
|--prompt|Set the prompt to the specified format|||
|--protocol|Transport protocol to use|||
|--quick|Do not cache each query result|||
|--raw|Write column values without escape conversion|||
|--reconnect|If the connection to the server is lost, automatically try to reconnect|||
|--safe-updates, --i-am-a-dummy|Allow only UPDATE and DELETE statements that specify key values|||
|--select-limit|The automatic limit for SELECT statements when using --safe-updates|||
|--server-public-key-path|Path name to file containing RSA public key|||
|--shared-memory-base-name|Shared-memory name for shared-memory connections (Windows only)|||
|--show-warnings|Show warnings after each statement if there are any|||
|--sigint-ignore|Ignore SIGINT signals (typically the result of typing Control+C)|||
|--silent|Silent mode|||
|--skip-auto-rehash|Disable automatic rehashing|||
|--skip-column-names|Do not write column names in results|||
|--skip-line-numbers|Skip line numbers for errors|||
|--skip-named-commands|Disable named mysql commands|||
|--skip-pager|Disable paging|||
|--skip-reconnect|Disable reconnecting|||
|--socket|Unix socket file or Windows named pipe to use|||
|--ssl-ca|File that contains list of trusted SSL Certificate Authorities|||
|--ssl-capath|Directory that contains trusted SSL Certificate Authority certificate files|||
|--ssl-cert|File that contains X.509 certificate|||	
|--ssl-cipher|Permissible ciphers for connection encryption|||	
|--ssl-crl|File that contains certificate revocation lists|||
|--ssl-crlpath|Directory that contains certificate revocation-list files|||
|--ssl-fips-mode|Whether to enable FIPS mode on client side||8.0.34|
|--ssl-key|File that contains X.509 key|||
|--ssl-mode|Desired security state of connection to server|||
|--ssl-session-data|File that contains SSL session data|8.0.29||
|--ssl-session-data-continue-on-failed-reuse|Whether to establish connections if session reuse fails|8.0.29||
|--syslog|Log interactive statements to syslog|||
|--table|Display output in tabular format|||
|--tee|Append a copy of output to named file|||
|--tls-ciphersuites|Permissible TLSv1.3 ciphersuites for encrypted connections|8.0.16||
|--tls-version|Permissible TLS protocols for encrypted connections|||
|--unbuffered|Flush the buffer after each query|||
|--user|MySQL user name to use when connecting to server|||
|--verbose|Verbose mode|||
|--version|Display version information and exit|||
|--vertical|Print query output rows vertically (one line per column value)|||
|--wait|If the connection cannot be established, wait and retry instead of aborting|||
|--xml|Produce XML output|||
|--zstd-compression-level|Compression level for connections to server that use zstd compression|8.0.18||

### --help, -?

|**Command-Line Format**|**--help**|
|:--|--|

Display a help message and exit.

### --auto-rehash

|**Command-Line Format**|**--help**|
|:--|--|
|**Disabled by**|**skip-auto-rehash**|

Enable automatic rehashing. This option is on by default, which enables database, table, and column name completion. Use `--disable-auto-rehash` to disable rehashing. That causes **mysql** to start faster, but you must issue the rehash command or its \\# shortcut if you want to use name completion.

To complete a name, enter the first part and press Tab. If the name is unambiguous, **mysql** completes it. Otherwise, you can press Tab again to see the possible names that begin with what you have typed so far. Completion does not occur if there is no default database.

> **Note:** This feature requires a MySQL client that is compiled with the readline library. Typically, the readline library is not available on Windows.

### --auto-vertical-output

|**Command-Line Format**|**--auto-vertical-output**|
|:--|--|

Cause result sets to be displayed vertically if they are too wide for the current window, and using normal tabular format otherwise. (This applies to statements terminated by ; or \G.)

### --batch, -B

|**Command-Line Format**|**--batch**|
|:--|--|

Print results using tab as the column separator, with each row on a new line. With this option, **mysql** does not use the history file.

Batch mode results in nontabular output format and escaping of special characters. Escaping may be disabled by using raw mode; see the description for the `--raw` option.

### --binary-as-hex

|**Command-Line Format**|**--binary-as-hex**|
|:--|--|
|**Type**|**Boolean**|
|**Default Value(≥ 8.0.19)**|**FALSE in noninteractive mode**|
|**Default Value(≤ 8.0.18)**|**FALSE**|

When this option is given, **mysql** displays binary data using hexadecimal notation (0x*value*). This occurs whether the overall output display format is tabular, vertical, HTML, or XML.

`--binary-as-hex` when enabled affects display of all binary strings, including those returned by functions such as `CHAR()` and `UNHEX()`. The following example demonstrates this using the ASCII code for *A* (65 decimal, 41 hexadecimal):

- --binary-as-hex disabled:

```sql
mysql> SELECT CHAR(0x41), UNHEX('41');
+------------+-------------+
| CHAR(0x41) | UNHEX('41') |
+------------+-------------+
| A          | A           |
+------------+-------------+
```

- --binary-as-bex enabled:

```sql
mysql> SELECT CHAR(0x41), UNHEX('41');
+------------------------+--------------------------+
| CHAR(0x41)             | UNHEX('41')              |
+------------------------+--------------------------+
| 0x41                   | 0x41                     |
+------------------------+--------------------------+
```

To write a binary string expression so that it displays as a character string regardless of whether `--binary-as-hex` is enabled, use these techniques:

- The `CHAR()` function has a USING *charset* clause:

```sql
mysql> SELECT CHAR(0x41 USING utf8mb4);
+--------------------------+
| CHAR(0x41 USING utf8mb4) |
+--------------------------+
| A                        |
+--------------------------+
```

- More generally, use `CONVERT()` to convert an expression to a given character set:

```sql
mysql> SELECT CONVERT(UNHEX('41') USING utf8mb4);
+------------------------------------+
| CONVERT(UNHEX('41') USING utf8mb4) |
+------------------------------------+
| A                                  |
+------------------------------------+
```

As of MySQL 8.0.19, when **mysql** operates in interactive mode, this option is enabled by default. In addition, output from the status (or \s) command includes this line when the option is enabled implicitly or explicitly:

```
Binary data as: Hexadecimal
```

To disable hexadecimal notation, use `--skip-binary-as-hex`

### --binary-model

|**Command-Line Format**|**--binary-mode**|
|:--|--|

This option helps when processing **mysqlbinlog** output that may contain `BLOB` values. By default, **mysql** translates \r\n in statement strings to \n and interprets \0 as the statement terminator. `--binary-mode` disables both features. It also disables all **mysql** commands except *charset* and *delimiter* in noninteractive mode (for input piped to **mysql** or loaded using the source command).

### --bind-address=*ip_address*

|**Command-Line Format**|**--bind-address=ip_address**|
|:--|--|

On a computer having multiple network interfaces, use this option to select which interface to use for connecting to the MySQL server.

### --character-sets-dir=`dir_name`

|**Command-Line Format**|**--character-sets-dir=dir_name**|
|:--|--|
|**Type**|**Directory name**|

The directory where character sets are installed. See []"Character Set Configuration"](https://dev.mysql.com/doc/refman/8.0/en/charset-configuration.html).

### --column-names

|**Command-Line Format**|**--column-names**|
|:--|--|

Write column names in results.

### --column-type-info

|**Command-Line Format**|**--column-type-info**|
|:--|--|

Display result set metadata. This information corresponds to the contents of C API *MYSQL_FIELD* data structures. See [C API Basic Data Structures](https://dev.mysql.com/doc/c-api/8.0/en/c-api-data-structures.html).

### --comments, -c

|**Command-Line Format**|**--comments**|
|:--|--|
|**Type**|**Boolean**|
|**Default Value**|**FALSE**|

Whether to strip or preserve comments in statements sent to the server. The default is `--skip-comments` (strip comments), enable with `--comments` (preserve comments).

> **Note:** The **mysql** client always passes optimizer hints to the server, regardless of whether this option is given. Comment stripping is deprecated. Expect this feature and the options to control it to be removed in a future MySQL release.

### --compress, -C

|**Command-Line Format**|**--compress\[={OFF\|ON}\]**|
|:--|--|
|**Deprecated**|**8.0.18**|
|**Type**|**Boolean**|
|**Default Value**|**OFF**|

Compress all information sent between the client and the server if possible. See ["Connection Compression Control"](https://dev.mysql.com/doc/refman/8.0/en/connection-compression-control.html).

As of MySQL 8.0.18, this option is deprecated. Expect it to be removed in a future version of MySQL. See [Configuring Legacy Connection Compression](https://dev.mysql.com/doc/refman/8.0/en/connection-compression-control.html#connection-compression-legacy-configuration).

### --compression-algorithms=*value*

|**Command-Line Format**|**--compression-algorithms=value**|
|:--|--|
|**Deprecated**|**8.0.18**|
|**Type**|**Set**|
|**Default Value**|**uncompressed**|
|**Valid Values**|**zlib / zstd / uncompressed**|

The permitted compression algorithms for connections to the server. The available algorithms are the same as for the `protocol_compression_algorithms` system variable. The default value is *uncompressed*.

For more information, see ["Connection Compression Control"](https://dev.mysql.com/doc/refman/8.0/en/connection-compression-control.html).

This option was added in MySQL 8.0.18.

### --connect-expired-password

|**Command-Line Format**|**--connect-expired-password**|
|:--|--|

Indicate to the server that the client can handle sandbox mode if the account used to connect has an expired password. This can be useful for noninteractive invocations of **mysql** because normally the server disconnects noninteractive clients that attempt to connect using an account with an expired password. (See ["Server Handling of Expired Passwords"](https://dev.mysql.com/doc/refman/8.0/en/expired-password-handling.html).)

### --connect-timeout=*value*

|**Command-Line Format**|**--connect-timeout=value**|
|:--|--|
|**Type**|**Numeric**|
|**Default Value**|**0**|

The number of seconds before connection timeout. (Default value is 0.)

### --database=*db_name*, -D *db_name*

|**Command-Line Format**|**--database=dbname**|
|:--|--|
|**Type**|**String**|

The database to use. This is useful primarily in an option file.

### --debug \[=*debug_options*\], -# \[*debug_options*\]

|**Command-Line Format**|**--debug\[=debug_options\]**|
|:--|--|
|**Type**|**String**|
|**Default Value**|**d:t:o,/tmp/mysql.trace**|

Write a debugging log. A typical *debug_options* string is d:t:o,*file_name*. The default is d:t:o,/tmp/mysql.trace.

This option is available only if MySQL was built using `WITH_DEBUG`. MySQL release binaries provided by Oracle are not built using this option.

### --debug-check

|**Command-Line Format**|**--debug-check**|
|:--|--|
|**Type**|**Boolean**|
|**Default Value**|**FALSE**|

Print some debugging information when the program exits.

This option is available only if MySQL was built using `WITH_DEBUG`. MySQL release binaries provided by Oracle are not built using this option.

### --debug-info, -T

|**Command-Line Format**|**--debug-info**|
|:--|--|
|**Type**|**Boolean**|
|**Default Value**|**FALSE**|

Print debugging information and memory and CPU usage statistics when the program exits.

This option is available only if MySQL was built using `WITH_DEBUG`. MySQL release binaries provided by Oracle are not built using this option.

### --default-auth=*plugin*

|**Command-Line Format**|**--default-auth=plugin**|
|:--|--|
|**Type**|**String**|

A hint about which client-side authentication plugin to use. See ["Pluggable Authentication"](https://dev.mysql.com/doc/refman/8.0/en/pluggable-authentication.html).

### --default-character-set=*charset_name*

|**Command-Line Format**|**--default-character-set=charset_name**|
|:--|--|
|**Type**|**String**|

Use *charset_name* as the default character set for the client and connection.

This option can be useful if the operating system uses one character set and the **mysql** client by default uses another. In this case, output may be formatted incorrectly. You can usually fix such issues by using this option to force the client to use the system character set instead.

For more information, see ["Connection Character Sets and Collations"](https://dev.mysql.com/doc/refman/8.0/en/charset-connection.html), and ["Character Set Configuration"](https://dev.mysql.com/doc/refman/8.0/en/charset-configuration.html).

### --defaults-extra-file=*file-name*

|**Command-Line Format**|**--defaults-extra-file=file_name**|
|:--|--|
|**Type**|**File name**|

Read this option file after the global option file but (on Unix) before the user option file. If the file does not exist or is otherwise inaccessible, an error occurs. If *file_name* is not an absolute path name, it is interpreted relative to the current directory.

For additional information about this and other option-file options, see ["Command-Line Options that Affect Option-File Handling"](https://dev.mysql.com/doc/refman/8.0/en/option-file-options.html).

### --defaults-file=*file_name*

|**Command-Line Format**|**--defaults-file=file_name**|
|:--|--|
|**Type**|**File name**|

Use only the given option file. If the file does not exist or is otherwise inaccessible, an error occurs. If *file_name* is not an absolute path name, it is interpreted relative to the current directory.

Exception: Even with `--defaults-file`, client programs read .mylogin.cnf.

For additional information about this and other option-file options, see ["Command-Line Options that Affect Option-File Handling"](https://dev.mysql.com/doc/refman/8.0/en/option-file-options.html).

### --defaults-group-suffix=*str*

|**Command-Line Format**|**--defaults-group-suffix=str**|
|:--|--|
|**Type**|**String**|

Read not only the usual option groups, but also groups with the usual names and a suffix of str. For example, **mysql** normally reads the `[client]` and `[mysql]` groups. If this option is given as `--defaults-group-suffix=_other`, **mysql** also reads the [client_other] and `[mysql_other]` groups.

For additional information about this and other option-file options, see ["Command-Line Options that Affect Option-File Handling"](https://dev.mysql.com/doc/refman/8.0/en/option-file-options.html).

### --delimiter=*str*

|**Command-Line Format**|**--delimiter=str**|
|:--|--|
|**Type**|**String**|
|**Default Value**|**;**|

Set the statement delimiter. The default is the semicolon character (;).

### --disable-named-commands

Disable named commands. Use the \\* form only, or use named commands only at the beginning of a line ending with a semicolon (;). **mysql** starts with this option *enabled* by default. However, even with this option, long-format commands still work from the first line. See ["mysql Client Commands"](https://dev.mysql.com/doc/refman/8.0/en/mysql-commands.html).

### --dns-srv-name=*name*

|**Command-Line Format**|**--dns-srv-name=name**|
|:--|--|
|**Introduced**|**8.0.22**|
|**Type**|**String**|

Specifies the name of a DNS SRV record that determines the candidate hosts to use for establishing a connection to a MySQL server. For information about DNS SRV support in MySQL, see ["Connecting to the Server Using DNS SRV Records"](https://dev.mysql.com/doc/refman/8.0/en/connecting-using-dns-srv.html).

Suppose that DNS is configured with this SRV information for the *example.com* domain:

```simple
Name                     TTL   Class   Priority Weight Port Target
_mysql._tcp.example.com. 86400 IN SRV  0        5      3306 host1.example.com
_mysql._tcp.example.com. 86400 IN SRV  0        10     3306 host2.example.com
_mysql._tcp.example.com. 86400 IN SRV  10       5      3306 host3.example.com
_mysql._tcp.example.com. 86400 IN SRV  20       5      3306 host4.example.com
```

To use that DNS SRV record, invoke **mysql** like this:

```terminal
mysql --dns-srv-name=_mysql._tcp.example.com
```

**mysql** then attempts a connection to each server in the group until a successful connection is established. A failure to connect occurs only if a connection cannot be established to any of the servers. The priority and weight values in the DNS SRV record determine the order in which servers should be tried.

When invoked with `--dns-srv-name`, **mysql** attempts to establish TCP connections only.

The `--dns-srv-name` option takes precedence over the `--host` option if both are given. `--dns-srv-name` causes connection establishment to use the `mysql_real_connect_dns_srv()` C API function rather than `mysql_real_connect()`. However, if the *connect* command is subsequently used at runtime and specifies a host name argument, that host name takes precedence over any `--dns-srv-name` option given at **mysql** startup to specify a DNS SRV record.

This option was added in MySQL 8.0.22.

### --enable-cleartext-plugin

|**Command-Line Format**|**--enable-cleartext-plugin**|
|:--|--|
|**Type**|**Boolean**|
|**Default Value**|**FALSE**|

Enable the *mysql_clear_password* cleartext authentication plugin. (See ["Client-Side Cleartext Pluggable Authentication"](https://dev.mysql.com/doc/refman/8.0/en/cleartext-pluggable-authentication.html).)

### --execute=*statement*, -e *statement*

|**Command-Line Format**|**--execute=statement**|
|:--|--|
|**Type**|**String**|

Execute the statement and quit. The default output format is like that produced with `--batch`. See ["Using Options on the Command Line"](https://dev.mysql.com/doc/refman/8.0/en/command-line-options.html), for some examples. With this option, **mysql** does not use the history file.

### --fido-register-factor=*value*

|**Command-Line Format**|**--fido-register-factor=value**|
|:--|--|
|**Introduced**|**8.0.27**|
|**Deprecated**|**8.0.35**|
|**Type**|**String**|

> **Note:** As of MySQL 8.0.35, this option is deprecated and subject to removal in a future MySQL release.

The factor or factors for which FIDO device registration must be performed. This option value must be a single value, or two values separated by commas. Each value must be 2 or 3, so the permitted option values are '2', '3', '2,3' and '3,2'.

For example, an account that requires registration for a 3rd authentication factor invokes the **mysql** client as follows:

```terminal
mysql --user=user_name --fido-register-factor=3
```

An account that requires registration for a 2nd and 3rd authentication factor invokes the **mysql** client as follows:

```terminal
mysql --user=user_name --fido-register-factor=2,3
```

If registration is successful, a connection is established. If there is an authentication factor with a pending registration, a connection is placed into pending registration mode when attempting to connect to the server. In this case, disconnect and reconnect with the correct `--fido-register-factor` value to complete the registration.

Registration is a two step process comprising *initiate registration* and *finish registration* steps. The initiate registration step executes this statement:

```sql
ALTER USER user factor INITIATE REGISTRATION
```

The statement returns a result set containing a 32 byte challenge, the user name, and the relying party ID (see "["authentication_fido_rp_id"](https://dev.mysql.com/doc/refman/8.0/en/pluggable-authentication-system-variables.html#sysvar_authentication_fido_rp_id)").

The finish registration step executes this statement:

```sql
ALTER USER user factor FINISH REGISTRATION SET CHALLENGE_RESPONSE AS 'auth_string'
```

The statement completes the registration and sends the following information to the server as part of the *auth_string*: authenticator data, an optional attestation certificate in X.509 format, and a signature.

The initiate and registration steps must be performed in a single connection, as the challenge received by the client during the initiate step is saved to the client connection handler. Registration would fail if the registration step was performed by a different connection. The `--fido-register-factor` option executes both the initiate and registration steps, which avoids the failure scenario described above and prevents having to execute the `ALTER USER` initiate and registration statements manually.

The `--fido-register-factor` option is only available for the **mysql** client and MySQL Shell. Other MySQL client programs do not support it.

For related information, see ["Using FIDO Authentication"](https://dev.mysql.com/doc/refman/8.0/en/fido-pluggable-authentication.html#fido-pluggable-authentication-usage).

### force, -f

|**Command-Line Format**|**--force**|
|:--|--|

Continue even if an SQL error occurs.

### --get-server-public-key

|**Command-Line Format**|**--get-server-public-key**|
|:--|--|
|**Type**|**Boolean**|

Request from the server the public key required for RSA key pair-based password exchange. This option applies to clients that authenticate with the *caching_sha2_password* authentication plugin. For that plugin, the server does not send the public key unless requested. This option is ignored for accounts that do not authenticate with that plugin. It is also ignored if RSA-based password exchange is not used, as is the case when the client connects to the server using a secure connection.

If `--server-public-key-path=file_name` is given and specifies a valid public key file, it takes precedence over `--get-server-public-key`.

For information about the *caching_sha2_password* plugin, see ["Caching SHA-2 Pluggable Authentication"](https://dev.mysql.com/doc/refman/8.0/en/caching-sha2-pluggable-authentication.html).

### --histignore

|**Command-Line Format**|**--histignore=pattern_list**|
|:--|--|
|**Type**|**String**|

A list of one or more colon-separated patterns specifying statements to ignore for logging purposes. These patterns are added to the default pattern list ("\*IDENTIFIED\*:\*PASSWORD\*"). The value specified for this option affects logging of statements written to the history file, and to syslog if the `--syslog` option is given. For more information, see ["mysql Client Logging"](https://dev.mysql.com/doc/refman/8.0/en/mysql-logging.html).

### --host=*host_name*, -h *host_name*

|**Command-Line Format**|**--host=host_name**|
|:--|--|
|**Type**|**String**|
|**Default Value**|**localhost**|

Connect to the MySQL server on the given host.

The `--dns-srv-name` option takes precedence over the `--host` option if both are given. `--dns-srv-name` causes connection establishment to use the `mysql_real_connect_dns_srv()` C API function rather than `mysql_real_connect()`. However, if the connect command is subsequently used at runtime and specifies a host name argument, that host name takes precedence over any `--dns-srv-name` option given at **mysql** startup to specify a DNS SRV record.

### --html, -H

|**Command-Line Format**|**--html**|
|:--|--|

Produce HTML output.




// https://dev.mysql.com/doc/refman/8.0/en/mysql.html

// https://cloud.tencent.com/developer/ask/sof/114604