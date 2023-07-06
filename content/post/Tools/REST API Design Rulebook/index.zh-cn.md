---
title: REST API Design Rulebook
description: REST API Design Rulebook
date: '2022-06-21'
categories:
    - Tools
tags:
    - Tools
---

# REST API Design Rulebook

## URI Format(RFC 3986)

```
URL = scheme "://" authority "/" path [ "?" query ] [ "#" fragment ]
```

## URI Rules

1. 必须使用正斜杠分隔符（/）来表示层次结构关系

   ```
   http://api.canvas.restapi.org/shapes/polygons/quadrilaterals/squares
   ```

2. URI最后不应该有斜杠（/）

   ```
   Incorrect:	http://api.canvas.restapi.org/shapes/
   Correct:	http://api.canvas.restapi.org/shapes
   ```

3. 应该使用连字符（-）来提高URI可读性

   ```
   http://api.example.restapi.org/blogs/mark-masse/entries/this-is-my-first-post
   ```

4. URI中不应该使用下划线（_）

5. 在URI路径中，应该首选小写字母

   ```
   1: http://api.example.restapi.org/my-folder/my-doc	Correct
   2: HTTP://API.EXAMPLE.RESTAPI.ORG/my-fplder/my-doc	Correct
   3: httpL//api.example.restapi.org/My-Folder/my-doc	Incorrect
   ```

6. 文件扩展名不应该包含在URI中

   ```
   Incorrect:	http://api.college.restapi.org/students/3248234/transcripts/2005/fall.json
   Correct:	http://api.college.restapi.org/students/3248234/transcripts/2005/fall
   ```

7. 对于API，应该使用一致的子域名，API的完整域名应该添加一个名为api的子域

   ```
   Incorrect:	http://soccer.restapi.org
   Correct:	http://api.soccer.restapi.org
   ```

8. 对于客户端开发人员，应该使用一致的子域名

   ```
   httpL//developer.soccer.restapi.org
   ```

9. 表示文档资源的URI应该用单数名词

   ```
   http://api.soccer.restapi.org/leagues/seattle/teams/trebuchet/players/claudio
   ```

10. 标识一个集合的URI应该用一个复数名词

    ```
    http://api.soccer.restapi.org/leagues/seattle/teams/trebuchet/players
    ```

11. 标识资源存储的URI应该用复数名词

    ```
    http://api.music.restapi.org/artists/mikemassedotcom/playlists
    ```

12. 动词或动词短语应用于控制器名称

    ```
    http://api.college.restapi.org/students/morgan/register
    http://api.example.restapi.org/lists/4324/dedupe
    http://api.ognom.restapi.org/dbs/reindex
    http://api.build.restapi.org/qa/nightly/runTestSuite
    ```

13. 变量路径段可以用于基于标识的值进行替换

    ```
    http://api.soccer.restapi.org/leagues/{leagueId}/teams/{teamsId}/players/{playerId}
    http://api.soccer.restapi.org/leagues/seattle/teams/trebuchet/players/21
    ```

14. CRUD函数名称不应该使用在URI中

    ```
    Incorrect:
    	GET /deleteUser?id=1234
    	GET /deleteUsers/1234
    	DELETE /deleteUser/1234
    	POST /users/1234/delete
    Correct:
    	DELETE /users/1234
    ```

15. 一个URI的查询组件可以用于过滤集合或存储

    ```
    GET /users
    GET /users?role=admin
    ```

16. URI的查询组件应该用于分页收集或存储结果

    ```
    GET /users?pageSize=25&&pageStartIndex=50
    ```

## Request Methods(RFC2616)

```
Request-Line = Method SP Request-URI SP HTTP-Version CRLF
```

**GET** is to retrieve a representation of a resource's state.

**HEAD** is used to retrieve the metadata associated with the resource's state.

**PUT** should be used to add a new resource to a store or update a resource.

**DELETE** removes a resource from its parent.

**POST** should be used to create a new resource within a collection and execute controllers.

## Request Method Rules

1. GET和POST不能用于其他请求方法

2. 必须使用GET来检索资源的表达形式

   ```shell
   $ curl -v http://api.example.restapi.org/greeting
   
   > GET /greeting HTTP/1.1
   > User-Agent: curl/7.20.1
   > Host: api.example.restapi.org
   > Accept: *.*
   
   < HTTP/1.1 200 OK
   < Date: Sat, 20 Aug 2011 16:02:40 GMT
   < Server: Apache
   < Expires: Sat, 20 Aug 2011 16:06:40 GMT
   < Cache-Control: max-age=60, must-revalidate
   < ETag: text/html:hello world
   < Last-Modified: Sat, 20 Aug 2011 16:02:17 GMT
   < Vary: Accept-Encoding
   < Content-Type: text/html
   
   <!doctype html><head><meta charset="utf-8"><title>Greeting</title></head>
   <body><div id="greeting">Hello World!</div></body></html>
   ```

3. HEAD应用于检索响应报头

   ```shell
   $curl --head http://api.example.restapi.org/greeting
   
   HTTP/1.1 200 OK
   Date: Sat, 20 Aug 2011 16:02:40 GMT
   Server: Apache
   Expires: Sat, 20 Aug 2011 16:03:40 GMT
   Cache-Control: max-age=60, must-revalidate
   ETag: text/html:hello world
   Last-Modified: Sat, 20 Aug 2011 16:02:17 GMT
   Vary: Accept-Encoding
   Context-Type: text/html
   ```

4. 必须使用PUT来插入和更新所存储的资源

   ```
   PUT /accounts/4ef2d5d0-cb7e-11e0-9572-0800200c9a66/buckets/objects/4321
   ```

5. 必须使用PUT来更新可变的资源

6. 必须使用POST在一个集合中创建一个新的资源

   ```shell
   POST /leagues/seattle/teams/trebuchet/players
   
   # Note the request message may contain a representation that suggests the initial state of the player to be created.
   ```

7. 必须使用POST来执行控制器

   ```
   POST /alerts/245743/resend
   ```

8. 必须使用DELETE来删除资源

   ```
   DELETE /accounts/4ef2d5d0-cb7e-11e0-9572-080020c9a66/buckets/objects/4321
   ```

9. OPTIONS应该使用来检索描述资源可用交互的元数据

## Response Status Codes

| Category           | Description                                                  |
| ------------------ | ------------------------------------------------------------ |
| 1xx: Informational | Communicates transfer protocol-level information.            |
| 2xx: Success       | Indicates that the client's request was accepted successfully. |
| 3xx: Redirection   | Indicates that the client must take some additional action in order to complete their request. |
| 4xx: Client Error  | This category of error status codes points the finger at clients. |
| 5xx: Server Error  | The server takes responsibility for these error status codes |

## Response Status  Code Rules

1. 200 OK 表示非特定成功
2. 200 OK 不能用于通信相应主体中的错误
3. 201 Created 表示资源创建成功
4. 202 Accepted 必须用于指示已成功启动异步操作
5. 204 No Content 相应主体故意空时，使用204
6. 301 Moved Permanently 用来重新定位资源
7. 302 Found 不应该使用该规则
8. 303 See Other 应用于将客户端引用到不同的URI
9. 304 Not Modified 应用来保留带宽
10. 307 Temporary Redirect 告诉客户将请求重新提交到另一个URI
11. 400 Bad Request 表示非特定失败
12. 401 Unauthorized 当客户端的凭据出现问题，必须使用401
13. 403 Forbidden 用户访问资源超出权限，禁止访问
14. 404 Not Found 当URI无法映射到资源时，必须使用404
15. 405 Method Not Allowed 当HTTP方法不受支持时，必须使用405
16. 406 Not Acceptable 当无法提供请求的文件类型时，必须使用406
17. 409 Conflict 试图将资源置于不可能或不一致的状态时
18. 412 Precondition Failed 请求头中的先决条件不满足，返回412，并未执行请求
19. 415 Unsupported Media Type 当无法处理客户端请求的文件类型时，必须使用415
20. 500 Internal Server Error 用来指示API故障

## HTTP Headers Rules

1. Content-Type 必须使用
2. Content-Length 应该使用
3. Last-Modified 应该在响应中使用
4. ETag 应该在响应中使用
5. 存储必须支持有条件的PUT请求
6. 必须使用Location来指定新创建的资源的URI
7. 应该使用Cache-Control、Expires和Date请求头来鼓励缓存
8. Cache-Control、Expires和Pragma响应头可以用来阻止缓存
9. Caching should be encouraged
10. Expiration caching缓存头应该与200（OK）响应一起使用
11. Expiration caching缓存头可以选择与3xx和4xx响应一起使用
12. 不能使用自定义HTTP标头来更改HTTP方法的行为

## Media Types

```
type "/" subtype *( ";" parameter )
```

## Registered Media Types

| Registered Media Types | Description                                                  |
| ---------------------- | ------------------------------------------------------------ |
| text/plain             | A plain text format with no specific content structure or markup. |
| text/html              | Content that is formatted using the HyperText Markup Language (HTML). |
| image/jpeg             | An image compression method that was standardized by the Joint Photographic Experts Group (JEPG). |
| application/xml        | Content that is structured using the Extensible Markup Language (XML). |
| application/atom+xml   | Content that uses the Atom Syndication Format (Atom), which is an XML-based format that structures data into lists known as feeds. |
| application/javascript | Source code written in the JavaScript programming language.  |
| application/json       | The JavaScript Object Notation (JSON) text-based format that is often used by programs to exchange structured data. |

## Media Types Rules

1. Application-specific media types should be used
2. Media type negotiation should be supported when multiple representations are available
3. Media type selection using a query parameter may be supported

## Message Body Rules

1. 资源表示应该支持JSON
2. JSON必须是格式良好的
3. XML和其他格式可以选择用于资源表示
4. Additional envelopes must not be created

## Hypermedia Representation Rules

1. A consistent form should be used to represent links
2. A consistent form should be used to represent link relations
3. A consistent form should be used to advertise links
4. A self link should be included in response message body representations
5. Minimize the number of advertised “entry point” API URIs
6. Links should be used to advertise a resource’s available actions in a state-sensitive manner

## Media Type Representation Rules

1. A consistent form should be used to represent media type formats
2. A consistent form should be used to represent media type schemas

## Error Representation Rules

1. A consistent form should be used to represent errors
2. A consistent form should be used to represent error responses
3. Consistent error types should be used for common error conditions

## Client Concerns Rules

1. New URIs should be used to introduce new concepts
2. Schemas should be used to manage representational form versions
3. Entity tags should be used to manage representational state versions
4. OAuth may be used to protect resources
5. API management solutions may be used to protect resources
6. The query component of a URI should be used to support partial responses
7. The query component of a URI should be used to embed linked resources
8. JSONP should be supported to provide multi-origin read access from JavaScript

## Final Thoughts Principles

1. REST API designs differ more than necessary
2. A REST API should be designed, not coded
3. Programmers and their organizations benefit from consistency
4. A REST API should be created using a GUI tool