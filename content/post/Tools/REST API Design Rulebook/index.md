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

1. A forward-slash separator (/) must be used to indicate hierarchical relationships

   ```
   http://api.canvas.restapi.org/shapes/polygons/quadrilaterals/squares
   ```

2. The URI should not have a slash (/) at the end

   ```
   Incorrect:	http://api.canvas.restapi.org/shapes/
   Correct:	http://api.canvas.restapi.org/shapes
   ```

3. Hyphens (-) should be used to improve URI readability

   ```
   http://api.example.restapi.org/blogs/mark-masse/entries/this-is-my-first-post
   ```

4. Underscores (_) should not be used in URIs

5. In the URI path, lowercase letters should be preferred

   ```
   1: http://api.example.restapi.org/my-folder/my-doc	Correct
   2: HTTP://API.EXAMPLE.RESTAPI.ORG/my-fplder/my-doc	Correct
   3: httpL//api.example.restapi.org/My-Folder/my-doc	Incorrect
   ```

6. The file extension should not be included in the URI

   ```
   Incorrect:	http://api.college.restapi.org/students/3248234/transcripts/2005/fall.json
   Correct:	http://api.college.restapi.org/students/3248234/transcripts/2005/fall
   ```

7. For the API, a consistent subdomain should be used, and a subdomain named api should be added to the full domain of the API

   ```
   Incorrect:	http://soccer.restapi.org
   Correct:	http://api.soccer.restapi.org
   ```

8. For client developers, a consistent subdomain should be used

   ```
   httpL//developer.soccer.restapi.org
   ```

9. URIs that represent document resources should use singular nouns

   ```
   http://api.soccer.restapi.org/leagues/seattle/teams/trebuchet/players/claudio
   ```

10. The URI that identifies a collection should use a plural noun

    ```
    http://api.soccer.restapi.org/leagues/seattle/teams/trebuchet/players
    ```

11. The URI identifying the resource store should use a plural noun

    ```
    http://api.music.restapi.org/artists/mikemassedotcom/playlists
    ```

12. Verb or verb phrase applied to controller name

    ```
    http://api.college.restapi.org/students/morgan/register
    http://api.example.restapi.org/lists/4324/dedupe
    http://api.ognom.restapi.org/dbs/reindex
    http://api.build.restapi.org/qa/nightly/runTestSuite
    ```

13. Variable path segments can be used for substitution based on the value of the identifier

    ```
    http://api.soccer.restapi.org/leagues/{leagueId}/teams/{teamsId}/players/{playerId}
    http://api.soccer.restapi.org/leagues/seattle/teams/trebuchet/players/21
    ```

14. CRUD function names should not be used in URIs

    ```
    Incorrect:
    	GET /deleteUser?id=1234
    	GET /deleteUsers/1234
    	DELETE /deleteUser/1234
    	POST /users/1234/delete
    Correct:
    	DELETE /users/1234
    ```

15. A query component of a URI can be used to filter collections or store

    ```
    GET /users
    GET /users?role=admin
    ```

16. The query component of the URI should be used for paging to collect or store results

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

1. GET and POST cannot be used for other request methods

2. Must use GET to retrieve the expression of the resource

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

3. HEAD is applied to retrieve response headers

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

4. PUT must be used to insert and update the stored resources

   ```
   PUT /accounts/4ef2d5d0-cb7e-11e0-9572-0800200c9a66/buckets/objects/4321
   ```

5. PUT must be used to update variable resources

6. Must use POST to create a new resource in a collection

   ```shell
   POST /leagues/seattle/teams/trebuchet/players
   
   # Note the request message may contain a representation that suggests the initial state of the player to be created.
   ```

7. POST must be used to execute the controller

   ```
   POST /alerts/245743/resend
   ```

8. DELETE must be used to delete the resource

   ```
   DELETE /accounts/4ef2d5d0-cb7e-11e0-9572-080020c9a66/buckets/objects/4321
   ```

9. OPTIONS should be used to retrieve metadata describing the interactions available to the resource

## Response Status Codes

| Category           | Description                                                  |
| ------------------ | ------------------------------------------------------------ |
| 1xx: Informational | Communicates transfer protocol-level information.            |
| 2xx: Success       | Indicates that the client's request was accepted successfully. |
| 3xx: Redirection   | Indicates that the client must take some additional action in order to complete their request. |
| 4xx: Client Error  | This category of error status codes points the finger at clients. |
| 5xx: Server Error  | The server takes responsibility for these error status codes |

## Response Status  Code Rules

1. 200 OK (indicates non-specific success)
2. 200 OK (cannot be used to communicate errors in the corresponding body)
3. 201 Created (indicates that the resource was created successfully)
4. 202 Accepted (must be used to indicate that an asynchronous operation has been successfully started)
5. 204 No Content (Use 204 if the corresponding body is intentionally empty)
6. 301 Moved Permanently (used to relocate the resource)
7. 302 Found (this rule should not be used)
8. 303 See Other (applied to refer clients to a different URI)
9. 304 Not Modified (applied to reserve bandwidth)
10. 307 Temporary Redirect (tells the client to resubmit the request to another URI)
11. 400 Bad Request (indicates a non-specific failure)
12. 401 Unauthorized (must be used when there is a problem with the client's credentials)
13. 403 Forbidden (user access to the resource exceeds permissions, access is prohibited)
14. 404 Not Found (404 must be used when the URI cannot be mapped to a resource)
15. 405 Method Not Allowed (when HTTP methods are not supported, 405 must be used)
16. 406 Not Acceptable (406 must be used when the requested file type cannot be provided)
17. 409 Conflict (when attempting to place a resource in an impossible or inconsistent state)
18. 412 Precondition Failed (precondition in request header not met, returned 412 and did not execute request)
19. 415 Unsupported Media Type (415 must be used when the file type requested by the client cannot be handled)
20. 500 Internal Server Error (used to indicate API failure)

## HTTP Headers Rules

1. Content-Type must be used
2. Content-Length should be used
3. Last-Modified should be used in the response
4. ETag should be used in the response
5. Storage must support conditional PUT requests
6. Location must be used to specify the URI of the newly created resource
7. Cache-Control, Expires and Date request headers should be used to encourage caching
8. Cache-Control, Expires, and Pragma response headers can be used to block caching
9. Caching should be encouraged
10. Expiration caching cache headers should be used with the 200 (OK) response
11. Expiration caching cache headers can optionally be used with 3xx and 4xx responses
12. custom HTTP headers cannot be used to change the behavior of HTTP methods

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

1. the resource representation should support JSON
2. JSON must be well-formed
3. XML and other formats are optional for the resource representation
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