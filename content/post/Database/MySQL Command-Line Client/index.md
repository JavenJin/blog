---
title: MySQL Command-Line Client
description: MySQL 命令行客户端
date: ''
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

- --help, -?

|**Command-Line Format**|**--help**|
|:--|--|

Display a help message and exit.

- --auto-rehash

|**Command-Line Format**|**--help**|
|:--|--|
|**Disabled by**|**skip-auto-rehash**|

Enable automatic rehashing. This option is on by default, which enables database, table, and column name completion. Use `--disable-auto-rehash` to disable rehashing. That causes **mysql** to start faster, but you must issue the rehash command or its \\# shortcut if you want to use name completion.

To complete a name, enter the first part and press Tab. If the name is unambiguous, **mysql** completes it. Otherwise, you can press Tab again to see the possible names that begin with what you have typed so far. Completion does not occur if there is no default database.

> **Note:** This feature requires a MySQL client that is compiled with the readline library. Typically, the readline library is not available on Windows.

// https://dev.mysql.com/doc/refman/8.0/en/mysql.html

// https://cloud.tencent.com/developer/ask/sof/114604