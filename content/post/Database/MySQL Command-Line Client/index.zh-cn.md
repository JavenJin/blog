---
title: MySQL 命令行客户端
description: MySQL Command-Line Client
date: '2023-11-21'
categories:
    - Database
tags:
    - Database
---

# MySQL 命令行客户端

**mysql** 是一个简单的 SQL shell，具有输入行编辑功能。它支持交互式和非交互式使用。交互式使用时，查询结果以 ASCII 表格格式显示。非交互式使用时（例如，作为过滤器），结果以制表符分隔的格式显示。输出格式可以通过命令选项进行更改。

如果因内存不足而无法处理大型结果集，请使用 `--quick` 选项。这会强制**mysql**每次从服务器检索一行结果，而不是检索整个结果集，并在显示之前将其缓冲在内存中。具体做法是使用客户端/服务器库中的 `mysql_use_result()` C API 函数而不是 `mysql_store_result()`来返回结果集。

> **注意：** 另外，MySQL Shell 还提供对 X DevAPI 的访问。有关详情，请参阅 [MySQL Shell 8.0](https://dev.mysql.com/doc/mysql-shell/8.0/en/)。

使用 **mysql** 非常简单。在命令解释器的提示符下调用它，如下所示：

```terminal
mysql db_name
```

或者：

```terminal
mysql --user=user_name --password db_name
```

在这种情况下，您需要根据 **mysql** 显示的提示输入密码：

```terminal
Enter password: your_password
```

然后键入一条 SQL 语句，以 ;、\g 或 \G 结尾并按 Enter。

如果有当前语句，键入 **Control+C** 会中断该语句，否则会取消任何部分输入行。

您可以像这样在脚本文件（批处理文件）中执行 SQL 语句：

```terminal
mysql db_name < script.sql > output.tab
```

在 Unix 上，mysql 客户端会将交互执行的语句记录到历史文件中。请参阅 [mysql 客户端日志](https://dev.mysql.com/doc/refman/8.0/en/mysql-logging.html)。

## mysql 客户端选项

**mysql** supports the following options, which can be specified on the command line or in the `[mysql]` and `[client]` groups of an option file. For information about option files used by MySQL programs, see [Using Option Files](https://dev.mysql.com/doc/refman/8.0/en/option-files.html).

**mysql**支持以下选项，这些选项可以在命令行或选项文件的`[mysql]`和`[client]`组中指定。有关 MySQL 程序使用的选项文件的信息，请参阅 [Using Option Files](https://dev.mysql.com/doc/refman/8.0/en/option-files.html)。

|选项名称|说明|引入版本|废弃版本|
|:--|--|--|--|
|\-\-auto-rehash|启用自动重新哈希|||
|\-\-auto-vertical-output|启用自动垂直结果集显示|||
|\-\-batch|不使用历史记录文件|||		
|\-\-binary-as-hex|以十六进制显示二进制值|||	
|\-\-binary-mode|禁用 \r \n 到 -n 转换和将 \0 视为查询结束|||	
|\-\-bind-address|使用指定的网络接口连接 MySQL Server|||
|\-\-character-sets-dir|安装字符集的目录|||
|\-\-column-names|在结果中写入列名|||
|\-\-column-type-info|显示结果集元数据|||
|\-\-comments|是否保留或删除发送到服务器的语句中的注释|||
|\-\-compress|压缩客户端和服务器之间发送的所有信息||8.0.18|
|\-\-compression-algorithms|用于连接服务器的允许压缩算法|8.0.18||
|\-\-connect-expired-password|指示服务器客户端可以处理过期密码沙箱模式|||
|\-\-connect-timeout|连接超时之前的秒数|||
|\-\-database|要使用的数据库|||
|\-\-debug|编写调试日志；仅当MySQL使用调试支持构建时才受支持|||
|\-\-debug-check|程序退出时打印调试信息|||
|\-\-debug-info|程序退出时打印调试信息，内存和CPU统计信息|||
|\-\-default-auth|身份验证插件使用|||
|\-\-default-character-set|指定默认字符集|||
|\-\-defaults-extra-file|除了通常的选项文件，还读取命名的选项文件|||
|\-\-defaults-file|只读命名的选项文件|||
|\-\-defaults-group-suffix|选项组后缀值|||
|\-\-delimiter|设置语句定界符|||
|\-\-dns-srv-name|使用 DNS SRV 查找主机信息|8.0.22||
|\-\-enable-cleartext-plugin|启用明文身份验证插件|||
|\-\-execute|执行语句并退出|||
|\-\-fido-register-factor|必须进行注册的多因素身份验证因素|8.0.27|8.0.35|
|\-\-force|即使发生SQL错误，也要继续|||
|\-\-get-server-public-key|从服务器请求RSA公钥|||
|\-\-help|显示帮助信息并退出|||
|\-\-histignore|模式指定日志记录要忽略的语句|||
|\-\-host|MySQL服务器所在的主机|||
|\-\-html|生成 HTML 输出|||
|\-\-ignore-spaces|忽略函数名称后的空格|||
|\-\-init-command|连接后执行的SQL语句|||
|\-\-line-numbers|输入行号以查找错误|||
|\-\-load-data-local-dir|LOAD DATA LOCAL 语句中命名的文件目录|8.0.21||
|\-\-local-infile|启用或禁用LOAD DATA的LOCAL功能|||
|\-\-login-path|从.mylogin.cnf中读取登录路径选项|||
|\-\-max-allowed-packet|发送到服务器或从服务器接收的最大数据包长度|||
|\-\-max-join-size|使用\-\-safe-updates时联接中行的自动限制|||
|\-\-named-commands|启用命名的mysql命令|||
|\-\-net-buffer-length|TCP/IP和套接字通信的缓冲区大小|||
|\-\-network-namespace|指定网络命名空间|8.0.22||
|\-\-no-auto-rehash|禁用自动重新哈希|||
|\-\-no-beep|发生错误时不发出蜂鸣声|||
|\-\-no-defaults|不读取选项文件|||
|\-\-oci-config-file|定义 Oracle 云计算基础架构 CLI 配置文件的备用位置。|8.0.27||	
|\-\-one-database|忽略命令行中指定的默认数据库的语句以外的语句|||
|\-\-pager|使用给定命令进行分页查询输出|||
|\-\-password|连接服务器时使用的密码|||
|\-\-password1|连接服务器时使用的第一个多因素身份验证密码|8.0.27||
|\-\-password2|连接服务器时使用的第二个多因素身份验证密码|8.0.27||
|\-\-password3|连接服务器时使用的第三个多因素身份验证密码|8.0.27||
|\-\-pipe|使用命名管道连接到服务器（仅Windows）|||
|\-\-plugin-authentication-kerberos-client-mode|允许通过 Windows 上的 MIT Kerberos 库进行 GSSAPI 可插拔身份验证|8.0.32||
|\-\-plugin-dir|安装插件的目录|||
|\-\-port|用于连接的TCP/IP端口号|||
|\-\-print-defaults|打印默认选项|||
|\-\-prompt|将提示设置为指定格式|||
|\-\-protocol|使用的连接协议|||
|\-\-quick|不要缓存每个查询结果|||
|\-\-raw|写入列值而不进行转义转换|||
|\-\-reconnect|如果与服务器的连接丢失，则自动尝试重新连接|||
|\-\-safe-updates, \-\-i-am-a-dummy|仅允许指定键值的UPDATE和DELETE语句|||
|\-\-select-limit|使用\-\-safe-updates时SELECT语句的自动限制|||
|\-\-server-public-key-path|包含RSA公钥的文件的路径名|||
|\-\-shared-memory-base-name|共享内存连接的共享内存名称（仅限 Windows）|||
|\-\-show-warnings|在每条语句后显示警告（如果有的话）|||
|\-\-sigint-ignore|忽略 SIGINT 信号（通常是输入 Control+C 的结果）|||
|\-\-silent|静音模式|||
|\-\-skip-auto-rehash|禁用自动重新哈希|||
|\-\-skip-column-names|不要在结果中写入列名|||
|\-\-skip-line-numbers|跳过行号以获取错误|||
|\-\-skip-named-commands|禁用命名的mysql命令|||
|\-\-skip-pager|禁用分页|||
|\-\-skip-reconnect|禁用重新连接|||
|\-\-socket|Unix套接字文件或Windows命名管道使用|||
|\-\-ssl-ca|包含受信任的SSL证书颁发机构列表的文件|||
|\-\-ssl-capath|包含受信任的SSL证书颁发机构证书文件的目录|||
|\-\-ssl-cert|包含X.509证书的文件|||	
|\-\-ssl-cipher|连接加密的允许密码|||	
|\-\-ssl-crl|包含证书吊销列表的文件|||
|\-\-ssl-crlpath|包含证书吊销列表文件的目录|||
|\-\-ssl-fips-mode|是否在客户端启用FIPS模式||8.0.34|
|\-\-ssl-key|包含X.509密钥的文件|||
|\-\-ssl-mode|与服务器连接的所需安全状态|||
|\-\-ssl-session-data|包含 SSL 会话数据的文件|8.0.29||
|\-\-ssl-session-data-continue-on-failed-reuse|会话重用失败时是否建立连接|8.0.29||
|\-\-syslog|将交互式语句记录到syslog|||
|\-\-table|以表格格式显示输出结果|||
|\-\-tee|将输出副本附加到命名文件中|||
|\-\-tls-ciphersuites|允许用于加密连接的 TLSv1.3 密码套件|8.0.16||
|\-\-tls-version|允许的加密连接 TLS 协议|||
|\-\-unbuffered|每次查询后清空缓冲区|||
|\-\-user|连接服务器时使用的 MySQL 用户名|||
|\-\-verbose|详细模式|||
|\-\-version|显示版本信息并退出|||
|\-\-vertical|垂直打印查询输出行（每列值一行）|||
|\-\-wait|如果无法建立连接，请等待并重试，而不是终止连接|||
|\-\-xml|生成 XML 输出|||
|\-\-zstd-compression-level|使用 zstd 压缩的服务器连接的压缩级别|8.0.18||

### \-\-help, -?

|**Command-Line Format**|**\-\-help**|
|:--|--|

显示帮助信息并退出。

### \-\-auto-rehash

|**Command-Line Format**|**\-\-auto-rehash**|
|:--|--|
|**Disabled by**|**skip-auto-rehash**|

Enable automatic rehashing. This option is on by default, which enables database, table, and column name completion. Use `--disable-auto-rehash` to disable rehashing. That causes **mysql** to start faster, but you must issue the rehash command or its \\# shortcut if you want to use name completion.

启用自动哈希。该选项默认为开启，可启用数据库、表和列名补全。使用`--disable-auto-rehash`禁用哈希。这会使 **mysql** 启动得更快，但如果你想使用名称补全，就必须发出 rehash 命令或其快捷方式。

要补全名称，请输入第一部分并按 Tab 键。如果名称不明确，**mysql** 将完成它。否则，您可以再次按 Tab 键，查看以您目前键入的内容开头的可能名称。如果没有默认数据库，则不会完成。

> **注意：** 此功能需要使用 readline 库编译的 MySQL 客户端。通常情况下，Windows 上没有 readline 库。

### \-\-auto-vertical-output

|**Command-Line Format**|**\-\-auto-vertical-output**|
|:--|--|

如果结果集对于当前窗口来说太宽，则使其垂直显示，否则使用正常的表格格式。（这适用于以 ; 或 \G 结束的语句）。

### \-\-batch, -B

|**Command-Line Format**|**\-\-batch**|
|:--|--|

使用制表符作为列分隔符打印结果，每行打印一行。使用该选项后，**mysql** 不会使用历史文件。

批处理模式会导致非表格输出格式和特殊字符转义。使用原始模式可以禁用转义；请参阅`--raw`选项的说明。

### \-\-binary-as-hex

|**Command-Line Format**|**\-\-binary-as-hex**|
|:--|--|
|**Type**|**Boolean**|
|**Default Value(≥ 8.0.19)**|**FALSE in noninteractive mode**|
|**Default Value(≤ 8.0.18)**|**FALSE**|

给定该选项后，**mysql** 将使用十六进制符号（0x*value*）显示二进制数据。无论整体输出显示格式是表格、垂直、HTML 还是 XML，都会出现这种情况。

启用 `--binary-as-hex` 后，将影响所有二进制字符串的显示，包括那些由 `CHAR()` 和 `UNHEX()` 等函数返回的字符串。下面的示例使用 *A* 的 ASCII 码（十进制 65 位，十六进制 41 位）进行了演示：

- 禁用`--binary-as-hex`:

```sql
mysql> SELECT CHAR(0x41), UNHEX('41');
+------------+-------------+
| CHAR(0x41) | UNHEX('41') |
+------------+-------------+
| A          | A           |
+------------+-------------+
```

- 启用`--binary-as-hex`:

```sql
mysql> SELECT CHAR(0x41), UNHEX('41');
+------------------------+--------------------------+
| CHAR(0x41)             | UNHEX('41')              |
+------------------------+--------------------------+
| 0x41                   | 0x41                     |
+------------------------+--------------------------+
```

要编写二进制字符串表达式，使其无论是否启用`--binary-as-hex`都能显示为字符串，请使用以下技巧：

- 函数 `CHAR()` 有一个 USING *charset* 子句：

```sql
mysql> SELECT CHAR(0x41 USING utf8mb4);
+--------------------------+
| CHAR(0x41 USING utf8mb4) |
+--------------------------+
| A                        |
+--------------------------+
```

- 更一般地说，使用 `CONVERT()` 可以将表达式转换为给定的字符集：

```sql
mysql> SELECT CONVERT(UNHEX('41') USING utf8mb4);
+------------------------------------+
| CONVERT(UNHEX('41') USING utf8mb4) |
+------------------------------------+
| A                                  |
+------------------------------------+
```

从MySQL 8.0.19开始，当**mysql**在交互模式下运行时，默认启用该选项。此外，在隐式或显式启用该选项时，status（或 \s）命令的输出也会包含这一行：

```
Binary data as: Hexadecimal
```

要禁用十六进制符号，请使用 `--skip-binary-as-hex`

### \-\-binary-model

|**Command-Line Format**|**\-\-binary-mode**|
|:--|--|

该选项有助于处理可能包含`BLOB`值的**mysqlbinlog**输出。默认情况下，**mysql**会将语句字符串中的\r\n翻译成\n，并将\0解释为语句结束符。`--binary-mode`禁用了这两个功能。在非交互模式下，除了 *charset* 和 *delimiter* 之外，它还禁用了所有 **mysql** 命令（对于通过管道输入到 **mysql** 或使用源代码命令加载的输入）。

### \-\-bind-address=*ip_address*

|**Command-Line Format**|**\-\-bind-address=ip_address**|
|:--|--|

在有多个网络接口的计算机上，使用此选项选择用于连接 MySQL 服务器的接口。

### \-\-character-sets-dir=`dir_name`

|**Command-Line Format**|**\-\-character-sets-dir=dir_name**|
|:--|--|
|**Type**|**Directory name**|

安装字符集的目录。请参阅["Character Set Configuration"](https://dev.mysql.com/doc/refman/8.0/en/charset-configuration.html)。

### \-\-column-names

|**Command-Line Format**|**\-\-column-names**|
|:--|--|

在结果中写入列名。

### \-\-column-type-info

|**Command-Line Format**|**\-\-column-type-info**|
|:--|--|

显示结果集元数据。这些信息与 C API *MYSQL_FIELD* 数据结构的内容相对应。请参阅 [C API Basic Data Structures](https://dev.mysql.com/doc/c-api/8.0/en/c-api-data-structures.html)。

### \-\-comments, -c

|**Command-Line Format**|**\-\-comments**|
|:--|--|
|**Type**|**Boolean**|
|**Default Value**|**FALSE**|

在发送到服务器的语句中剥离或保留注释。默认值是 `-skip-comments`（去除注释），启用时使用 `-comments`（保留注释）。

> **注意：** 无论是否给出此选项，**mysql** 客户端都会将优化器提示传递给服务器。注释剥离已被弃用。预计在未来的 MySQL 版本中，该功能和控制该功能的选项将被移除。

### \-\-compress, -C

|**Command-Line Format**|**\-\-compress\[={OFF\|ON}\]**|
|:--|--|
|**Deprecated**|**8.0.18**|
|**Type**|**Boolean**|
|**Default Value**|**OFF**|

尽可能压缩客户端与服务器之间发送的所有信息。请参阅["Connection Compression Control"](https://dev.mysql.com/doc/refman/8.0/en/connection-compression-control.html)。

自 MySQL 8.0.18 起，该选项已被弃用。预计未来的 MySQL 版本将删除该选项。请参阅 [Configuring Legacy Connection Compression](https://dev.mysql.com/doc/refman/8.0/en/connection-compression-control.html#connection-compression-legacy-configuration)。

### \-\-compression-algorithms=*value*

|**Command-Line Format**|**\-\-compression-algorithms=value**|
|:--|--|
|**Deprecated**|**8.0.18**|
|**Type**|**Set**|
|**Default Value**|**uncompressed**|
|**Valid Values**|**zlib / zstd / uncompressed**|

与服务器连接时允许使用的压缩算法。可用算法与 `protocol_compression_algorithms` 系统变量相同。默认值为 *uncompressed*。

更多信息，请参阅["Connection Compression Control"](https://dev.mysql.com/doc/refman/8.0/en/connection-compression-control.html)。

此选项在 MySQL 8.0.18 中添加。

### \-\-connect-expired-password

|**Command-Line Format**|**\-\-connect-expired-password**|
|:--|--|

如果用于连接的账户密码已过期，则向服务器表明客户端可以处理沙箱模式。这对非交互式调用 **mysql** 很有用，因为通常情况下，服务器会断开试图使用密码过期账户进行连接的非交互式客户端。（请参阅["Server Handling of Expired Passwords"](https://dev.mysql.com/doc/refman/8.0/en/expired-password-handling.html)）。

### \-\-connect-timeout=*value*

|**Command-Line Format**|**\-\-connect-timeout=value**|
|:--|--|
|**Type**|**Numeric**|
|**Default Value**|**0**|

连接超时前的秒数。（默认值为 0）。

### \-\-database=*db_name*, -D *db_name*

|**Command-Line Format**|**\-\-database=dbname**|
|:--|--|
|**Type**|**String**|

要使用的数据库。这主要在选项文件中有用。

### \-\-debug \[=*debug_options*\], -# \[*debug_options*\]

|**Command-Line Format**|**\-\-debug\[=debug_options\]**|
|:--|--|
|**Type**|**String**|
|**Default Value**|**d:t:o,/tmp/mysql.trace**|

编写调试日志。典型的 *debug_options* 字符串为 d:t:o,*file_name*。默认值为 d:t:o,/tmp/mysql.trace。

只有在使用`WITH_DEBUG`构建 MySQL 时，该选项才可用。Oracle 提供的 MySQL 发行版二进制文件不使用此选项构建。

### \-\-debug-check

|**Command-Line Format**|**\-\-debug-check**|
|:--|--|
|**Type**|**Boolean**|
|**Default Value**|**FALSE**|

在程序退出时打印一些调试信息。

只有在使用`WITH_DEBUG`构建 MySQL 时，该选项才可用。Oracle 提供的 MySQL 发行版二进制文件不使用此选项构建。

### \-\-debug-info, -T

|**Command-Line Format**|**\-\-debug-info**|
|:--|--|
|**Type**|**Boolean**|
|**Default Value**|**FALSE**|

在程序退出时打印调试信息以及内存和 CPU 使用率统计信息。

只有在使用`WITH_DEBUG`构建 MySQL 时，该选项才可用。Oracle 提供的 MySQL 发行版二进制文件不使用此选项构建。

### \-\-default-auth=*plugin*

|**Command-Line Format**|**\-\-default-auth=plugin**|
|:--|--|
|**Type**|**String**|

关于使用哪个客户端身份验证插件的提示。请参阅["Pluggable Authentication"](https://dev.mysql.com/doc/refman/8.0/en/pluggable-authentication.html)。

### \-\-default-character-set=*charset_name*

|**Command-Line Format**|**\-\-default-character-set=charset_name**|
|:--|--|
|**Type**|**String**|

使用 *charset_name* 作为客户端和连接的默认字符集。

如果操作系统使用一种字符集，而 **mysql** 客户端默认使用另一种字符集，则该选项会很有用。在这种情况下，输出的格式可能不正确。使用该选项强制客户端使用系统字符集，通常可以解决此类问题。

更多信息，请参阅["Connection Character Sets and Collations"](https://dev.mysql.com/doc/refman/8.0/en/charset-connection.html) 和["Character Set Configuration"](https://dev.mysql.com/doc/refman/8.0/en/charset-configuration.html)。

### \-\-defaults-extra-file=*file-name*

|**Command-Line Format**|**\-\-defaults-extra-file=file_name**|
|:--|--|
|**Type**|**File name**|

在全局选项文件之后、用户选项文件之前（在 Unix 上）读取该选项文件。如果文件不存在或无法访问，则会出错。如果 *file_name* 不是绝对路径名，则解释为相对于当前目录。

有关该选项和其他选项文件选项的更多信息，请参阅["Command-Line Options that Affect Option-File Handling"](https://dev.mysql.com/doc/refman/8.0/en/option-file-options.html)。

### \-\-defaults-file=*file_name*

|**Command-Line Format**|**\-\-defaults-file=file_name**|
|:--|--|
|**Type**|**File name**|

只使用给定的选项文件。如果文件不存在或无法访问，则会出错。如果 *file_name* 不是绝对路径名，则解释为相对于当前目录。

异常： 即使使用 `--defaults-file`，客户端程序也会读取 .mylogin.cnf。

有关该选项和其他选项文件选项的更多信息，请参阅["Command-Line Options that Affect Option-File Handling"](https://dev.mysql.com/doc/refman/8.0/en/option-file-options.html)。

### \-\-defaults-group-suffix=*str*

|**Command-Line Format**|**\-\-defaults-group-suffix=str**|
|:--|--|
|**Type**|**String**|

不仅读取通常的选项组，也读取通常名称和后缀为 str 的组。例如，**mysql** 通常读取`[client]`和`[mysql]`组。如果将此选项设置为 `--defaults-group-suffix=_other`，**mysql** 也会读取 `[client_other]` 和 `[mysql_other]` 组。

有关该选项和其他选项文件选项的更多信息，请参阅["Command-Line Options that Affect Option-File Handling"](https://dev.mysql.com/doc/refman/8.0/en/option-file-options.html)。

### \-\-delimiter=*str*

|**Command-Line Format**|**\-\-delimiter=str**|
|:--|--|
|**Type**|**String**|
|**Default Value**|**;**|

设置语句分隔符。默认为分号（;）。

### \-\-disable-named-commands

禁用命名命令。只使用 \\* 形式，或只在以分号（;）结尾的行首使用命名命令。默认情况下，**mysql**启动时该选项已*enabled*。不过，即使使用该选项，长格式命令仍可从第一行开始执行。参见["mysql Client Commands"](https://dev.mysql.com/doc/refman/8.0/en/mysql-commands.html)。

### \-\-dns-srv-name=*name*

|**Command-Line Format**|**\-\-dns-srv-name=name**|
|:--|--|
|**Introduced**|**8.0.22**|
|**Type**|**String**|

指定 DNS SRV 记录的名称，该记录用于确定与 MySQL 服务器建立连接时要使用的候选主机。有关 MySQL 支持 DNS SRV 的信息，请参阅["Connecting to the Server Using DNS SRV Records"](https://dev.mysql.com/doc/refman/8.0/en/connecting-using-dns-srv.html)。

假设 DNS 已为 *example.com* 域配置了此 SRV 信息：

```simple
Name                     TTL   Class   Priority Weight Port Target
_mysql._tcp.example.com. 86400 IN SRV  0        5      3306 host1.example.com
_mysql._tcp.example.com. 86400 IN SRV  0        10     3306 host2.example.com
_mysql._tcp.example.com. 86400 IN SRV  10       5      3306 host3.example.com
_mysql._tcp.example.com. 86400 IN SRV  20       5      3306 host4.example.com
```

要使用 DNS SRV 记录，请像这样调用 **mysql**：

```terminal
mysql --dns-srv-name=_mysql._tcp.example.com
```

然后，**mysql** 会尝试与组中的每个服务器建立连接，直到连接成功为止。只有在无法与任何服务器建立连接时，才会发生连接失败。DNS SRV 记录中的优先级和权重值决定了尝试服务器的顺序。

使用`--dns-srv-name`调用时，**mysql** 只尝试建立 TCP 连接。

The `--dns-srv-name` option takes precedence over the `--host` option if both are given. `--dns-srv-name` causes connection establishment to use the `mysql_real_connect_dns_srv()` C API function rather than `mysql_real_connect()`. However, if the *connect* command is subsequently used at runtime and specifies a host name argument, that host name takes precedence over any `--dns-srv-name` option given at **mysql** startup to specify a DNS SRV record.

如果同时给出`--dns-srv-name`和`--host`选项，`--dns-srv-name`选项优先于`--host`选项。`--dns-srv-name`会导致连接的建立使用`mysql_real_connect_dns_srv()` C API函数，而不是 `mysql_real_connect()`。不过，如果随后在运行时使用 *connect* 命令并指定了主机名参数，则该主机名优先于在 **mysql** 启动时指定 DNS SRV 记录的任何 `--dns-srv-name` 选项。

此选项在 MySQL 8.0.22 中添加。

### \-\-enable-cleartext-plugin

|**Command-Line Format**|**\-\-enable-cleartext-plugin**|
|:--|--|
|**Type**|**Boolean**|
|**Default Value**|**FALSE**|

启用*mysql_clear_password*明文身份验证插件。（请参阅["Client-Side Cleartext Pluggable Authentication"](https://dev.mysql.com/doc/refman/8.0/en/cleartext-pluggable-authentication.html)）。

### \-\-execute=*statement*, -e *statement*

|**Command-Line Format**|**\-\-execute=statement**|
|:--|--|
|**Type**|**String**|

执行语句并退出。默认输出格式与使用 `--batch` 生成的格式相同。请参阅["Using Options on the Command Line"](https://dev.mysql.com/doc/refman/8.0/en/command-line-options.html)，了解一些示例。使用该选项后，**mysql** 不使用历史文件。

### \-\-fido-register-factor=*value*

|**Command-Line Format**|**\-\-fido-register-factor=value**|
|:--|--|
|**Introduced**|**8.0.27**|
|**Deprecated**|**8.0.35**|
|**Type**|**String**|

> **注意：** 自 MySQL 8.0.35 起，该选项已被弃用，并可能在未来的 MySQL 版本中删除。

必须进行 FIDO 设备注册的一个或多个因素。该选项值必须是单个值，或用逗号分隔的两个值。每个值必须是 2 或 3，因此允许的选项值有 "2"、"3"、"2,3 "和 "3,2"。

例如，需要注册第 3 个身份验证因素的账户调用 **mysql** 客户端的步骤如下：

```terminal
mysql --user=user_name --fido-register-factor=3
```

需要注册第 2 和第 3 个身份验证因素的账户调用 **mysql** 客户端的方式如下：

```terminal
mysql --user=user_name --fido-register-factor=2,3
```

如果注册成功，就会建立连接。如果存在待注册的身份验证因素，则在尝试连接服务器时，连接会进入待注册模式。在这种情况下，请断开连接，然后使用正确的 `-fido-register-factor` 值重新连接，以完成注册。

注册分两个步骤，包括*initiate registration*和*finish registration*两个步骤。启动注册步骤执行本语句：

```sql
ALTER USER user factor INITIATE REGISTRATION
```

语句会返回一个结果集，其中包含一个 32 字节的challenge、user name和relying party ID（请参阅"["authentication_fido_rp_id"](https://dev.mysql.com/doc/refman/8.0/en/pluggable-authentication-system-variables.html#sysvar_authentication_fido_rp_id)"）。

finish registration步骤将执行该语句：

```sql
ALTER USER user factor FINISH REGISTRATION SET CHALLENGE_RESPONSE AS 'auth_string'
```

语句完成注册并向服务器发送以下信息，作为 *auth_string* 的一部分：验证器数据、X.509 格式的可选认证证书和签名。

启动和注册步骤必须在单个连接中执行，因为客户端在启动步骤中收到的挑战会保存到客户端连接处理程序中。如果在不同的连接中执行注册步骤，注册就会失败。使用`--fido-register-factor`选项可同时执行启动和注册步骤，从而避免上述失败情况，并避免手动执行`ALTER USER`启动和注册语句。

`--fido-register-factor`选项仅适用于**mysql**客户端和 MySQL Shell。其他 MySQL 客户端程序不支持该选项。

相关信息请参阅["Using FIDO Authentication"](https://dev.mysql.com/doc/refman/8.0/en/fido-pluggable-authentication.html#fido-pluggable-authentication-usage)。

### \-\-force, -f

|**Command-Line Format**|**\-\-force**|
|:--|--|

即使出现 SQL 错误也要继续。

### \-\-get-server-public-key

|**Command-Line Format**|**\-\-get-server-public-key**|
|:--|--|
|**Type**|**Boolean**|

向服务器请求基于 RSA 密钥对的密码交换所需的公钥。该选项适用于使用 *caching_sha2_password* 验证插件进行验证的客户端。对于该插件，除非请求，否则服务器不会发送公钥。对于不使用该插件进行身份验证的账户，该选项将被忽略。如果不使用基于 RSA 的密码交换，如客户端使用安全连接连接到服务器时，该选项也会被忽略。

如果给出了 `--server-public-key-path=file_name`，并指定了一个有效的公钥文件，则它优先于 `--get-server-public-key`。

有关 *caching_sha2_password* 插件的信息，请参阅["Caching SHA-2 Pluggable Authentication"](https://dev.mysql.com/doc/refman/8.0/en/caching-sha2-pluggable-authentication.html)。

### \-\-histignore

|**Command-Line Format**|**\-\-histignore=pattern_list**|
|:--|--|
|**Type**|**String**|

由一个或多个冒号分隔模式组成的列表，用于指定忽略日志记录的语句。这些模式会添加到默认模式列表（"\*IDENTIFIED\*:\*PASSWORD\*"）中。为该选项指定的值会影响写入历史文件的语句的日志记录，如果给定了 `--syslog`选项，还会影响写入 syslog 的日志记录。更多信息，请参阅["mysql Client Logging"](https://dev.mysql.com/doc/refman/8.0/en/mysql-logging.html)。

### \-\-host=*host_name*, -h *host_name*

|**Command-Line Format**|**\-\-host=host_name**|
|:--|--|
|**Type**|**String**|
|**Default Value**|**localhost**|

连接指定主机上的 MySQL 服务器。

如果同时给出`--dns-srv-name`和`--host`选项，`--dns-srv-name`选项优先于`--host`选项。`dns-srv-name`会导致连接的建立使用`mysql_real_connect_dns_srv()` C API函数，而不是`mysql_real_connect()`。但是，如果随后在运行时使用 connect 命令并指定了主机名参数，则该主机名优先于在 **mysql** 启动时指定 DNS SRV 记录的任何 `--dns-srv-name` 选项。

### \-\-html, -H

|**Command-Line Format**|**\-\-html**|
|:--|--|

生成 HTML 输出。

### \-\-ignore-spaces, -i

|**Command-Line Format**|**\-\-ignore-spaces**|
|:--|--|

忽略函数名称后的空格。其效果在有关 `IGNORE_SPACE` SQL 模式的讨论中有所描述（参见["Server SQL Modes"](https://dev.mysql.com/doc/refman/8.0/en/sql-mode.html)）。

### \-\-init-command=str

|**Command-Line Format**|**\-\-init-command=str**|
|:--|--|

连接服务器后要执行的 SQL 语句。如果启用了自动重新连接，则会在重新连接后再次执行语句。

### \-\-line-numbers

|**Command-Line Format**|**\-\-line-numbers**|
|:--|--|
|**Disabled by**|**skip-line-numbers**|

为错误写入行号。使用 `-skip-line-numbers`禁用此功能。

### \-\-load-data-local-dir=*dir_name*

|**Command-Line Format**|**\-\-load-data-local-dir=dir_name**|
|:--|--|
|**Introduced**|**8.0.21**|
|**Type**|**Directory name**|
|**Default Value**|**empty string**|

该选项会影响客户机端 LOCAL 功能对 `LOAD DATA` 操作的影响。它指定了在 `LOAD DATA LOCAL` 语句中命名的文件必须位于的目录。`load-data-local-dir`的效果取决于 LOCAL 数据加载是启用还是禁用：

- 如果启用了本地数据加载（在 MySQL 客户端库中默认启用或通过指定 `--local-infile[=1]`），则会忽略 `--load-data-local-dir`选项。

- 如果 MySQL 客户端库默认或通过指定 `--local-infile=0`禁用了本地数据加载，则 `--load-data-local-dir`选项适用。

当使用`--load-data-local-dir`时，选项值指定了本地数据文件所在的目录。无论底层文件系统的大小写敏感性如何，目录路径名和要加载的文件路径名的比较都是区分大小写的。如果选项值为空字符串，则不命名任何目录，结果是不允许加载本地数据文件。

例如，要显式禁用本地数据加载（位于 */my/local/data* 目录下的文件除外），请像这样调用 **mysql** ：

```terminal
mysql --local-infile=0 --load-data-local-dir=/my/local/data
```

当同时给出 `--local-infile` 和 `--load-data-local-dir` 时，它们的顺序并不重要。

在 **mysql** 中成功使用 LOCAL 加载操作还要求服务器允许本地加载；请参阅["Security Considerations for LOAD DATA LOCAL"](https://dev.mysql.com/doc/refman/8.0/en/load-data-local-security.html)

在 MySQL 8.0.21 中添加了`--load-data-local-dir`选项。

### \-\-local-infile[={0|1}]

|**Command-Line Format**|**\-\-local-infile[={0\|1}]**|
|:--|--|
|**Type**|**Boolean**|
|**Default Value**|**FALSE**|

默认情况下，`LOAD DATA`的本地能力由编译到 MySQL 客户端库中的默认值决定。要明确启用或禁用本地数据加载，请使用 `--local-infile` 选项。如果不指定值，该选项将启用本地数据加载。如果给出的是`--local-infile=0`或`--local-infile=1`，则该选项会禁用或启用本地数据加载。

如果禁用了 LOCAL 功能，则可以使用 `--load-data-local-dir` 选项来限制本地加载指定目录中的文件。

在 **mysql** 中成功使用 LOCAL 加载操作还要求服务器允许本地加载；请参阅["Security Considerations for LOAD DATA LOCAL"](https://dev.mysql.com/doc/refman/8.0/en/load-data-local-security.html)

### \-\-login-path=*name*

|**Command-Line Format**|**\-\-login-path=name**|
|:--|--|
|**Type**|**String**|

Read options from the named login path in the *.mylogin.cnf* login path file. A "login path" is an option group containing options that specify which MySQL server to connect to and which account to authenticate as. To create or modify a login path file, use the **mysql_config_editor** utility. See ["mysql_config_editor — MySQL Configuration Utility"](https://dev.mysql.com/doc/refman/8.0/en/mysql-config-editor.html).

从 *.mylogin.cnf* 登录路径文件中指定的登录路径读取选项。登录路径 "是一个选项组，包含指定连接到哪个 MySQL 服务器和以哪个账户进行身份验证的选项。要创建或修改登录路径文件，请使用**mysql_config_editor**工具。参见["mysql_config_editor — MySQL Configuration Utility"](https://dev.mysql.com/doc/refman/8.0/en/mysql-config-editor.html)。

有关该选项和其他选项文件选项的更多信息，请参阅["Command-Line Options that Affect Option-File Handling"](https://dev.mysql.com/doc/refman/8.0/en/option-file-options.html)。

### \-\-max-allowed-packet=*value*

|**Command-Line Format**|**\-\-max-allowed-packet=value**|
|:--|--|
|**Type**|**Numeric**|
|**Default Value**|**16777216**|

客户端/服务器通信缓冲区的最大大小。默认为 16MB，最大为 1GB。

### \-\-max-join-size=*value*

|**Command-Line Format**|**\-\-max-join-size=value**|
|:--|--|
|**Type**|**Numeric**|
|**Default Value**|**1000000**|

使用 `--safe-updates` 时连接中记录的自动限制。（默认值为 1,000,000）。

### \-\-named-commands, -G

|**Command-Line Format**|**\-\-named-commands**|
|:--|--|
|**Disabled by**|**skip-named-commands**|

Enable named **mysql** commands. Long-format commands are permitted, not just short-format commands. For example, `quit` and `\q` both are recognized. Use `--skip-named-commands` to disable named commands. See ["mysql Client Commands"](https://dev.mysql.com/doc/refman/8.0/en/mysql-commands.html).

启用已命名的 **mysql** 命令。允许使用长格式命令，而不仅仅是短格式命令。例如，`quit`和`\q`都能被识别。使用 `-skip-named-commands`禁用命名命令。参见["mysql Client Commands"](https://dev.mysql.com/doc/refman/8.0/en/mysql-commands.html)。

### \-\-net-buffer-length=*value*

|**Command-Line Format**|**\-\-net-buffer-length=value**|
|:--|--|
|**Type**|**Numeric**|
|**Default Value**|**16384**|

TCP/IP 和套接字通信的缓冲区大小。（默认值为 16KB）。

### \-\-network-namespace=*name*

|**Command-Line Format**|**\-\-network-namespace=name**|
|:--|--|
|**Introduced**|**8.0.22**|
|**Type**|**String**|

TCP/IP 连接使用的网络命名空间。如果省略，连接将使用默认（全局）命名空间。有关网络命名空间的信息，请参阅["Network Namespace Support"](https://dev.mysql.com/doc/refman/8.0/en/network-namespace-support.html)。

此选项在 MySQL 8.0.22 中添加。它仅适用于支持网络命名空间的平台。

### \-\-no-auto-rehash, -A

|**Command-Line Format**|**\-\-no-auto-rehash**|
|:--|--|
|**Deprecated**|**Yes**|

与`--skip-auto-rehash`效果相同。请参阅`--auto-rehash`的说明。

### \-\-no-beep, -b

|**Command-Line Format**|**\-\-no-beep**|
|:--|--|

发生错误时不发出蜂鸣声。

### \-\-no-defaults

|**Command-Line Format**|**\-\-no-defaults**|
|:--|--|

不读取任何选项文件。如果从选项文件中读取未知选项导致程序启动失败，可以使用`--no-defaults`来阻止读取这些选项。

例外情况是，如果存在 *.mylogin.cnf* 文件，则在所有情况下都会读取该文件。这样，即使使用了`--no-defaults`，也能以比命令行更安全的方式指定密码。要创建 *.mylogin.cnf*，请使用 **mysql_config_editor** 工具。请参阅["mysql_config_editor — MySQL Configuration Utility"](https://dev.mysql.com/doc/refman/8.0/en/mysql-config-editor.html)。

有关该选项和其他选项文件选项的更多信息，请参阅["Command-Line Options that Affect Option-File Handling"](https://dev.mysql.com/doc/refman/8.0/en/option-file-options.html)。

### \-\-one-database, -o

|**Command-Line Format**|**\-\-one-database**|
|:--|--|

忽略语句，但默认数据库为命令行中指定的数据库时出现的语句除外。该选项非常简单，应谨慎使用。语句过滤只基于 `USE` 语句。

最初，**mysql** 执行输入中的语句，因为在命令行中指定数据库 *db_name* 等于在输入的开头插入 `USE db_name`。然后，对于遇到的每一条 `USE` 语句，**mysql** 都会接受或拒绝以下语句，这取决于所指定的数据库是否是命令行中的数据库。语句的内容无关紧要。

假设调用 **mysql** 处理这组语句：

```sql
DELETE FROM db2.t2;
USE db2;
DROP TABLE db1.t1;
CREATE TABLE db1.t1 (i INT);
USE db1;
INSERT INTO t1 (i) VALUES(1);
CREATE TABLE db2.t1 (j INT);
```

如果命令行是 **mysql \-\-force \-\-one-database db1**，**mysql** 会如下处理输入：

- 由于默认数据库是 db1，所以执行了 `DELETE` 语句，尽管该语句命名的是另一个数据库中的表。

- 由于默认数据库不是 db1，所以未执行 `DROP TABLE` 和 `CREATE TABLE` 语句，即使这些语句命名了 db1 中的表。

- 由于默认数据库是 db1，因此会执行 `INSERT` 和 `CREATE TABLE` 语句，即使 `CREATE TABLE` 语句命名了不同数据库中的表。

### \-\-pager[=*command*]

|**Command-Line Format**|**\-\-pager[=command]**|
|:--|--|
|**Disabled by**|**skip-pager**|
|**Type**|**String**|

使用给定命令对查询输出进行分页。如果省略该命令，默认分页器就是 *PAGER* 环境变量的值。有效的分页器有**less**、**more**、**cat [> filename]** 等。该选项仅在 Unix 和交互模式下有效。要禁用分页功能，请使用 `-skip-pager`。请参阅["mysql Client Commands"](https://dev.mysql.com/doc/refman/8.0/en/mysql-commands.html)节将进一步讨论输出分页。

### \-\-password[=*password*], -p [*password*]

|**Command-Line Format**|**\-\-password[=password]**|
|:--|--|
|**Type**|**String**|

用于连接服务器的 MySQL 账户密码。密码值是可选的。如果未给出，**mysql** 会提示输入密码。如果指定了密码，`--password=`或`-p`与后面的密码之间必须*无空格*。如果没有指定密码选项，默认情况下不发送密码。

在命令行中指定密码是不安全的。为避免在命令行上提供密码，请使用选项文件。请参阅["End-User Guidelines for Password Security"](https://dev.mysql.com/doc/refman/8.0/en/password-security-user.html)。

要明确指定不需要密码，也不提示**mysql**输入密码，可使用`--skip-password`选项。

### \-\-password1[=*pass_val*]

用于连接服务器的 MySQL 账户的多因素身份验证因素 1 的密码。密码值是可选的。如果未给出，**mysql** 会提示输入密码。如果给定，`--password1=`和后面的密码之间必须没有空格。如果未指定密码选项，默认情况下不发送密码。

在命令行中指定密码是不安全的。为避免在命令行上提供密码，请使用选项文件。请参阅["End-User Guidelines for Password Security"](https://dev.mysql.com/doc/refman/8.0/en/password-security-user.html)。

要明确指定没有密码，且 **mysql** 不提示输入密码，请使用 `--skip-password1` 选项。

`--password1`和`--password`是同义词，`--skip-password1`和`--skip-password`也是同义词。

### \-\-password2[=*pass_val*]

用于连接服务器的 MySQL 账户的多因素身份验证因素 2 的密码。该选项的语义类似于`--password1`的语义；详情请参见该选项的说明。

### \-\-password3[=*pass_val*]

用于连接服务器的 MySQL 账户的多因素身份验证因素 3 的密码。该选项的语义类似于`--password1`的语义；详情请参见该选项的说明。

### \-\-pipe, -W

|**Command-Line Format**|**\-\-pipe**|
|:--|--|
|**Type**|**String**|

在 Windows 系统中，使用命名管道连接服务器。只有在服务器启动时启用了支持命名管道连接的系统变量`named_pipe`，此选项才适用。此外，进行连接的用户必须是由 `named_pipe_full_access_group` 系统变量指定的 Windows 组的成员。

### \-\-plugin-authentication-kerberos-client-mode=*value*

|**Command-Line Format**|**\-\-plugin-authentication-kerberos-client-mode**|
|:--|--|
|**Introduced**|**8.0.32**|
|**Type**|**String**|
|**Default Value**|**SSPI**|
|**Valid Values**|**GSSAPI / SSPI**|

在 Windows 系统中，*authentication_kerberos_client* 身份验证插件支持该插件选项。它提供两种可能的值，客户端用户可在运行时进行设置： *SSPI* 和 *GSSAPI*。

客户端插件选项的默认值使用安全支持提供程序接口（SSPI），该接口可从 Windows 内存缓存中获取凭证。另外，客户端用户也可以选择通过 Windows 上的 MIT Kerberos 库支持通用安全服务应用程序接口（GSSAPI）的模式。GSSAPI 能够获取以前使用 **kinit** 命令生成的缓存凭证。

更多信息，请参阅 [Commands for Windows Clients in GSSAPI Mode](https://dev.mysql.com/doc/refman/8.0/en/kerberos-pluggable-authentication.html#kerberos-usage-win-gssapi-client-commands)。

### \-\-plugin-dir=*dir_name*

|**Command-Line Format**|**\-\-plugin-dir=dir_name**|
|:--|--|
|**Type**|**Directory name**|

查找插件的目录。如果使用`--default-auth`选项指定了一个身份验证插件，但**mysql**没有找到它，则指定此选项。参见["Pluggable Authentication"](https://dev.mysql.com/doc/refman/8.0/en/pluggable-authentication.html)。

### \-\-port=*port_num*, -P *port_num*

|**Command-Line Format**|**\-\-port=port_num**|
|:--|--|
|**Type**|**Numeric**|
|**Default Value**|**3306**|

对于 TCP/IP 连接，要使用的端口号。

### \-\-print-defaults

|**Command-Line Format**|**\-\-print-defaults**|
|:--|--|

打印程序名称及其从选项文件中获取的所有选项。

有关该选项和其他选项文件选项的更多信息，请参阅["Command-Line Options that Affect Option-File Handling"](https://dev.mysql.com/doc/refman/8.0/en/option-file-options.html)。

### \-\-protocol={TCP\|SOCKET\|PIPE\|MEMORY}

|**Command-Line Format**|**\-\-protocol=type**|
|:--|--|
|**Type**|**String**|
|**Default Value**|**[see text]**|
|**Valid Values**|**TCP / SOCKET / PIPE / MEMORY**|

用于连接服务器的传输协议。当其他连接参数通常会导致使用与所需协议不同的协议时，该协议非常有用。有关允许值的详细信息，请参阅章节["Connection Transport Protocols"](https://dev.mysql.com/doc/refman/8.0/en/transport-protocols.html)。

### \-\-quick, -q

|**Command-Line Format**|**\-\-quick**|
|:--|--|

不要缓存每个查询结果，而是在收到每一行时打印出来。如果暂停输出，服务器速度可能会变慢。使用此选项后，**mysql** 不会使用历史文件。

### \-\-raw, -r

|**Command-Line Format**|**\-\-raw**|
|:--|--|

对于表格输出，列周围的 "方框" 可使一列值与另一列值区分开来。对于非表格输出（例如在批处理模式下或使用 `--batch` 或 `--silent` 选项时产生的输出），特殊字符会在输出中转义，以便于识别。换行符、制表符、NUL 和反斜线被写成 \n、\t、\0 和 \\\\。`--raw` 选项会禁用这种字符转义。

下面的示例演示了表格输出与非表格输出，以及使用原始模式禁用转义：

```sql
% mysql
mysql> SELECT CHAR(92);
+----------+
| CHAR(92) |
+----------+
| \        |
+----------+

% mysql -s
mysql> SELECT CHAR(92);
CHAR(92)
\\

% mysql -s -r
mysql> SELECT CHAR(92);
CHAR(92)
\
```

### \-\-reconnect

|**Command-Line Format**|**\-\-reconnect**|
|:--|--|
|**Disabled by**|**skip-reconnect**|

如果与服务器的连接丢失，会自动尝试重新连接。每次连接丢失都会尝试一次重新连接。要抑制重新连接行为，请使用 `-skip-reconnect`。

### \-\-asfe-updates, \-\-i-am-a-dummy, -U

|**Command-Line Format**|**\-\-safe-updates / \-\-i-am-a-dummy**|
|:--|--|
|**Type**|**Boolean**|
|**Default Value**|**FALSE**|

If this option is enabled, `UPDATE` and `DELETE` statements that do not use a key in the WHERE clause or a `LIMIT` clause produce an error. In addition, restrictions are placed on `SELECT` statements that produce (or are estimated to produce) very large result sets. If you have set this option in an option file, you can use `--skip-safe-updates` on the command line to override it. For more information about this option, see [Using Safe-Updates Mode (--safe-updates)](https://dev.mysql.com/doc/refman/8.0/en/mysql-tips.html#safe-updates).

如果启用了该选项，在 WHERE 子句中未使用键或 `LIMIT` 子句的 `UPDATE` 和 `DELETE` 语句将产生错误。此外，对产生（或估计会产生）超大结果集的 `SELECT` 语句也会进行限制。如果在选项文件中设置了该选项，可以在命令行中使用 `-skip-safe-updates`来覆盖它。有关该选项的更多信息，请参阅[Using Safe-Updates Mode (--safe-updates)](https://dev.mysql.com/doc/refman/8.0/en/mysql-tips.html#safe-updates)。

### \-\-select-limit=*value*

|**Command-Line Format**|**\-\-select-limit=value**|
|:--|--|
|**Type**|**Numeric**|
|**Default Value**|**1000**|

使用 `--safe-updates` 时 `SELECT` 语句的自动限制。（默认值为 1,000）。

### \-\-server-public-key-path=*file_name*

|**Command-Line Format**|**\-\-server-public-key-path=file_name**|
|:--|--|
|**Type**|**File name**|

PEM 格式文件的路径名，该文件包含服务器在基于 RSA 密钥对的密码交换中需要的公钥的客户端副本。该选项适用于使用 *sha256_password* 或 *caching_sha2_password* 身份验证插件进行身份验证的客户端。对于未使用上述插件之一进行身份验证的账户，该选项将被忽略。如果不使用基于 RSA 的密码交换，如客户端使用安全连接连接到服务器时，该选项也会被忽略。

如果给出了 `--server-public-key-path=file_name`，并指定了一个有效的公钥文件，则它优先于 `--get-server-public-key`。

对于 *sha256_password*，该选项仅适用于使用 OpenSSL 构建的 MySQL。

有关 *sha256_password* 和 *caching_sha2_password* 插件的信息，请参阅第 ["SHA-256 Pluggable Authentication"](https://dev.mysql.com/doc/refman/8.0/en/sha256-pluggable-authentication.html) 和第 ["Caching SHA-2 Pluggable Authentication"](https://dev.mysql.com/doc/refman/8.0/en/caching-sha2-pluggable-authentication.html) 。

### \-\-shared-memory-base-name=*name*

|**Command-Line Format**|**\-\-shared-memory-base-name=name**|
|:--|--|
|**Platform Specific**|**Windows**|

在 Windows 中，使用共享内存连接本地服务器时要使用的共享内存名称。默认值为 MYSQL。共享内存名称区分大小写。

该选项仅适用于服务器启动时启用了 `shared_memory` 系统变量以支持共享内存连接的情况。

### \-\-show-warnings

|**Command-Line Format**|**\-\-show-warnings**|
|:--|--|

在每条语句后显示警告（如果有的话）。该选项适用于交互式和批处理模式。

### \-\-sigint-ignore

|**Command-Line Format**|**\-\-sigint-ignore**|
|:--|--|

忽略 SIGINT 信号（通常是输入 **Control+C** 的结果）。

如果没有该选项，键入 **Control+C** 会中断当前语句，否则会取消任何部分输入行。

### \-\-silent, -s

|**Command-Line Format**|**\-\-silent**|
|:--|--|

静音模式。减少输出。该选项可多次使用，以减少输出。

该选项会导致非表格输出格式和特殊字符转义。使用原始模式可以禁用 "转义"；请参阅`--raw`选项的说明。

### \-\-skip-column-names, -N

|**Command-Line Format**|**\-\-skip-column-names**|
|:--|--|

不要在结果中写入列名。

### \-\-skpi-line-numbers, -L

|**Command-Line Format**|**\-\-skpi-line-numbers**|
|:--|--|

不写入错误的行号。在比较包含错误信息的结果文件时非常有用。

### \-\-socket=*path*, -S *path*

|**Command-Line Format**|**\-\-socket={file_name\|pipe_name}**|
|:--|--|
|**Type**|**String**|

对于与 *localhost* 的连接，要使用的 Unix 套接字文件，或者在 Windows 下，要使用的命名管道名称。

在 Windows 系统中，只有在服务器启动时启用了`named_pipe`系统变量以支持命名管道连接的情况下，该选项才适用。此外，进行连接的用户必须是由 `named_pipe_full_access_group` 系统变量指定的 Windows 组的成员。

### \-\-ssl*

以`--ssl`开头的选项指定是否使用加密方式连接服务器，并指明在哪里可以找到 SSL 密钥和证书。请参阅[Command Options for Encrypted Connections](https://dev.mysql.com/doc/refman/8.0/en/connection-options.html#encrypted-connection-options)。

### \-\-ssl-fips-mode={OFF\|ON\|STRICT}

|**Command-Line Format**|**\-\-ssl-fips-mode={OFF\|ON\|STRICT}**|
|:--|--|
|**Deprecated**|**8.0.34**|
|**Type**|**Enumeration**|
|**Default Value**|**OFF**|
|**Valid Values**|**OFF / ON / STRICT**|
todo：
Controls whether to enable FIPS mode on the client side. The `--ssl-fips-mode` option differs from other `--ssl-xxx` options in that it is not used to establish encrypted connections, but rather to affect which cryptographic operations to permit. See ["FIPS Support"](https://dev.mysql.com/doc/refman/8.0/en/fips-mode.html).

These `--ssl-fips-mode` values are permitted:

- OFF: Disable FIPS mode.

- ON: Enable FIPS mode.

- STRICT: Enable “strict” FIPS mode.

> **Note:** If the OpenSSL FIPS Object Module is not available, the only permitted value for `--ssl-fips-mode` is OFF. In this case, setting `--ssl-fips-mode` to *ON* or *STRICT* causes the client to produce a warning at startup and to operate in non-FIPS mode.

As of MySQL 8.0.34, this option is deprecated. Expect it to be removed in a future version of MySQL.

### \-\-syslog, -j

|**Command-Line Format**|**\-\-syslog**|
|:--|--|

This option causes **mysql** to send interactive statements to the system logging facility. On Unix, this is *syslog*; on Windows, it is the Windows Event Log. The destination where logged messages appear is system dependent. On Linux, the destination is often the */var/log/messages* file.

Here is a sample of output generated on Linux by using `--syslog`. This output is formatted for readability; each logged message actually takes a single line.

```
Mar  7 12:39:25 myhost MysqlClient[20824]:
  SYSTEM_USER:'oscar', MYSQL_USER:'my_oscar', CONNECTION_ID:23,
  DB_SERVER:'127.0.0.1', DB:'--', QUERY:'USE test;'
Mar  7 12:39:28 myhost MysqlClient[20824]:
  SYSTEM_USER:'oscar', MYSQL_USER:'my_oscar', CONNECTION_ID:23,
  DB_SERVER:'127.0.0.1', DB:'test', QUERY:'SHOW TABLES;'
```

For more information, see ["mysql Client Logging"](https://dev.mysql.com/doc/refman/8.0/en/mysql-logging.html).

### \-\-table, -t

|**Command-Line Format**|**\-\-table**|
|:--|--|

Display output in table format. This is the default for interactive use, but can be used to produce table output in batch mode.

### \-\-tee-*file_name*

|**Command-Line Format**|**\-\-tee=file_name**|
|:--|--|
|**Type**|**File name**|

Append a copy of output to the given file. This option works only in interactive mode. Section ["mysql Client Commands"](https://dev.mysql.com/doc/refman/8.0/en/mysql-commands.html), discusses tee files further.

### \-\-tls-ciphersuites=*ciphersuite_list*

|**Command-Line Format**|**\-\-tls-ciphersuites=ciphersuite_list**|
|:--|--|
|**Introduced**|**8.0.16**|
|**Type**|**String**|

The permissible ciphersuites for encrypted connections that use TLSv1.3. The value is a list of one or more colon-separated ciphersuite names. The ciphersuites that can be named for this option depend on the SSL library used to compile MySQL. For details, see ["Encrypted Connection TLS Protocols and Ciphers"](https://dev.mysql.com/doc/refman/8.0/en/encrypted-connection-protocols-ciphers.html).

This option was added in MySQL 8.0.16.

### \-\-tls-version=*protocol_list*

|**Command-Line Format**|**\-\-tls-version=protocol_list**|
|:--|--|
|**Type**|**String**|
|**Default Value(≥ 8.0.19)**|**TLSv1,TLSv1.1,TLSv1.2,TLSv1.3 (OpenSSL 1.1.1 or higher) / TLSv1,TLSv1.1,TLSv1.2 (otherwise)**|
|**Default Value(≤ 8.0.18)**|**TLSv1,TLSv1.1,TLSv1.2**|

The permissible TLS protocols for encrypted connections. The value is a list of one or more comma-separated protocol names. The protocols that can be named for this option depend on the SSL library used to compile MySQL. For details, see ["Encrypted Connection TLS Protocols and Ciphers"](https://dev.mysql.com/doc/refman/8.0/en/encrypted-connection-protocols-ciphers.html).

### \-\-unbuffered, -n

|**Command-Line Format**|**\-\-unbuffered**|
|:--|--|

Flush the buffer after each query.

### \-\-user=*user_name*, -u *user_name*

|**Command-Line Format**|**\-\-user=user_name**|
|:--|--|
|**Type**|**String**|

The user name of the MySQL account to use for connecting to the server.

### \-\-verbose, -v

|**Command-Line Format**|**\-\-verbose**|
|:--|--|

Verbose mode. Produce more output about what the program does. This option can be given multiple times to produce more and more output. (For example, -v -v -v produces table output format even in batch mode.)

### \-\-version, -V

|**Command-Line Format**|**\-\-version**|
|:--|--|

Display version information and exit.

### \-\-vertical, -E

|**Command-Line Format**|**\-\-vertical**|
|:--|--|

Print query output rows vertically (one line per column value). Without this option, you can specify vertical output for individual statements by terminating them with \G.

### \-\-wait, -w

|**Command-Line Format**|**\-\-wait**|
|:--|--|

If the connection cannot be established, wait and retry instead of aborting.

### \-\-xml, -X

|**Command-Line Format**|**\-\-xml**|
|:--|--|

Produce XML output.

```xml
<field name="column_name">NULL</field>
```

The output when `--xml` is used with **mysql** matches that of **mysqldump** `--xml`. See ["mysqldump — A Database Backup Program"](https://dev.mysql.com/doc/refman/8.0/en/mysqldump.html), for details.

The XML output also uses an XML namespace, as shown here:

```xml
$> mysql --xml -uroot -e "SHOW VARIABLES LIKE 'version%'"
<?xml version="1.0"?>

<resultset statement="SHOW VARIABLES LIKE 'version%'" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
<row>
<field name="Variable_name">version</field>
<field name="Value">5.0.40-debug</field>
</row>

<row>
<field name="Variable_name">version_comment</field>
<field name="Value">Source distribution</field>
</row>

<row>
<field name="Variable_name">version_compile_machine</field>
<field name="Value">i686</field>
</row>

<row>
<field name="Variable_name">version_compile_os</field>
<field name="Value">suse-linux-gnu</field>
</row>
</resultset>
```

### \-\-zstd-compression-level=*level*

|**Command-Line Format**|**\-\-zstd-compression-level=#**|
|:--|--|
|**Introduced**|**8.0.18**|
|**Type**|**Integer**|

The compression level to use for connections to the server that use the zstd compression algorithm. The permitted levels are from 1 to 22, with larger values indicating increasing levels of compression. The default zstd compression level is 3. The compression level setting has no effect on connections that do not use zstd compression.

For more information, see ["Connection Compression Control"](https://dev.mysql.com/doc/refman/8.0/en/connection-compression-control.html).

This option was added in MySQL 8.0.18.

## mysql Client Commands

**mysql** sends each SQL statement that you issue to the server to be executed. There is also a set of commands that **mysql** itself interprets. For a list of these commands, type `help` or `\h` at the `mysql>` prompt:

```
mysql> help

List of all MySQL commands:
Note that all text commands must be first on line and end with ';'
?         (\?) Synonym for `help'.
clear     (\c) Clear the current input statement.
connect   (\r) Reconnect to the server. Optional arguments are db and host.
delimiter (\d) Set statement delimiter.
edit      (\e) Edit command with $EDITOR.
ego       (\G) Send command to mysql server, display result vertically.
exit      (\q) Exit mysql. Same as quit.
go        (\g) Send command to mysql server.
help      (\h) Display this help.
nopager   (\n) Disable pager, print to stdout.
notee     (\t) Don't write into outfile.
pager     (\P) Set PAGER [to_pager]. Print the query results via PAGER.
print     (\p) Print current command.
prompt    (\R) Change your mysql prompt.
quit      (\q) Quit mysql.
rehash    (\#) Rebuild completion hash.
source    (\.) Execute an SQL script file. Takes a file name as an argument.
status    (\s) Get status information from the server.
system    (\!) Execute a system shell command.
tee       (\T) Set outfile [to_outfile]. Append everything into given
               outfile.
use       (\u) Use another database. Takes database name as argument.
charset   (\C) Switch to another charset. Might be needed for processing
               binlog with multi-byte charsets.
warnings  (\W) Show warnings after every statement.
nowarning (\w) Don't show warnings after every statement.
resetconnection(\x) Clean session context.
query_attributes Sets string parameters (name1 value1 name2 value2 ...)
for the next query to pick up.
ssl_session_data_print Serializes the current SSL session data to stdout 
or file.

For server side help, type 'help contents'
```

If **mysql** is invoked with the `--binary-mode` option, all **mysql** commands are disabled except *charset* and *delimiter* in noninteractive mode (for input piped to **mysql** or loaded using the *source* command).

Each command has both a long and short form. The long form is not case-sensitive; the short form is. The long form can be followed by an optional semicolon terminator, but the short form should not.

The use of short-form commands within multiple-line /* ... */ comments is not supported. Short-form commands do work within single-line /*! ... */ version comments, as do /*+ ... */ optimizer-hint comments, which are stored in object definitions. If there is a concern that optimizer-hint comments may be stored in object definitions so that dump files when reloaded with *mysql* would result in execution of such commands, either invoke **mysql** with the `--binary-mode` option or use a reload client other than **mysql**.

- help \[*arg*\], \\h \[*arg*\], \\? \[*arg*\], ? \[*arg*\]

    Display a help message listing the available mysql commands.
    
    If you provide an argument to the *help* command, **mysql** uses it as a search string to access server-side help from the contents of the MySQL Reference Manual. For more information, see ["mysql Client Server-Side Help"](https://dev.mysql.com/doc/refman/8.0/en/mysql-server-side-help.html).

- charset *charset_name*, \\C *charset_name*

    Change the default character set and issue a `SET NAMES` statement. This enables the character set to remain synchronized on the client and server if **mysql** is run with auto-reconnect enabled (which is not recommended), because the specified character set is used for reconnects.

- clear, \\c

    Clear the current input. Use this if you change your mind about executing the statement that you are entering.

- connect \[*db_name* \[*host_name*\]\], \\r \[*db_name* \[*host_name*\]\]

    Reconnect to the server. The optional database name and host name arguments may be given to specify the default database or the host where the server is running. If omitted, the current values are used.

    If the connect command specifies a host name argument, that host takes precedence over any `--dns-srv-name` option given at **mysql** startup to specify a DNS SRV record.

- delimiter *str*, \\d *str*

    Change the string that **mysql** interprets as the separator between SQL statements. The default is the semicolon character (;).

    The delimiter string can be specified as an unquoted or quoted argument on the *delimiter* command line. Quoting can be done with either single quote ('), double quote ("), or backtick (`) characters. To include a quote within a quoted string, either quote the string with a different quote character or escape the quote with a backslash (\\) character. Backslash should be avoided outside of quoted strings because it is the escape character for MySQL. For an unquoted argument, the delimiter is read up to the first space or end of line. For a quoted argument, the delimiter is read up to the matching quote on the line.

    **mysql** interprets instances of the delimiter string as a statement delimiter anywhere it occurs, except within quoted strings. Be careful about defining a delimiter that might occur within other words. For example, if you define the delimiter as `X`, it is not possible to use the word `INDEX` in statements. **mysql** interprets this as INDE followed by the delimiter `X`.

    When the delimiter recognized by **mysql** is set to something other than the default of ;, instances of that character are sent to the server without interpretation. However, the server itself still interprets ; as a statement delimiter and processes statements accordingly. This behavior on the server side comes into play for multiple-statement execution (see [Multiple Statement Execution Support](https://dev.mysql.com/doc/c-api/8.0/en/c-api-multiple-queries.html)), and for parsing the body of stored procedures and functions, triggers, and events (see ["Defining Stored Programs"](https://dev.mysql.com/doc/refman/8.0/en/stored-programs-defining.html)).

- edit, \\e

    Edit the current input statement. **mysql** checks the values of the EDITOR and VISUAL environment variables to determine which editor to use. The default editor is **vi** if neither variable is set.

    The *edit* command works only in Unix.

- ego, \\G

    Send the current statement to the server to be executed and display the result using vertical format.

- exit, \\q

    Exit **mysql**.

- go, \\g

    Send the current statement to the server to be executed.

- nopaper, \\n

    Disable output paging. See the description for *pager*.

    The *nopaper* command works only in Unix.

- notee, \\t

    Disable output copying to the tee file. See the description for *tee*.

- nowarning, \\w

    Disable display of warnings after each statement.

- pager \[*command*\], \\P \[*command*\]

    Enable output paging. By using the `--pager` option when you invoke **mysql**, it is possible to browse or search query results in interactive mode with Unix programs such as **less**, **more**, or any other similar program. If you specify no value for the option, **mysql** checks the value of the `PAGER` environment variable and sets the pager to that. Pager functionality works only in interactive mode.

    Output paging can be enabled interactively with the *pager* command and disabled with *nopager*. The command takes an optional argument; if given, the paging program is set to that. With no argument, the pager is set to the pager that was set on the command line, or *stdout* if no pager was specified.

    Output paging works only in Unix because it uses the *popen()* function, which does not exist on Windows. For Windows, the *tee* option can be used instead to save query output, although it is not as convenient as *pager* for browsing output in some situations.

- print, \\p

    Print the current input statement without executing it.

- prompt \[*str*\], \\R \[*str*\]

    Reconfigure the **mysql** prompt to the given string. The special character sequences that can be used in the prompt are described later in this section.

    If you specify the `prompt` command with no argument, **mysql** resets the prompt to the default of `mysql>`.

- query_attributes *name* *value* \[*name* *value* ...\]

    Define query attributes that apply to the next query sent to the server. For discussion of the purpose and use of query attributes, see ["Query Attributes"](https://dev.mysql.com/doc/refman/8.0/en/query-attributes.html).

    The `query_attributes` command follows these rules:

    - The format and quoting rules for attribute names and values are the same as for the `delimiter` command.

    - The command permits up to 32 attribute name/value pairs. Names and values may be up to 1024 characters long. If a name is given without a value, an error occurs.

    - If multiple `query_attributes` commands are issued prior to query execution, only the last command applies. After sending the query, **mysql** clears the attribute set.

    - If multiple attributes are defined with the same name, attempts to retrieve the attribute value have an undefined result.

    - An attribute defined with an empty name cannot be retrieved by name.

    - If a reconnect occurs while **mysql** executes the query, **mysql** restores the attributes after reconnecting so the query can be executed again with the same attributes.

- quit, \\q

    Exit **mysql**.

- rehash, \\#

    Rebuild the completion hash that enables database, table, and column name completion while you are entering statements. (See the description for the `--auto-rehash` option.)

- resetconnection, \\x

    Reset the connection to clear the session state. This includes clearing any current query attributes defined using the `query_attributes` command.

    Resetting a connection has effects similar to `mysql_change_user()` or an auto-reconnect except that the connection is not closed and reopened, and re-authentication is not done. See [mysql_change_user()](https://dev.mysql.com/doc/c-api/8.0/en/mysql-change-user.html), and [Automatic Reconnection Control](https://dev.mysql.com/doc/c-api/8.0/en/c-api-auto-reconnect.html).

    This example shows how `resetconnection` clears a value maintained in the session state:

    ```sql
    mysql> SELECT LAST_INSERT_ID(3);
    +-------------------+
    | LAST_INSERT_ID(3) |
    +-------------------+
    |                 3 |
    +-------------------+

    mysql> SELECT LAST_INSERT_ID();
    +------------------+
    | LAST_INSERT_ID() |
    +------------------+
    |                3 |
    +------------------+

    mysql> resetconnection;

    mysql> SELECT LAST_INSERT_ID();
    +------------------+
    | LAST_INSERT_ID() |
    +------------------+
    |                0 |
    +------------------+
    ```

- source *file_name*, \\. *file_name*

    Read the named file and executes the statements contained therein. On Windows, specify path name separators as / or \\\\.

    Quote characters are taken as part of the file name itself. For best results, the name should not include space characters.

- ssl_session_data_print \[*file_name*\]

    Fetches, serializes, and optionally stores the session data of a successful connection. The optional file name and arguments may be given to specify the file to store serialized session data. If omitted, the session data is printed to `stdout`.

    If the MySQL session is configured for reuse, session data from the file is deserialized and supplied to the *connect* command to reconnect. When the session is reused successfully, the *status* command contains a row showing *SSL session reused: true* while the client remains reconnected to the server.

- status, \\s

    Provide status information about the connection and the server you are using. If you are running with `--safe-updates` enabled, *status* also prints the values for the **mysql** variables that affect your queries.

- system *command*, \\! *command*

    Execute the given command using your default command interpreter.

    Prior to MySQL 8.0.19, the *system* command works only in Unix. As of 8.0.19, it also works on Windows.

- tee \[*file_name*\], \\T \[*file_name*\]

    By using the `--tee` option when you invoke **mysql**, you can log statements and their output. All the data displayed on the screen is appended into a given file. This can be very useful for debugging purposes also. **mysql** flushes results to the file after each statement, just before it prints its next prompt. Tee functionality works only in interactive mode.

    You can enable this feature interactively with the *tee* command. Without a parameter, the previous file is used. The *tee* file can be disabled with the notee command. Executing *tee* again re-enables logging.

- use *db_name*, \\u *db_name*

    Use *db_name* as the default database.

- warnings, \\W

    Enable display of warnings after each statement (if there are any).

Here are a few tips about the *pager* command:

- You can use it to write to a file and the results go only to the file:

    ```sql
    mysql> pager cat > /tmp/log.txt
    ```

    You can also pass any options for the program that you want to use as your pager:

    ```sql
    mysql> pager less -n -i -S
    ```

- In the preceding example, note the `-S` option. You may find it very useful for browsing wide query results. Sometimes a very wide result set is difficult to read on the screen. The `-S` option to **less** can make the result set much more readable because you can scroll it horizontally using the left-arrow and right-arrow keys. You can also use `-S` interactively within **less** to switch the horizontal-browse mode on and off. For more information, read the **less** manual page:

    ```terminal
    man less
    ```

- The `-F` and `-X` options may be used with **less** to cause it to exit if output fits on one screen, which is convenient when no scrolling is necessary:

    ```sql
    mysql> pager less -n -i -S -F -X
    ```

- You can specity very complex pager commands for handling query output:

    ```sql
    mysql> pager cat | tee /dr1/tmp/res.txt \
            | tee /dr2/tmp/res2.txt | less -n -i -S
    ```

    In this example, the command would send query results to two files in two different directories on two different file systems mounted on */dr1* and */dr2*, yet still display the results onscreen using **less**.

You can also combine the *tee* and *pager* functions. Have a *tee* file enabled and *pager* set to **less**, and you are able to browse the results using the **less** program and still have everything appended into a file the same time. The difference between the Unix *tee* used with the *pager* command and the **mysql** built-in *tee* command is that the built-in *tee* works even if you do not have the Unix **tee** available. The built-in *tee* also logs everything that is printed on the screen, whereas the Unix **tee** used with *pager* does not log quite that much. Additionally, *tee* file logging can be turned on and off interactively from within **mysql**. This is useful when you want to log some queries to a file, but not others.

The `prompt` command reconfigures the default `mysql>` prompt. The string for defining the prompt can contain the following special sequences.

|**Option**|**Description**|
|:--|--|
|\\C|The current connection identifier|
|\\c|A counter that increments for each statement you issue|
|\\D|The full current date|
|\\d|The default database|
|\\h|The server host|
|\\l|The current delimiter|
|\\m|Minutes of the current time|
|\\n|A newline character|
|\\O|The current month in three-letter format (Jan, Feb, …)|
|\\o|The current month in numeric format|
|\\P|am/pm|
|\\p|The current TCP/IP port or socket file|
|\\R|The current time, in 24-hour military time (0–23)|
|\\r|The current time, standard 12-hour time (1–12)|
|\\S|Semicolon|
|\\s|Seconds of the current time|
|\\T|Print an asterisk (*) if the current session is inside a transaction block (from MySQL 8.0.28)|
|\\t|A tab character|
|\\U|Your full *user_name@host_name* account name|
|\\u|Your user name|
|\\v|The server version|
|\\w|The current day of the week in three-letter format (Mon, Tue, …)|
|\\Y|The current year, four digits|
|\\y|The current year, two digits|
|\\_|A space|
|\\ |A space (a space follows the backslash)|
|\\'|Single quote|
|\\"|Double quote|
|\\\\ |A literal \\ backslash character|
|\\**x**|**x**, for any "**x**" not listed above|

You can set the prompt in several ways:

- ***Use an environment variable.*** You can set the `MYSQL_PS1` environment variable to a prompt string. For example:

    ```terminal
    export MYSQL_PS1="(\u@\h) [\d]> "
    ```

- ***Use a command-line option.*** You can set the `--prompt` option on the command line to **mysql**. For example:

    ```terminal
    $> mysql --prompt="(\u@\h) [\d]> "
    (user@host) [database]>
    ```

- ***Use an option file.*** You can set the `prompt` option in the `[mysql]` group of any MySQL option file, such as */etc/my.cnf* or the *.my.cnf* file in your home directory. For example:

    ```ini
    [mysql]
    prompt=(\\u@\\h) [\\d]>\\_
    ```

    In this example, note that the backslashes are doubled. If you set the `prompt` using the prompt option in an option file, it is advisable to double the backslashes when using the special prompt options. There is some overlap in the set of permissible prompt options and the set of special escape sequences that are recognized in option files. (The rules for escape sequences in option files are listed in ["Using Option Files"](https://dev.mysql.com/doc/refman/8.0/en/option-files.html).) The overlap may cause you problems if you use single backslashes. For example, `\s` is interpreted as a space rather than as the current seconds value. The following example shows how to define a prompt within an option file to include the current time in ***hh:mm:ss>*** format:

    ```ini
    [mysql]
    prompt="\\r:\\m:\\s> "
    ```

- ***Set the prompt interactively.*** You can change your prompt interactively by using the `prompt` (or `\R`) command. For example:

    ```sql
    mysql> prompt (\u@\h) [\d]>\_
    PROMPT set to '(\u@\h) [\d]>\_'
    (user@host) [database]>
    (user@host) [database]> prompt
    Returning to default PROMPT of mysql>
    mysql>
    ```

## mysql Client Logging

The **mysql** client can do these types of logging for statements executed interactively:

- On Unix, **mysql** writes the statements to a history file. By default, this file is named `.mysql_history` in your home directory. To specify a different file, set the value of the `MYSQL_HISTFILE` environment variable.

- On all platforms, if the `--syslog` option is given, **mysql** writes the statements to the system logging facility. On Unix, this is `syslog;` on Windows, it is the Windows Event Log. The destination where logged messages appear is system dependent. On Linux, the destination is often the */var/log/messages* file.

The following discussion describes characteristics that apply to all logging types and provides information specific to each logging type.

- How Logging Occurs

- Controlling the History File

- syslog Logging Characteristics

### How Logging Occurs

For each enabled logging destination, statement logging occurs as follows:

- Statements are logged only when executed interactively. Statements are noninteractive, for example, when read from a file or a pipe. It is also possible to suppress statement logging by using the `--batch` or `--execute` option.

- Statements are ignored and not logged if they match any pattern in the "ignore" list. This list is described later.

- **mysql** logs each nonignored, nonempty statement line individually.

- If a nonignored statement spans multiple lines (not including the terminating delimiter), **mysql** concatenates the lines to form the complete statement, maps newlines to spaces, and logs the result, plus a delimiter.

Consequently, an input statement that spans multiple lines can be logged twice. Consider this input:

```sql
mysql> SELECT
    -> 'Today is'
    -> ,
    -> CURDATE()
    -> ;
```

In this case, **mysql** logs the "SELECT", "'Today is'", ",", "CURDATE()", and ";" lines as it reads them. It also logs the complete statement, after mapping `SELECT\n'Today is'\n,\nCURDATE()` to `SELECT 'Today is' , CURDATE()`, plus a delimiter. Thus, these lines appear in logged output:

```sql
SELECT
'Today is'
,
CURDATE()
;
SELECT 'Today is' , CURDATE();
```

**mysql** ignores for logging purposes statements that match any pattern in the "ignore" list. By default, the pattern list is `"*IDENTIFIED*:*PASSWORD*"`, to ignore statements that refer to passwords. Pattern matching is not case-sensitive. Within patterns, two characters are special:

- **?** matches any single character.

- **\*** matches any sequence of zero or more characters.

To specify additional patterns, use the `--histignore` option or set the `MYSQL_HISTIGNORE` environment variable. (If both are specified, the option value takes precedence.) The value should be a list of one or more colon-separated patterns, which are appended to the default pattern list.

Patterns specified on the command line might need to be quoted or escaped to prevent your command interpreter from treating them specially. For example, to suppress logging for `UPDATE` and `DELETE` statements in addition to statements that refer to passwords, invoke **mysql** like this:

```terminal
mysql --histignore="*UPDATE*:*DELETE*"
```

### Controlling the History File

The `.mysql_history` file should be protected with a restrictive access mode because sensitive information might be written to it, such as the text of SQL statements that contain passwords. See ["End-User Guidelines for Password Security"](https://dev.mysql.com/doc/refman/8.0/en/password-security-user.html). Statements in the file are accessible from the **mysql** client when the **up-arrow** key is used to recall the history. See [Disabling Interactive History](https://dev.mysql.com/doc/refman/8.0/en/mysql-tips.html#mysql-history).

If you do not want to maintain a history file, first remove `.mysql_history` if it exists. Then use either of the following techniques to prevent it from being created again:

- Set the `MYSQL_HISTFILE` environment variable to `/dev/null`. To cause this setting to take effect each time you log in, put it in one of your shell's startup files.

- Create `.mysql_history` as a symbolic link to `/dev/null`; this need be done only once:

```terminal
ln -s /dev/null $HOME/.mysql_history
```

### syslog Logging Characteristics

If the `--syslog` option is given, **mysql** writes interactive statements to the system logging facility. Message logging has the following characteristics.

Logging occurs at the "information" level. This corresponds to the `LOG_INFO` priority for `syslog` on Unix/Linux `syslog` capability and to `EVENTLOG_INFORMATION_TYPE` for the Windows Event Log. Consult your system documentation for configuration of your logging capability.

Message size is limited to 1024 bytes.

Messages consist of the identifier `MysqlClient` followed by these values:

- `SYSTEM_USER`

    The operating system user name (login name) or -- if the user is unknown.

- `MYSQL_USER`

    The MySQL user name (specified with the `--user` option) or -- if the user is unknown.

- `CONNECTION_ID:`

    The client connection identifier. This is the same as the `CONNECTION_ID()` function value within the session.

- `DB_SERVER`

    The server host or \-\- if the host is unknown.

- `DB`

    The default database or \-\- if no database has been selected.

- `QUERY`

    The text of the logged statement.

Here is a sample of output generated on Linux by using `--syslog`. This output is formatted for readability; each logged message actually takes a single line.

```
Mar  7 12:39:25 myhost MysqlClient[20824]:
  SYSTEM_USER:'oscar', MYSQL_USER:'my_oscar', CONNECTION_ID:23,
  DB_SERVER:'127.0.0.1', DB:'--', QUERY:'USE test;'
Mar  7 12:39:28 myhost MysqlClient[20824]:
  SYSTEM_USER:'oscar', MYSQL_USER:'my_oscar', CONNECTION_ID:23,
  DB_SERVER:'127.0.0.1', DB:'test', QUERY:'SHOW TABLES;'
```

## mysql Client Server-Side Help

```
mysql> help search_string
```

If you provide an argument to the `help` command, **mysql** uses it as a search string to access server-side help from the contents of the MySQL Reference Manual. The proper operation of this command requires that the help tables in the **mysql** database be initialized with help topic information (see ["Server-Side Help Support"](https://dev.mysql.com/doc/refman/8.0/en/server-side-help-support.html)).

If there is no match for the search string, the search fails:

```
mysql> help me

Nothing found
Please try to run 'help contents' for a list of all accessible topics
```

Use [help contents](https://dev.mysql.com/doc/refman/8.0/en/help.html) to see a list of the help categories:

```
mysql> help contents
You asked for help about help category: "Contents"
For more information, type 'help <item>', where <item> is one of the
following categories:
   Account Management
   Administration
   Data Definition
   Data Manipulation
   Data Types
   Functions
   Functions and Modifiers for Use with GROUP BY
   Geographic Features
   Language Structure
   Plugins
   Storage Engines
   Stored Routines
   Table Maintenance
   Transactions
   Triggers
```

If the search string matches multiple items, **mysql** shows a list of matching topics:

```
mysql> help logs
Many help items for your request exist.
To make a more specific request, please type 'help <item>',
where <item> is one of the following topics:
   SHOW
   SHOW BINARY LOGS
   SHOW ENGINE
   SHOW LOGS
```

Use a topic as the search string to see the help entry for that topic:

```
mysql> help show binary logs
Name: 'SHOW BINARY LOGS'
Description:
Syntax:
SHOW BINARY LOGS
SHOW MASTER LOGS

Lists the binary log files on the server. This statement is used as
part of the procedure described in [purge-binary-logs], that shows how
to determine which logs can be purged.
```

```sql
mysql> SHOW BINARY LOGS;
+---------------+-----------+-----------+
| Log_name      | File_size | Encrypted |
+---------------+-----------+-----------+
| binlog.000015 |    724935 | Yes       |
| binlog.000016 |    733481 | Yes       |
+---------------+-----------+-----------+
```

The search string can contain the wildcard characters `%` and `_`. These have the same meaning as for pattern-matching operations performed with the `LIKE` operator. For example, `HELP rep%` returns a list of topics that begin with `rep`:

```
mysql> HELP rep%
Many help items for your request exist.
To make a more specific request, please type 'help <item>',
where <item> is one of the following
topics:
   REPAIR TABLE
   REPEAT FUNCTION
   REPEAT LOOP
   REPLACE
   REPLACE FUNCTION
```

## Executing SQL Statements from a Text File

The **mysql** client typically is used interactively, like this:

```terminal
mysql db_name
```

However, it is also possible to put your SQL statements in a file and then tell **mysql** to read its input from that file. To do so, create a text file `text_file` that contains the statements you wish to execute. Then invoke **mysql** as shown here:

```terminal
mysql db_name < text_file
```

If you place a `USE db_name` statement as the first statement in the file, it is unnecessary to specify the database name on the command line:

```terminal
mysql < text_file
```

If you are already running **mysql**, you can execute an SQL script file using the `source` command or `\.` command:

```sql
mysql> source file_name
mysql> \. file_name
```

Sometimes you may want your script to display progress information to the user. For this you can insert statements like this:

```sql
SELECT '<info_to_display>' AS ' ';
```

The statement shown outputs `<info_to_display>`.

You can also invoke **mysql** with the `--verbose` option, which causes each statement to be displayed before the result that it produces.

**mysql** ignores Unicode byte order mark (BOM) characters at the beginning of input files. Previously, it read them and sent them to the server, resulting in a syntax error. Presence of a BOM does not cause **mysql** to change its default character set. To do that, invoke **mysql** with an option such as `--default-character-set=utf8mb4`.

For more information about batch mode, see Section ["Using mysql in Batch Mode"](https://dev.mysql.com/doc/refman/8.0/en/batch-mode.html).

## mysql Client Tips

This section provides information about techniques for more effective use of **mysql** and about **mysql** operational behavior.

- Input-Line Editing

- Disabling Interactive History

- Unicode Support on Windows

- Displaying Query Results Vertically

- Using Safe-Updates Mode (--safe-updates)

- Disabling mysql Auto-Reconnect

- mysql Client Parser Versus Server Parser

### Input-Line Editing

**mysql** supports input-line editing, which enables you to modify the current input line in place or recall previous input lines. For example, the `left-arrow` and `right-arrow` keys move horizontally within the current input line, and the `up-arrow` and `down-arrow` keys move up and down through the set of previously entered lines. `Backspace` deletes the character before the cursor and typing new characters enters them at the cursor position. To enter the line, press `Enter`.

On Windows, the editing key sequences are the same as supported for command editing in console windows. On Unix, the key sequences depend on the input library used to build **mysql** (for example, the `libedit` or `readline` library).

Documentation for the `libedit` and `readline` libraries is available online. To change the set of key sequences permitted by a given input library, define key bindings in the library startup file. This is a file in your home directory: `.editrc` for `libedit` and `.inputrc` for `readline`.

For example, in `libedit`, `Control+W` deletes everything before the current cursor position and `Control+U` deletes the entire line. In `readline`, `Control+W` deletes the word before the cursor and `Control+U` deletes everything before the current cursor position. If **mysql** was built using `libedit`, a user who prefers the `readline` behavior for these two keys can put the following lines in the `.editrc` file (creating the file if necessary):

```terminal
bind "^W" ed-delete-prev-word
bind "^U" vi-kill-line-prev
```

To see the current set of key bindings, temporarily put a line that says only bind at the end of `.editrc.` **mysql** shows the bindings when it starts.

### Disabling Interactive History

The `up-arrow` key enables you to recall input lines from current and previous sessions. In cases where a console is shared, this behavior may be unsuitable. **mysql** supports disabling the interactive history partially or fully, depending on the host platform.

On Windows, the history is stored in memory. `Alt+F7` deletes all input lines stored in memory for the current history buffer. It also deletes the list of sequential numbers in front of the input lines displayed with `F7` and recalled (by number) with `F9`. New input lines entered after you press `Alt+F7` repopulate the current history buffer. Clearing the buffer does not prevent logging to the Windows Event Viewer, if the `--syslog` option was used to start **mysql**. Closing the console window also clears the current history buffer.

To disable interactive history on Unix, first delete the `.mysql_history` file, if it exists (previous entries are recalled otherwise). Then start **mysql** with the `--histignore="*"` option to ignore all new input lines. To re-enable the recall (and logging) behavior, restart **mysql** without the option.

If you prevent the `.mysql_history` file from being created (see [Controlling the History File](https://dev.mysql.com/doc/refman/8.0/en/mysql-logging.html#mysql-logging-history-file)) and use `--histignore="*"` to start the **mysql** client, the interactive history recall facility is disabled fully. Alternatively, if you omit the `--histignore` option, you can recall the input lines entered during the current session.

### Unicode Support on Windows

Windows provides APIs based on UTF-16LE for reading from and writing to the console; the **mysql** client for Windows is able to use these APIs. The Windows installer creates an item in the MySQL menu named `MySQL command line client - Unicode`. This item invokes the **mysql** client with properties set to communicate through the console to the MySQL server using Unicode.

To take advantage of this support manually, run **mysql** within a console that uses a compatible Unicode font and set the default character set to a Unicode character set that is supported for communication with the server:

1. Open a console window.

2. Go to the console window properties, select the font tab, and choose Lucida Console or some other compatible Unicode font. This is necessary because console windows start by default using a DOS raster font that is inadequate for Unicode.

3. Execute **mysql.exe** with the `--default-character-set=utf8mb4` (or `utf8mb3`) option. This option is necessary because `utf16le` is one of the character sets that cannot be used as the client character set. See [Impermissible Client Character Sets](https://dev.mysql.com/doc/refman/8.0/en/charset-connection.html#charset-connection-impermissible-client-charset).

With those changes, **mysql** uses the Windows APIs to communicate with the console using UTF-16LE, and communicate with the server using UTF-8. (The menu item mentioned previously sets the font and character set as just described.)

To avoid those steps each time you run **mysql**, you can create a shortcut that invokes **mysql.exe**. The shortcut should set the console font to Lucida Console or some other compatible Unicode font, and pass the `--default-character-set=utf8mb4` (or `utf8mb3`) option to **mysql.exe**.

Alternatively, create a shortcut that only sets the console font, and set the character set in the `[mysql]` group of your `my.ini` file:

```ini
[mysql]
default-character-set=utf8mb4   # or utf8mb3
```

### Displaying Query Results Vertically

Some query results are much more readable when displayed vertically, instead of in the usual horizontal table format. Queries can be displayed vertically by terminating the query with \\G instead of a semicolon. For example, longer text values that include newlines often are much easier to read with vertical output:

```sql
mysql> SELECT * FROM mails WHERE LENGTH(txt) < 300 LIMIT 300,1\G
*************************** 1. row ***************************
  msg_nro: 3068
     date: 2000-03-01 23:29:50
time_zone: +0200
mail_from: Jones
    reply: jones@example.com
  mail_to: "John Smith" <smith@example.com>
      sbj: UTF-8
      txt: >>>>> "John" == John Smith writes:

John> Hi.  I think this is a good idea.  Is anyone familiar
John> with UTF-8 or Unicode? Otherwise, I'll put this on my
John> TODO list and see what happens.

Yes, please do that.

Regards,
Jones
     file: inbox-jani-1
     hash: 190402944
1 row in set (0.09 sec)
```

### Using Safe-Updates Mode (--safe-updates)

For beginners, a useful startup option is `--safe-updates` (or `--i-am-a-dummy`, which has the same effect). Safe-updates mode is helpful for cases when you might have issued an `UPDATE` or `DELETE` statement but forgotten the `WHERE` clause indicating which rows to modify. Normally, such statements update or delete all rows in the table. With `--safe-updates`, you can modify rows only by specifying the key values that identify them, or a `LIMIT` clause, or both. This helps prevent accidents. Safe-updates mode also restricts `SELECT` statements that produce (or are estimated to produce) very large result sets.

The `--safe-updates` option causes **mysql** to execute the following statement when it connects to the MySQL server, to set the session values of the `sql_safe_updates`, `sql_select_limit`, and `max_join_size` system variables:

```sql
SET sql_safe_updates=1, sql_select_limit=1000, max_join_size=1000000;
```

The `SET` statement affects statement processing as follows:

- Enabling `sql_safe_updates` causes `UPDATE` and `DELETE` statements to produce an error if they do not specify a key constraint in the WHERE clause, or provide a `LIMIT` clause, or both. For example:

    ```sql
    UPDATE tbl_name SET not_key_column=val WHERE key_column=val;

    UPDATE tbl_name SET not_key_column=val LIMIT 1;
    ```

- Setting `sql_select_limit` to 1,000 causes the server to limit all `SELECT` result sets to 1,000 rows unless the statement includes a `LIMIT` clause.

- Setting `max_join_size` to 1,000,000 causes multiple-table `SELECT` statements to produce an error if the server estimates it must examine more than 1,000,000 row combinations.

To specify result set limits different from 1,000 and 1,000,000, you can override the defaults by using the `--select-limit` and `--max-join-size` options when you invoke **mysql**:

```terminal
mysql --safe-updates --select-limit=500 --max-join-size=10000
```

It is possible for `UPDATE` and `DELETE` statements to produce an error in safe-updates mode even with a key specified in the `WHERE` clause, if the optimizer decides not to use the index on the key column:

- Range access on the index cannot be used if memory usage exceeds that permitted by the `range_optimizer_max_mem_size` system variable. The optimizer then falls back to a table scan. See [Limiting Memory Use for Range Optimization](https://dev.mysql.com/doc/refman/8.0/en/range-optimization.html#range-optimization-memory-use).

- If key comparisons require type conversion, the index may not be used (see ["How MySQL Uses Indexes"](https://dev.mysql.com/doc/refman/8.0/en/mysql-indexes.html)). Suppose that an indexed string column `c1` is compared to a numeric value using `WHERE c1 = 2222`. For such comparisons, the string value is converted to a number and the operands are compared numerically (see ["Type Conversion in Expression Evaluation"](https://dev.mysql.com/doc/refman/8.0/en/type-conversion.html)), preventing use of the index. If safe-updates mode is enabled, an error occurs.

As of MySQL 8.0.13, safe-updates mode also includes these behaviors:

- `EXPLAIN` with `UPDATE` and `DELETE` statements does not produce safe-updates errors. This enables use of `EXPLAIN` plus `SHOW WARNINGS` to see why an index is not used, which can be helpful in cases such as when a `range_optimizer_max_mem_size` violation or type conversion occurs and the optimizer does not use an index even though a key column was specified in the `WHERE` clause.

- When a safe-updates error occurs, the error message includes the first diagnostic that was produced, to provide information about the reason for failure. For example, the message may indicate that the `range_optimizer_max_mem_size` value was exceeded or type conversion occurred, either of which can preclude use of an index.

- For multiple-table deletes and updates, an error is produced with safe updates enabled only if any target table uses a table scan.

### Disabling mysql Auto-Reconnect

If the **mysql** client loses its connection to the server while sending a statement, it immediately and automatically tries to reconnect once to the server and send the statement again. However, even if **mysql** succeeds in reconnecting, your first connection has ended and all your previous session objects and settings are lost: temporary tables, the autocommit mode, and user-defined and session variables. Also, any current transaction rolls back. This behavior may be dangerous for you, as in the following example where the server was shut down and restarted between the first and second statements without you knowing it:

```sql
mysql> SET @a=1;
Query OK, 0 rows affected (0.05 sec)

mysql> INSERT INTO t VALUES(@a);
ERROR 2006: MySQL server has gone away
No connection. Trying to reconnect...
Connection id:    1
Current database: test

Query OK, 1 row affected (1.30 sec)

mysql> SELECT * FROM t;
+------+
| a    |
+------+
| NULL |
+------+
1 row in set (0.05 sec)
```

The @a user variable has been lost with the connection, and after the reconnection it is undefined. If it is important to have **mysql** terminate with an error if the connection has been lost, you can start the **mysql** client with the `--skip-reconnect` option.

For more information about auto-reconnect and its effect on state information when a reconnection occurs, see [Automatic Reconnection Control](https://dev.mysql.com/doc/c-api/8.0/en/c-api-auto-reconnect.html).

### mysql Client Parser Versus Server Parser

The **mysql** client uses a parser on the client side that is not a duplicate of the complete parser used by the **mysqld** server on the server side. This can lead to differences in treatment of certain constructs. Examples:

- The server parser treats strings delimited by " characters as identifiers rather than as plain strings if the `ANSI_QUOTES` SQL mode is enabled.

    The **mysql** client parser does not take the `ANSI_QUOTES` SQL mode into account. It treats strings delimited by ", ', and \` characters the same, regardless of whether `ANSI_QUOTES` is enabled.

- Within \/\*\! ... \*\/ and \/\*\+ ... \*\/ comments, the **mysql** client parser interprets short-form **mysql** commands. The server parser does not interpret them because these commands have no meaning on the server side.

    If it is desirable for **mysql** not to interpret short-form commands within comments, a partial workaround is to use the `--binary-mode` option, which causes all **mysql** commands to be disabled except `\C` and `\d` in noninteractive mode (for input piped to **mysql** or loaded using the `source` command).