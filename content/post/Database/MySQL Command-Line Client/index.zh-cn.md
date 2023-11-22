---
title: MySQL 命令行客户端
description: MySQL Command-Line Client
date: '2023-11-22'
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

在 Unix 上，mysql 客户端会将交互执行的语句记录到历史文件中。请参阅 [mysql Client Logging](https://javenjin.github.io/blog/zh-cn/p/mysql-%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%AE%A2%E6%88%B7%E7%AB%AF/#mysql-%E5%AE%A2%E6%88%B7%E7%AB%AF%E6%97%A5%E5%BF%97)。

## mysql 客户端选项

**mysql** supports the following options, which can be specified on the command line or in the `[mysql]` and `[client]` groups of an option file. For information about option files used by MySQL programs, see [Using Option Files](https://dev.mysql.com/doc/refman/8.0/en/option-files.html).

**mysql**支持以下选项，这些选项可以在命令行或选项文件的`[mysql]`和`[client]`组中指定。有关 MySQL 程序使用的选项文件的信息，请参阅 [Using Option Files](https://dev.mysql.com/doc/refman/8.0/en/option-files.html)。

|**选项名称**|**描述**|**引入版本**|**废弃版本**|
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

禁用命名命令。只使用 \\* 形式，或只在以分号（;）结尾的行首使用命名命令。默认情况下，**mysql**启动时该选项已*enabled*。不过，即使使用该选项，长格式命令仍可从第一行开始执行。参见["mysql Client Commands"](https://javenjin.github.io/blog/zh-cn/p/mysql-%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%AE%A2%E6%88%B7%E7%AB%AF/#mysql-%E5%AE%A2%E6%88%B7%E7%AB%AF%E5%91%BD%E4%BB%A4)。

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

由一个或多个冒号分隔模式组成的列表，用于指定忽略日志记录的语句。这些模式会添加到默认模式列表（"\*IDENTIFIED\*:\*PASSWORD\*"）中。为该选项指定的值会影响写入历史文件的语句的日志记录，如果给定了 `--syslog`选项，还会影响写入 syslog 的日志记录。更多信息，请参阅["mysql Client Logging"](https://javenjin.github.io/blog/zh-cn/p/mysql-%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%AE%A2%E6%88%B7%E7%AB%AF/#mysql-%E5%AE%A2%E6%88%B7%E7%AB%AF%E6%97%A5%E5%BF%97)。

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

Enable named **mysql** commands. Long-format commands are permitted, not just short-format commands. For example, `quit` and `\q` both are recognized. Use `--skip-named-commands` to disable named commands. See ["mysql Client Commands"](https://javenjin.github.io/blog/zh-cn/p/mysql-%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%AE%A2%E6%88%B7%E7%AB%AF/#mysql-%E5%AE%A2%E6%88%B7%E7%AB%AF%E5%91%BD%E4%BB%A4).

启用已命名的 **mysql** 命令。允许使用长格式命令，而不仅仅是短格式命令。例如，`quit`和`\q`都能被识别。使用 `-skip-named-commands`禁用命名命令。参见["mysql Client Commands"](https://javenjin.github.io/blog/zh-cn/p/mysql-%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%AE%A2%E6%88%B7%E7%AB%AF/#mysql-%E5%AE%A2%E6%88%B7%E7%AB%AF%E5%91%BD%E4%BB%A4)。

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

使用给定命令对查询输出进行分页。如果省略该命令，默认分页器就是 *PAGER* 环境变量的值。有效的分页器有**less**、**more**、**cat [> filename]** 等。该选项仅在 Unix 和交互模式下有效。要禁用分页功能，请使用 `-skip-pager`。请参阅["mysql Client Commands"](https://javenjin.github.io/blog/zh-cn/p/mysql-%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%AE%A2%E6%88%B7%E7%AB%AF/#mysql-%E5%AE%A2%E6%88%B7%E7%AB%AF%E5%91%BD%E4%BB%A4)节将进一步讨论输出分页。

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

如果启用了该选项，在 WHERE 子句中未使用键或 `LIMIT` 子句的 `UPDATE` 和 `DELETE` 语句将产生错误。此外，对产生（或估计会产生）超大结果集的 `SELECT` 语句也会进行限制。如果在选项文件中设置了该选项，可以在命令行中使用 `-skip-safe-updates`来覆盖它。有关该选项的更多信息，请参阅[Using Safe-Updates Mode (--safe-updates)](https://javenjin.github.io/blog/zh-cn/p/mysql-%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%AE%A2%E6%88%B7%E7%AB%AF/#%E4%BD%BF%E7%94%A8%E5%AE%89%E5%85%A8%E6%9B%B4%E6%96%B0%E6%A8%A1%E5%BC%8F---safe-updates)。

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

控制是否在客户端启用 FIPS 模式。`--ssl-fips-mode`选项与其他`--ssl-xxx`选项不同，它不是用来建立加密连接，而是影响允许哪些加密操作。请参阅["FIPS Support"](https://dev.mysql.com/doc/refman/8.0/en/fips-mode.html)。

允许使用这些`--ssl-fips-mode`值：

- OFF: 禁用 FIPS 模式。

- ON: 启用 FIPS 模式。

- STRICT: 启用 "strict" FIPS 模式。

> **注意：**如果 OpenSSL FIPS 对象模块不可用，`-ssl-fips-mode` 的唯一允许值是 OFF。在这种情况下，将 `-ssl-fips-mode` 设置为 *ON* 或 *STRICT* 会导致客户端在启动时发出警告，并以非 FIPS 模式运行。

自 MySQL 8.0.34 起，该选项已被弃用。预计未来的 MySQL 版本将删除该选项。

### \-\-syslog, -j

|**Command-Line Format**|**\-\-syslog**|
|:--|--|

该选项会使**mysql**向系统日志设备发送交互式语句。在 Unix 系统中，这是 *syslog*；在 Windows 系统中，这是 Windows 事件日志。记录信息的目的地取决于系统。在 Linux 系统中，目的地通常是 */var/log/messages* 文件。

下面是使用 `--syslog` 在 Linux 上生成的输出示例。为便于阅读，该输出已格式化；每条记录的信息实际上只占一行。

```
Mar  7 12:39:25 myhost MysqlClient[20824]:
  SYSTEM_USER:'oscar', MYSQL_USER:'my_oscar', CONNECTION_ID:23,
  DB_SERVER:'127.0.0.1', DB:'--', QUERY:'USE test;'
Mar  7 12:39:28 myhost MysqlClient[20824]:
  SYSTEM_USER:'oscar', MYSQL_USER:'my_oscar', CONNECTION_ID:23,
  DB_SERVER:'127.0.0.1', DB:'test', QUERY:'SHOW TABLES;'
```

更多信息，请参阅["mysql Client Logging"](https://javenjin.github.io/blog/zh-cn/p/mysql-%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%AE%A2%E6%88%B7%E7%AB%AF/#mysql-%E5%AE%A2%E6%88%B7%E7%AB%AF%E6%97%A5%E5%BF%97)。

### \-\-table, -t

|**Command-Line Format**|**\-\-table**|
|:--|--|

以表格格式显示输出。这是交互式使用的默认设置，但也可用于在批处理模式下生成表格输出。

### \-\-tee-*file_name*

|**Command-Line Format**|**\-\-tee=file_name**|
|:--|--|
|**Type**|**File name**|

将输出副本附加到指定文件。该选项仅在交互模式下有效。请参阅["mysql Client Commands"](https://javenjin.github.io/blog/zh-cn/p/mysql-%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%AE%A2%E6%88%B7%E7%AB%AF/#mysql-%E5%AE%A2%E6%88%B7%E7%AB%AF%E5%91%BD%E4%BB%A4) ，将进一步讨论 tee 文件。

### \-\-tls-ciphersuites=*ciphersuite_list*

|**Command-Line Format**|**\-\-tls-ciphersuites=ciphersuite_list**|
|:--|--|
|**Introduced**|**8.0.16**|
|**Type**|**String**|

使用 TLSv1.3 的加密连接允许使用的密码套件。该值是一个或多个以冒号分隔的密码组名称列表。可为该选项命名的密码库取决于编译 MySQL 时使用的 SSL 库。详情请参阅["Encrypted Connection TLS Protocols and Ciphers"](https://dev.mysql.com/doc/refman/8.0/en/encrypted-connection-protocols-ciphers.html)。

This option was added in MySQL 8.0.16.

### \-\-tls-version=*protocol_list*

|**Command-Line Format**|**\-\-tls-version=protocol_list**|
|:--|--|
|**Type**|**String**|
|**Default Value(≥ 8.0.19)**|**TLSv1,TLSv1.1,TLSv1.2,TLSv1.3 (OpenSSL 1.1.1 or higher) / TLSv1,TLSv1.1,TLSv1.2 (otherwise)**|
|**Default Value(≤ 8.0.18)**|**TLSv1,TLSv1.1,TLSv1.2**|

允许用于加密连接的 TLS 协议。值是一个或多个以逗号分隔的协议名称列表。可以为该选项命名的协议取决于编译 MySQL 时使用的 SSL 库。详情请参阅["Encrypted Connection TLS Protocols and Ciphers"](https://dev.mysql.com/doc/refman/8.0/en/encrypted-connection-protocols-ciphers.html)。

### \-\-unbuffered, -n

|**Command-Line Format**|**\-\-unbuffered**|
|:--|--|

每次查询后清空缓冲区。

### \-\-user=*user_name*, -u *user_name*

|**Command-Line Format**|**\-\-user=user_name**|
|:--|--|
|**Type**|**String**|

用于连接服务器的 MySQL 账户的用户名。

### \-\-verbose, -v

|**Command-Line Format**|**\-\-verbose**|
|:--|--|

详细模式。输出更多有关程序运行的信息。该选项可以多次使用，以产生越来越多的输出。（例如，-v -v -v 即使在批处理模式下也能产生表格输出格式）。

### \-\-version, -V

|**Command-Line Format**|**\-\-version**|
|:--|--|

显示版本信息并退出。

### \-\-vertical, -E

|**Command-Line Format**|**\-\-vertical**|
|:--|--|

垂直打印查询输出行（每列值一行）。如果不使用该选项，可以通过以 \G 结束单个语句来指定垂直输出。

### \-\-wait, -w

|**Command-Line Format**|**\-\-wait**|
|:--|--|

如果无法建立连接，请等待并重试，而不是放弃。

### \-\-xml, -X

|**Command-Line Format**|**\-\-xml**|
|:--|--|

生成 XML 输出。

```xml
<field name="column_name">NULL</field>
```

当 `--xml` 与 **mysql** 一起使用时，输出结果与 **mysqldump** `--xml` 的输出结果一致。详见["mysqldump — A Database Backup Program"](https://dev.mysql.com/doc/refman/8.0/en/mysqldump.html)。

XML 输出也使用 XML 命名空间，如图所示：

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

使用 zstd 压缩算法的服务器连接所使用的压缩级别。允许的压缩级别从 1 到 22，数值越大，压缩级别越高。默认的 zstd 压缩级别为 3。 压缩级别设置对不使用 zstd 压缩的连接没有影响。

更多信息，请参阅["Connection Compression Control"](https://dev.mysql.com/doc/refman/8.0/en/connection-compression-control.html)。

此选项在 MySQL 8.0.18 中添加。

## mysql 客户端命令

**mysql** 会将你发出的每条 SQL 语句发送到服务器执行。此外，**mysql**本身也会解释一组命令。要查看这些命令的列表，请在 `mysql>` 提示符下键入 `help` 或 `\h`：

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

如果在调用**mysql**时使用了`--binary-mode`选项，那么在非交互模式下（对于通过管道输入到**mysql**或使用*source*命令加载的输入），除了*charset*和*delimiter*之外，所有**mysql**命令都会被禁用。

每条命令都有长、短两种形式。长命令不区分大小写，短命令区分大小写。长命令后可以加上分号结束符，但短命令则不可以。

不支持在多行 /\* ... \*/ 注释中使用短格式命令。短格式命令可以在单行 /\*! ... \*/ 版本注释中使用，存储在对象定义中的 /\*+ ... \*/ 优化器提示注释也是如此。如果担心优化器提示注释可能存储在对象定义中，从而导致在使用 *mysql* 重载转储文件时执行此类命令，则应使用 `--binary-mode` 选项调用 **mysql**，或使用 **mysql**以外的重载客户端。

- help \[*arg*\], \\h \[*arg*\], \\? \[*arg*\], ? \[*arg*\]

    显示帮助信息，列出可用的 mysql 命令。
    
    如果为 *help* 命令提供参数，**mysql** 会将其用作搜索字符串，从《MySQL 参考手册》的内容中访问服务器端帮助。更多信息，请参阅["mysql Client Server-Side Help"](https://javenjin.github.io/blog/zh-cn/p/mysql-%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%AE%A2%E6%88%B7%E7%AB%AF/#syslog-%E6%97%A5%E5%BF%97%E7%89%B9%E5%BE%81)。

- charset *charset_name*, \\C *charset_name*

    更改默认字符集并发布一条 `SET NAMES` 语句。这样，如果 **mysql** 运行时启用了自动重新连接（不建议这样做），客户端和服务器上的字符集就能保持同步，因为重新连接时会使用指定的字符集。

- clear, \\c

    清除当前输入。如果改变主意不执行正在输入的语句，请使用此功能。

- connect \[*db_name* \[*host_name*\]\], \\r \[*db_name* \[*host_name*\]\]

    重新连接服务器。可选的数据库名称和主机名称参数可用于指定默认数据库或运行服务器的主机。如果省略，则使用当前值。

    如果 connect 命令指定了主机名参数，则该主机优先于在 **mysql** 启动时指定 DNS SRV 记录的任何 `--dns-srv-name` 选项。

- delimiter *str*, \\d *str*

    更改**mysql**解释为 SQL 语句之间分隔符的字符串。默认为分号（;）。

    分隔符字符串可以在 *delimiter* 命令行中指定为无引号或有引号参数。引号可以使用单引号（'）、双引号（"）或回车键（`）字符。要在引号字符串中包含引号，可以使用不同的引号字符或反斜杠（\\）字符转义引号。在引号字符串之外应避免使用反斜杠，因为它是 MySQL 的转义字符。对于未加引号的参数，分隔符一直读到第一个空格或行尾。对于带引号的参数，分隔符读到行中匹配的引号为止。

    除了在带引号的字符串中，**mysql** 会将任何分隔符字符串实例解释为语句分隔符。在定义可能出现在其他单词中的分隔符时要小心。例如，如果将分隔符定义为 `X`，就不能在语句中使用 `INDEX` 这个词。**mysql** 会将其解释为 INDE，后跟分隔符 `X`。

    当**mysql**识别的分隔符设置为默认的;以外的字符时，该字符的实例无需解释即可发送到服务器。不过，服务器本身仍会将;解释为语句分隔符，并据此处理语句。服务器端的这种行为适用于多语句执行（参见[Multiple Statement Execution Support](https://dev.mysql.com/doc/c-api/8.0/en/c-api-multiple-queries.html)），以及解析存储过程和函数、触发器和事件的正文（参见["Defining Stored Programs"](https://dev.mysql.com/doc/refman/8.0/en/stored-programs-defining.html)）。

- edit, \\e

    编辑当前输入语句。**mysql** 会检查 EDITOR 和 VISUAL 环境变量的值，以确定使用哪个编辑器。如果两个变量都未设置，则默认编辑器为 **vi**。

    *edit* 命令只在 Unix 下运行。

- ego, \\G

    将当前语句发送到服务器执行，并使用垂直格式显示结果。

- exit, \\q

    退出 **mysql**。

- go, \\g

    将当前语句发送到服务器执行。

- nopaper, \\n

    禁用输出分页。请参阅 *pager* 的说明。

    *nopaper*命令仅在Unix系统中有效。

- notee, \\t

    禁用向 tee 文件复制输出。请参阅 *tee* 的说明。

- nowarning, \\w

    禁止在每个语句后显示警告。

- pager \[*command*\], \\P \[*command*\]

    启用输出分页。通过在调用 **mysql** 时使用 `--pager` 选项，可以使用 Unix 程序（如 **less**、**more** 或其他类似程序）在交互模式下浏览或搜索查询结果。如果不指定该选项的值，**mysql** 会检查 `PAGER` 环境变量的值，并将寻呼器设置为该值。寻呼器功能仅在交互模式下工作。

    输出分页可以通过 *pager* 命令交互式启用，也可以通过 *nopager* 命令禁用。该命令包含一个可选参数；如果给出该参数，则分页程序将被设置为该参数。如果没有参数，分页程序将设置为命令行设置的分页程序，如果没有指定分页程序，则设置为 *stdout*。

    输出分页功能仅适用于 Unix 系统，因为它使用了 *popen()* 函数，而 Windows 系统中不存在该函数。在 Windows 中，可以使用 *tee* 选项来保存查询输出，但在某些情况下，它不如 *pager* 方便浏览输出。

- print, \\p

    打印当前输入语句，但不执行该语句。

- prompt \[*str*\], \\R \[*str*\]

    将 **mysql** 提示符重新配置为给定字符串。提示符中可使用的特殊字符序列将在本节后面介绍。

    如果指定不带参数的 `prompt` 命令，**mysql** 会将提示重置为默认的 `mysql>`。

- query_attributes *name* *value* \[*name* *value* ...\]

    定义适用于下一次发送到服务器的查询的查询属性。有关查询属性的目的和用途，请参阅["Query Attributes"](https://dev.mysql.com/doc/refman/8.0/en/query-attributes.html)。

    `query_attributes` 命令遵循这些规则：

    - 属性名和值的格式和引号规则与 `delimiter` 命令相同。

    - 该命令最多允许 32 个属性名/值对。名称和值的长度最多为 1024 个字符。如果给出的名称没有值，则会出错。

    - 如果在执行查询之前发布了多条`query_attributes`命令，则只有最后一条命令适用。发送查询后，**mysql** 会清除属性集。

    - 如果用相同的名称定义了多个属性，尝试检索属性值的结果将是未定义的。

    - 用空名称定义的属性无法通过名称检索。

    - 如果在**mysql**执行查询时发生重新连接，**mysql**会在重新连接后恢复属性，这样就可以用相同的属性再次执行查询。

- quit, \\q

    退出 **mysql**。

- rehash, \\#

    Rebuild the completion hash that enables database, table, and column name completion while you are entering statements. (See the description for the `--auto-rehash` option.)

    重建完成哈希值，以便在输入语句时启用数据库、表和列名完成。（请参阅`--auto-rehash`选项的说明）。

- resetconnection, \\x

    重置连接以清除会话状态。这包括清除使用 `query_attributes` 命令定义的任何当前查询属性。

    重置连接的效果与 `mysql_change_user()` 或自动重新连接类似，但连接不会关闭和重新打开，也不会重新进行身份验证。请参阅 [mysql_change_user()](https://dev.mysql.com/doc/c-api/8.0/en/mysql-change-user.html) 和 [Automatic Reconnection Control](https://dev.mysql.com/doc/c-api/8.0/en/c-api-auto-reconnect.html)。

    本例展示了 `resetconnection` 如何清除会话状态中的一个值：

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

    读取指定文件并执行其中包含的语句。在 Windows 系统中，指定路径名分隔符为 / 或 \\\\。

    引号字符作为文件名本身的一部分。为达到最佳效果，文件名不应包含空格字符。

- ssl_session_data_print \[*file_name*\]

    获取、序列化并存储成功连接的会话数据。可选的文件名和参数可用于指定存储序列化会话数据的文件。如果省略，会话数据将打印到 `stdout`。

    如果 MySQL 会话配置为重复使用，文件中的会话数据将被反序列化，并提供给 *connect* 命令以重新连接。会话重用成功后，*status* 命令将包含一行显示 *SSL session reused: true* 的内容，同时客户端将保持与服务器的重新连接。

- status, \\s

    提供连接和服务器的状态信息。如果启用了 `--safe-updates` 功能，*status* 还会打印影响查询的 **mysql** 变量的值。

- system *command*, \\! *command*

    使用默认命令解释器执行给定命令。

    在 MySQL 8.0.19 之前，*system* 命令只能在 Unix 下运行。从 8.0.19 开始，它也能在 Windows 上运行。

- tee \[*file_name*\], \\T \[*file_name*\]

    在调用 **mysql** 时使用 `--tee` 选项，可以记录语句及其输出。屏幕上显示的所有数据都会追加到指定文件中。这对调试也非常有用。每条语句结束后，**mysql** 会在打印下一条提示语之前将结果刷新到文件中。此功能仅在交互模式下有效。

    您可以使用 *tee* 命令交互式地启用这一功能。如果没有参数，则使用前一个文件。可以使用 notee 命令禁用 *tee* 文件。再次执行 *tee* 可重新启用日志记录功能。

- use *db_name*, \\u *db_name*

    使用 *db_name* 作为默认数据库。

- warnings, \\W

    启用在每条语句后显示警告（如果有的话）。

下面是一些关于 *pager* 命令的提示：

- 您可以用它来写入文件，而且结果只写入文件：

    ```sql
    mysql> pager cat > /tmp/log.txt
    ```

    You can also pass any options for the program that you want to use as your pager:

    ```sql
    mysql> pager less -n -i -S
    ```

- 在前面的示例中，请注意`-S`选项。您可能会发现它在浏览宽查询结果时非常有用。有时，很宽的结果集很难在屏幕上阅读。使用**less**的`-S`选项可以使结果集更易于阅读，因为你可以使用左箭头键和右箭头键水平滚动结果集。您还可以在**less**中交互式地使用`-S`来开关水平浏览模式。更多信息，请阅读**less**手册页面：

    ```terminal
    man less
    ```

- `-F`和`-X`选项可与**less**一起使用，使其在输出适合一个屏幕时退出，这在无需滚动时非常方便：

    ```sql
    mysql> pager less -n -i -S -F -X
    ```

- You can specity very complex pager commands for handling query output:
- 您可以指定非常复杂的pager commands来处理查询输出：

    ```sql
    mysql> pager cat | tee /dr1/tmp/res.txt \
            | tee /dr2/tmp/res2.txt | less -n -i -S
    ```

    在本例中，该命令将把查询结果发送到挂载在 */dr1* 和 */dr2* 上的两个不同文件系统的两个不同目录中的两个文件，但仍使用 **less** 在屏幕上显示结果。

您还可以将*tee*和*pager*功能结合起来。启用*tee*文件并将*pager*设置为**less**，就可以使用**less**程序浏览结果，并同时将所有内容添加到文件中。与*pager*命令一起使用的Unix*tee*和**mysql**内置*tee*命令的区别在于，即使没有Unix**tee**，内置*tee*也能工作。内置 *tee* 还会记录屏幕上打印的所有内容，而与 *pager* 一起使用的 Unix **tee** 则不会记录这么多内容。此外，*tee*文件日志记录可以在**mysql**中以交互方式打开或关闭。当你想将某些查询记录到文件中，而不是其他查询时，这一点非常有用。

`prompt`命令用于重新配置默认的`mysql>`提示符。用于定义提示符的字符串可以包含以下特殊序列。

|**选项**|**描述**|
|:--|--|
|\\C|当前连接的标识符|
|\\c|一个计数器，您每发出一条语句，计数器就递增一次|
|\\D|完整的当前日期|
|\\d|默认数据库|
|\\h|服务器主机|
|\\l|当前分隔符|
|\\m|当前时间的分钟数|
|\\n|换行符|
|\\O|以三个字母格式表示的当前月份（Jan, Feb, …）|
|\\o|数字格式的当前月份|
|\\P|am/pm|
|\\p|当前 TCP/IP 端口或套接字文件|
|\\R|当前时间，24 小时军用时间（0-23）。|
|\\r|当前时间，标准 12 小时制时间 (1-12)|
|\\S|分号|
|\\s|当前时间的秒数|
|\\T|如果当前会话位于事务块内，则打印星号 (*)（来自 MySQL 8.0.28）|
|\\t|制表符|
|\\U|您的 *user_name@host_name* 完整账户名|
|\\u|您的用户名|
|\\v|服务器版本|
|\\w|用三个字母表示的当前星期（Mon, Tue, …）|
|\\Y|当前年，四位数|
|\\y|当前年，两位数|
|\\_|空格|
|\\ |空格（反斜杠后的空格）|
|\\'|单引号|
|\\"|双引号|
|\\\\ |一个字面的反斜杠字符|
|\\**x**|**x**，针对上面未列出的任何 "**x**"|

您可以通过多种方式设置提示：

- ***Use an environment variable***。可以将 `MYSQL_PS1` 环境变量设置为提示字符串。例如：

    ```terminal
    export MYSQL_PS1="(\u@\h) [\d]> "
    ```

- ***Use a command-line option***。你可以将命令行上的`--prompt`选项设置为 "**mysql**"。例如：

    ```terminal
    $> mysql --prompt="(\u@\h) [\d]> "
    (user@host) [database]>
    ```

- ***Use an option file***。你可以在任何 MySQL 选项文件的`[mysql]`组中设置`prompt`选项，例如*/etc/my.cnf*或你主目录中的*.my.cnf*文件。例如：

    ```ini
    [mysql]
    prompt=(\\u@\\h) [\\d]>\\_
    ```

    在本例中，请注意反斜线是加倍的。如果使用选项文件中的提示选项设置`prompt`，建议在使用特殊提示选项时将反斜线加倍。允许使用的提示选项集与选项文件中可识别的特殊转义序列集有一些重叠。（选项文件中的转义序列规则见["Using Option Files"](https://dev.mysql.com/doc/refman/8.0/en/option-files.html)）。如果使用单反斜线，重叠可能会造成问题。例如，`\s` 会被解释为空格，而不是当前的秒值。下面的示例展示了如何在选项文件中定义提示符，以 ***hh:mm:ss>*** 格式包含当前时间：

    ```ini
    [mysql]
    prompt="\\r:\\m:\\s> "
    ```

- ***Set the prompt interactively***。可以使用 `prompt`（或 `\R`）命令交互式更改提示符。例如

    ```sql
    mysql> prompt (\u@\h) [\d]>\_
    PROMPT set to '(\u@\h) [\d]>\_'
    (user@host) [database]>
    (user@host) [database]> prompt
    Returning to default PROMPT of mysql>
    mysql>
    ```

## mysql 客户端日志

**mysql** 客户端可以为交互式执行的语句记录这些类型的日志：

- 在 Unix 上，**mysql** 会将语句写入历史文件。默认情况下，该文件名为`.mysql_history`，位于你的主目录中。要指定不同的文件，请设置 `MYSQL_HISTFILE`环境变量的值。

- 在所有平台上，如果给出 `--syslog` 选项，**mysql** 会将语句写入系统日志设施。在 Unix 上，这是 `syslog;` 在 Windows 上，这是 Windows 事件日志。记录信息的目的地取决于系统。在 Linux 上，目的地通常是 */var/log/messages* 文件。

以下讨论介绍了适用于所有记录类型的特征，并提供了每种记录类型的特定信息。

- [如何记录日志](https://javenjin.github.io/blog/zh-cn/p/mysql-%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%AE%A2%E6%88%B7%E7%AB%AF/#%E5%A6%82%E4%BD%95%E8%AE%B0%E5%BD%95%E6%97%A5%E5%BF%97)

- [控制历史文件](https://javenjin.github.io/blog/zh-cn/p/mysql-%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%AE%A2%E6%88%B7%E7%AB%AF/#%E6%8E%A7%E5%88%B6%E5%8E%86%E5%8F%B2%E6%96%87%E4%BB%B6)

- [syslog 日志特征](https://javenjin.github.io/blog/zh-cn/p/mysql-%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%AE%A2%E6%88%B7%E7%AB%AF/#syslog-%E6%97%A5%E5%BF%97%E7%89%B9%E5%BE%81)

### 如何记录日志

对于每个已启用的日志记录目标，语句记录发生的情况如下：

- 语句只有在交互执行时才会被记录。例如，从文件或管道读取语句时，语句是非交互式的。也可以使用 `--batch` 或 `--execute` 选项来抑制语句记录。

- 如果语句与 "ignore" 列表中的任何模式匹配，就会被忽略，也不会被记录。稍后将对该列表进行说明。

- **mysql** 会单独记录每一行未忽略、非空的语句。

- 如果一条未忽略的语句跨越多行（不包括终止分隔符），**mysql** 会将这些行连接起来形成完整的语句，将换行符映射为空格，并记录结果和分隔符。

因此，跨越多行的输入语句可能会被记录两次。请看下面的输入

```sql
mysql> SELECT
    -> 'Today is'
    -> ,
    -> CURDATE()
    -> ;
```

在这种情况下，**mysql** 会在读取时记录 "SELECT"、"'Today is'"、","、"CURDATE() "和";"行。在将 `SELECT\n'Today is'\n,\nCURDATE()` 映射为 `SELECT 'Today is' , CURDATE()` 后，它还会记录完整的语句，并加上分隔符。因此，这些行将出现在日志输出中：

```sql
SELECT
'Today is'
,
CURDATE()
;
SELECT 'Today is' , CURDATE();
```

为了记录日志，**mysql** 会忽略与 "ignore" 列表中任何模式匹配的语句。默认情况下，模式列表为 `"*IDENTIFIED*:*PASSWORD*"`，以忽略涉及密码的语句。模式匹配不区分大小写。在模式中，有两个字符是特殊字符：

- **?** 匹配任何单个字符。

- **\*** 匹配任何由 0 个或多个字符组成的序列。

要指定其他模式，请使用 `--histignore` 选项或设置 `MYSQL_HISTIGNORE` 环境变量。（如果同时指定了这两个选项，则以选项值为准。）值应该是一个或多个以冒号分隔的模式列表，这些模式会被追加到默认模式列表中。

命令行中指定的模式可能需要加引号或转义，以防止命令解释器对其进行特殊处理。例如，要禁止记录 `UPDATE` 和 `DELETE` 语句以及引用密码的语句，可以这样调用 **mysql**：

```terminal
mysql --histignore="*UPDATE*:*DELETE*"
```

### 控制历史文件

应使用限制访问模式保护 `.mysql_history` 文件，因为敏感信息（如包含密码的 SQL 语句文本）可能会被写入该文件。请参阅["End-User Guidelines for Password Security"](https://dev.mysql.com/doc/refman/8.0/en/password-security-user.html)。使用**up-arrow**键调用历史记录时，可从**mysql**客户端访问文件中的语句。请参阅 [Disabling Interactive History](https://javenjin.github.io/blog/zh-cn/p/mysql-%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%AE%A2%E6%88%B7%E7%AB%AF/#%E7%A6%81%E7%94%A8%E4%BA%A4%E4%BA%92%E5%BC%8F%E5%8E%86%E5%8F%B2%E8%AE%B0%E5%BD%95)。

如果不想维护历史文件，首先删除存在的 `.mysql_history`。然后使用以下任一技术防止再次创建该文件：

- 将 `MYSQL_HISTFILE` 环境变量设置为 `/dev/null`。要使该设置在每次登录时生效，请将其放在 shell 的某个启动文件中。

- 将 `.mysql_history` 创建为指向 `/dev/null`的符号链接；只需创建一次：

```terminal
ln -s /dev/null $HOME/.mysql_history
```

### syslog 日志特征

如果给定了 `--syslog` 选项，**mysql** 会将交互式语句写入系统日志设施。消息日志具有以下特点。

日志记录发生在 "information" 级别。这相当于 Unix/Linux `syslog` 功能中 `syslog` 的 `LOG_INFO` 优先级，以及 Windows 事件日志的 `EVENTLOG_INFORMATION_TYPE` 优先级。有关日志功能的配置，请查阅系统文档。

信息大小限制为 1024 字节。

信息由标识符 `MysqlClient` 和这些值组成：

- `SYSTEM_USER`

    操作系统用户名（登录名），如果用户未知，则使用 \-\- 表示。

- `MYSQL_USER`

    MySQL 用户名（使用 `--user` 选项指定），如果用户未知，则使用 \-\-。

- `CONNECTION_ID:`

    客户端连接标识符。它与会话中的 `CONNECTION_ID()` 函数值相同。

- `DB_SERVER`

    服务器主机，如果主机未知，则为\-\-。

- `DB`

    默认数据库，如果没有选择数据库，则使用 \-\-。

- `QUERY`

    记录的声明文本。

下面是使用 `--syslog` 在 Linux 上生成的输出示例。为便于阅读，该输出已格式化；每条记录的信息实际上只占一行。

```
Mar  7 12:39:25 myhost MysqlClient[20824]:
  SYSTEM_USER:'oscar', MYSQL_USER:'my_oscar', CONNECTION_ID:23,
  DB_SERVER:'127.0.0.1', DB:'--', QUERY:'USE test;'
Mar  7 12:39:28 myhost MysqlClient[20824]:
  SYSTEM_USER:'oscar', MYSQL_USER:'my_oscar', CONNECTION_ID:23,
  DB_SERVER:'127.0.0.1', DB:'test', QUERY:'SHOW TABLES;'
```

## mysql 客户端服务器端帮助

```
mysql> help search_string
```

如果为 `help` 命令提供一个参数，**mysql**会将其作为搜索字符串，从《MySQL参考手册》的内容中访问服务器端帮助。该命令的正确操作要求**mysql**数据库中的帮助表用帮助主题信息初始化（参见["Server-Side Help Support"](https://dev.mysql.com/doc/refman/8.0/en/server-side-help-support.html)）。

如果搜索字符串没有匹配项，则搜索失败：

```
mysql> help me

Nothing found
Please try to run 'help contents' for a list of all accessible topics
```

使用 [help contents](https://dev.mysql.com/doc/refman/8.0/en/help.html) 查看帮助类别列表：

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

如果搜索字符串匹配多个项目，**mysql** 会显示匹配主题的列表：

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

使用主题作为搜索字符串，可查看该主题的帮助条目：

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

搜索字符串可以包含通配符 `%` 和 `_`。这些字符的含义与使用 `LIKE` 操作符执行的模式匹配操作相同。例如，`HELP rep%` 返回以`rep`开头的主题列表：

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

## 从文本文件执行 SQL 语句

**mysql** 客户端通常是交互式使用的，就像这样：

```terminal
mysql db_name
```

不过，也可以将 SQL 语句放在一个文件中，然后告诉 **mysql** 从该文件读取输入。为此，请创建一个文本文件 `text_file`，其中包含要执行的语句。然后调用 **mysql**，如下所示：

```terminal
mysql db_name < text_file
```

如果将 `USE db_name` 语句作为文件中的第一条语句，则无需在命令行中指定数据库名称：

```terminal
mysql < text_file
```

如果已在运行 **mysql**，则可以使用 `source` 命令或 `\.` 命令执行 SQL 脚本文件：

```sql
mysql> source file_name
mysql> \. file_name
```

有时，您可能希望脚本向用户显示进度信息。为此，您可以插入如下语句

```sql
SELECT '<info_to_display>' AS ' ';
```

所示语句输出`<info_to_display>`。

你也可以在调用 **mysql** 时使用 `--verbose` 选项，这将导致在显示每条语句产生的结果之前显示其结果。

**mysql** 忽略输入文件开头的 Unicode 字节序号 (BOM) 字符。以前，它会读取这些字符并将其发送到服务器，从而导致语法错误。BOM 字符的存在不会导致 **mysql** 更改默认字符集。要做到这一点，请在调用 **mysql** 时加入一个选项，如 `--default-character-set=utf8mb4`。

有关批处理模式的更多信息，请参阅章节["Using mysql in Batch Mode"](https://dev.mysql.com/doc/refman/8.0/en/batch-mode.html)。

## mysql 客户端提示

本节介绍更有效使用 **mysql** 的技巧以及 **mysql** 的操作行为。

- [输入行编辑](https://javenjin.github.io/blog/zh-cn/p/mysql-%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%AE%A2%E6%88%B7%E7%AB%AF/#%E8%BE%93%E5%85%A5%E8%A1%8C%E7%BC%96%E8%BE%91)

- [禁用交互式历史记录](https://javenjin.github.io/blog/zh-cn/p/mysql-%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%AE%A2%E6%88%B7%E7%AB%AF/#%E7%A6%81%E7%94%A8%E4%BA%A4%E4%BA%92%E5%BC%8F%E5%8E%86%E5%8F%B2%E8%AE%B0%E5%BD%95)

- [Windows 支持 Unicode](https://javenjin.github.io/blog/zh-cn/p/mysql-%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%AE%A2%E6%88%B7%E7%AB%AF/#windows-%E6%94%AF%E6%8C%81-unicode)

- [垂直显示查询结果](https://javenjin.github.io/blog/zh-cn/p/mysql-%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%AE%A2%E6%88%B7%E7%AB%AF/#%E5%9E%82%E7%9B%B4%E6%98%BE%E7%A4%BA%E6%9F%A5%E8%AF%A2%E7%BB%93%E6%9E%9C)

- [使用安全更新模式 (--safe-updates)](https://javenjin.github.io/blog/zh-cn/p/mysql-%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%AE%A2%E6%88%B7%E7%AB%AF/#%E4%BD%BF%E7%94%A8%E5%AE%89%E5%85%A8%E6%9B%B4%E6%96%B0%E6%A8%A1%E5%BC%8F---safe-updates)

- [禁用 mysql 自动重新连接功能](https://javenjin.github.io/blog/zh-cn/p/mysql-%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%AE%A2%E6%88%B7%E7%AB%AF/#%E7%A6%81%E7%94%A8-mysql-%E8%87%AA%E5%8A%A8%E9%87%8D%E6%96%B0%E8%BF%9E%E6%8E%A5%E5%8A%9F%E8%83%BD)

- [mysql 客户端解析器与服务器解析器对比](https://javenjin.github.io/blog/zh-cn/p/mysql-%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%AE%A2%E6%88%B7%E7%AB%AF/#mysql-%E5%AE%A2%E6%88%B7%E7%AB%AF%E8%A7%A3%E6%9E%90%E5%99%A8%E4%B8%8E%E6%9C%8D%E5%8A%A1%E5%99%A8%E8%A7%A3%E6%9E%90%E5%99%A8%E5%AF%B9%E6%AF%94)

### 输入行编辑

**mysql**支持输入行编辑，这使你可以就地修改当前输入行或调用以前的输入行。例如，`left-arrow` 和 `right-arrow` 键可在当前输入行内水平移动，`up-arrow` 和 `down-arrow` 键可在以前输入的行中上下移动。`Backspace` 删除光标前的字符，输入新字符时则在光标位置输入。要输入一行，按 `Enter`。

在 Windows 上，编辑键序与控制台窗口中的命令编辑所支持的键序相同。在 Unix 上，键序取决于用于构建 **mysql** 的输入库（例如，`libedit` 或 `readline` 库）。

`libedit` 或 `readline` 库的文档可在线获取。要更改特定输入库允许的键序列集，请在库启动文件中定义键绑定。这是一个位于你的主目录下的文件：`libedit` 为 `.editrc`，`readline` 为 `.inputrc`。

例如，在 `libedit` 中，`Control+W` 删除当前光标位置前的所有内容，`Control+U` 删除整行。在 `readline` 中，`Control+W` 删除光标前的单词，`Control+U` 删除当前光标位置前的所有内容。如果**mysql**是使用`libedit`创建的，那么如果用户喜欢这两个键的`readline`行为，可以在`.editrc`文件中加入以下几行（必要时创建文件）：

```terminal
bind "^W" ed-delete-prev-word
bind "^U" vi-kill-line-prev
```

要查看当前的按键绑定集，可暂时在 `.editrc.` **mysql**启动时显示绑定。

### 禁用交互式历史记录

`up-arrow`可以调用当前和以前会话中的输入行。在共享控制台的情况下，这种行为可能不合适。根据主机平台的不同，**mysql** 支持部分或完全禁用交互式历史记录。

在 Windows 中，历史记录存储在内存中。`Alt+F7`会删除当前历史记录缓冲区内存中存储的所有输入行。它还会删除用 `F7`显示并用 `F9`调用（按编号）的输入行前面的顺序编号列表。按 `Alt+F7` 键后输入的新输入行将重新填充当前历史记录缓冲区。如果在启动 **mysql** 时使用了 `--syslog` 选项，则清除缓冲区并不会阻止向 Windows 事件查看器记录日志。关闭控制台窗口也会清除当前的历史记录缓冲区。

要在 Unix 上禁用交互式历史记录，首先要删除 `.mysql_history` 文件（如果存在）（否则会调用以前的条目）。然后使用 `--histignore="*"`选项启动**mysql**，以忽略所有新输入行。要重新启用调用（和记录）行为，请在重启 **mysql** 时不带该选项。

如果阻止创建`.mysql_history`文件（请查阅[Controlling the History File](https://javenjin.github.io/blog/zh-cn/p/mysql-%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%AE%A2%E6%88%B7%E7%AB%AF/#%E6%8E%A7%E5%88%B6%E5%8E%86%E5%8F%B2%E6%96%87%E4%BB%B6)），并使用`--histignore="*"`来启动**mysql**客户端，交互式历史记录调用功能就会被完全禁用。另外，如果省略`--histignore`选项，则可以调用当前会话中输入的行。

### Windows 支持 Unicode

Windows 提供了基于 UTF-16LE 的 API，用于从控制台读取数据和向控制台写入数据；Windows 的 **mysql** 客户端可以使用这些 API。Windows 安装程序会在 MySQL 菜单中创建一个名为 "MySQL command line client - Unicode" 的项目。此项目调用**mysql**客户端，其属性设置为使用Unicode通过控制台与MySQL服务器通信。

要手动利用这一支持，请在使用兼容 Unicode 字体的控制台中运行 **mysql**，并将默认字符集设置为与服务器通信时支持的 Unicode 字符集：

1. 打开控制台窗口。

2. 进入控制台窗口属性，选择字体选项卡，选择 Lucida Console 或其他兼容的 Unicode 字体。这是必要的，因为控制台窗口启动时默认使用的 DOS 栅格字体不适合 Unicode。

3. 执行 **mysql.exe**，并设置 `--default-character-set=utf8mb4` （或 `utf8mb3`）选项。该选项是必要的，因为 `utf16le` 是不能用作客户端字符集的字符集之一。请参阅 [Impermissible Client Character Sets](https://dev.mysql.com/doc/refman/8.0/en/charset-connection.html#charset-connection-impermissible-client-charset)。

作出这些更改后，**mysql** 将使用 Windows API，使用 UTF-16LE 与控制台通信，并使用 UTF-8 与服务器通信。（前面提到的菜单项可以设置字体和字符集）。

为了避免每次运行**mysql**时都要进行这些步骤，可以创建一个调用**mysql.exe**的快捷方式。快捷方式应将控制台字体设置为 Lucida Console 或其他兼容的 Unicode 字体，并将 `--default-character-set=utf8mb4`（或 `utf8mb3`）选项传递给 **mysql.exe**。

或者，创建一个只设置控制台字体的快捷方式，并在`my.ini`文件的`[mysql]`组中设置字符集：

```ini
[mysql]
default-character-set=utf8mb4   # or utf8mb3
```

### 垂直显示查询结果

有些查询结果如果以垂直方式显示，而不是通常的水平表格格式，会更易读。可以用 \\G 代替分号来结束查询，从而垂直显示查询结果。例如，包含换行符的较长文本值通常在垂直输出时更容易阅读：

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

### 使用安全更新模式 (--safe-updates)

对于初学者来说，一个有用的启动选项是 `-safe-updates`（或 `--i-am-a-dummy`，效果相同）。安全更新模式对以下情况很有帮助：你可能已经发出了一条 `UPDATE` 或 `DELETE` 语句，但却忘记了指示要修改哪些行的 `WHERE` 子句。通常，此类语句会更新或删除表中的所有行。有了 `-safe-updates`，你就只能通过指定标识行的键值或 `LIMIT` 子句或两者来修改行。这有助于防止意外发生。安全更新模式还限制会产生（或估计会产生）非常大结果集的 `SELECT` 语句。

`--safe-updates`选项会导致**mysql**在连接到MySQL服务器时执行以下语句，以设置`sql_safe_updates`、`sql_select_limit`和`max_join_size`系统变量的会话值：

```sql
SET sql_safe_updates=1, sql_select_limit=1000, max_join_size=1000000;
```

`SET`语句对语句处理的影响如下：

- 启用 `sql_safe_updates` 后，如果 `UPDATE` 和 `DELETE` 语句没有在 WHERE 子句中指定键约束，或没有提供 `LIMIT` 子句，或两者都没有，就会产生错误。例如：

    ```sql
    UPDATE tbl_name SET not_key_column=val WHERE key_column=val;

    UPDATE tbl_name SET not_key_column=val LIMIT 1;
    ```

- 将 `sql_select_limit` 设置为 1,000 会导致服务器将所有 `SELECT` 结果集限制为 1,000 行，除非语句包含一个 `LIMIT` 子句。

- 将 `max_join_size` 设置为 1,000,000 会导致多表 `SELECT` 语句在服务器估计必须检查超过 1,000,000 行组合时产生错误。

要指定不同于 1,000 和 1,000,000 的结果集限制，可以在调用 **mysql** 时使用 `--select-limit` 和 `-ax-join-size` 选项来覆盖默认值：

```terminal
mysql --safe-updates --select-limit=500 --max-join-size=10000
```

如果优化器决定不使用键列上的索引，那么即使在 `WHERE` 子句中指定了键，`UPDATE` 和 `DELETE` 语句也有可能在安全更新模式下产生错误：

- 如果内存使用量超过 `range_optimizer_max_mem_size` 系统变量允许的范围，则无法使用索引上的范围访问。这时，优化器会退回到表扫描。请参阅 [Limiting Memory Use for Range Optimization](https://dev.mysql.com/doc/refman/8.0/en/range-optimization.html#range-optimization-memory-use)。

- 如果键比较需要类型转换，则可能无法使用索引（请参阅["How MySQL Uses Indexes"](https://dev.mysql.com/doc/refman/8.0/en/mysql-indexes.html)）。假设使用 `WHERE c1 = 2222` 将索引字符串列 `c1` 与数值进行比较。对于此类比较，字符串值将转换为数字，操作数将以数字形式进行比较（请参阅["Type Conversion in Expression Evaluation"](https://dev.mysql.com/doc/refman/8.0/en/type-conversion.html)），从而无法使用索引。如果启用了安全更新模式，则会出现错误。

从 MySQL 8.0.13 起，安全更新模式也包含这些行为：

- 带有 `UPDATE` 和 `DELETE` 语句的 `EXPLAIN` 不会产生安全更新错误。这样就可以使用 `EXPLAIN` 加上 `SHOW WARNINGS` 来查看不使用索引的原因，这在某些情况下很有帮助，例如当发生 `range_optimizer_max_mem_size` 违规或类型转换时，即使在 `WHERE` 子句中指定了键列，优化器也不会使用索引。

- 当发生安全更新错误时，错误消息会包含产生的第一个诊断，以提供有关失败原因的信息。例如，消息可能显示超出了 `range_optimizer_max_mem_size` 值或发生了类型转换，这两种情况都可能导致无法使用索引。

- 对于多表删除和更新，只有当任何目标表使用表扫描时，才会在启用安全更新后产生错误。

### 禁用 mysql 自动重新连接功能


如果**mysql**客户端在发送语句时与服务器失去连接，它会立即自动尝试重新连接服务器并再次发送语句。不过，即使**mysql**重新连接成功，第一次连接也已结束，所有以前的会话对象和设置都会丢失：临时表、自动提交模式、用户定义变量和会话变量。此外，任何当前事务都会回滚。这种行为可能会给您带来危险，例如在下面的示例中，服务器在您不知道的情况下在第一条和第二条语句之间被关闭并重新启动：

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

@a 用户变量随连接丢失，重新连接后未定义。如果需要在连接丢失时让**mysql**以错误方式终止，可以使用`--skip-reconnect`选项启动**mysql**客户端。

有关自动重新连接及其在发生重新连接时对状态信息影响的更多信息，请参阅 [Automatic Reconnection Control](https://dev.mysql.com/doc/c-api/8.0/en/c-api-auto-reconnect.html)。

### mysql 客户端解析器与服务器解析器对比

**mysql**客户端在客户端使用的解析器与**mysqld**服务器在服务器端使用的完整解析器并不相同。这可能会导致某些构造的处理方式不同。例如：

- 如果启用了 `ANSI_QUOTES` SQL 模式，服务器解析器会将以"字符分隔的字符串视为标识符，而不是纯字符串。

    **mysql** 客户端解析器不考虑 `ANSI_QUOTES` SQL 模式。无论是否启用了 `ANSI_QUOTES`，它对以"、'和\`字符分隔的字符串的处理方式都是一样的。

- Within \/\*\! ... \*\/ 和 \/\*\+ ... \*\/注释中，**mysql**客户端解析器解释简短的**mysql**命令。服务器解析器不会解释它们，因为这些命令在服务器端没有任何意义。

    如果希望**mysql**不解释注释中的短格式命令，部分变通方法是使用 `--binary-mode` 选项，该选项会导致所有**mysql**命令被禁用，但非交互模式下的 `\C` 和 `\d` 除外（对于通过管道输入到**mysql**或使用 `source` 命令加载的输入）。