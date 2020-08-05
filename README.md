# JTTP - Json coherent output format for HTTP

JTTP is a coherent and intelligible json format to wrap RESTful json responses.
JTTP covers creating and updating resources as well, not just responses.

JTTP is compatible with HATEOAS, RFC5988 and HAL standards.

## General JTTP output format:

```json
{
    "status": "success|error",
    "code": "HTTP status code",
    "message": "HTTP status message",
    "data|error": {
        "your data": "data or error field only in case of success or error"
    }
}
```

## JTTP for success - HTTP status codes 1xx, 2xx, 3xx
```json
{
    "status": "success",
    "code": "HTTP status code (1xx, 2xx, 3xx)",
    "message": "HTTP status message",
    "data": {
      "your data": "content"
    }
}
```

## JTTP for error - HTTP status codes 4xx, 5xx
```json
{
    "status": "error",
    "code": "HTTP status code (4xx, 5xx)",
    "message": "HTTP status message",
    "error": {
      "your error": "error content"
    }
}
```

--------

## Examples

#### GET /books
```json
{
    "status": "success",
    "code": 200,
    "message": "OK",
    "data": [
        {
            "id": 1,
            "title": "JTTP is awesome",
            "pages": 1000
        },
        {
            "id": 2,
            "title": "RESTful services",
            "pages": 1200
        }
    ]
}
```

#### GET /books/1
```json
{
    "status": "success",
    "code": 200,
    "message": "OK",
    "data": {
        "id": 1,
        "title": "JTTP is awesome",
        "pages": 1000
    }
}
```

#### POST /books with payload:
```json
{
    "data": {
        "title": "JTTP is awesome",
        "pages": 1000
    }
}
```
JTTP Response:
```json
{
    "status": "success",
    "code": 201,
    "message": "OK",
    "data": [
        {
            "id": 1,
            "title": "JTTP is awesome",
            "pages": 1000
        }
    ]
}
```

#### Example - error: Resource not found: GET /books/123123
```json
{
    "status": "error",
    "code": 404,
    "message": "Not Found",
    "error": {
        "details": "Resource 123123 not found"
    }
}
```

#### Example - 500 Internal Server Error
(your server should avoid these errors!)
```json
{
    "status": "error",
    "code": 500,
    "message": "Internal Server Error",
    "error": {
        "details": "Notice: Undefined variable: unknown_var"
    }
}
```

## HATEOAS + HAL implementation
Even if HAL is [currently in draft status](https://tools.ietf.org/html/draft-kelly-json-hal-08), we have implemented it by following its latest definition.
Here's below an example
#### GET /books
```json
{
    "status": "success",
    "code": 200,
    "message": "OK",
    "data": [
        {
            "id": 1,
            "title": "JTTP is awesome",
            "pages": 1000,
            "_links": {
                "self": {
                    "href": "/books/1"
                },
                "next": {
                    "href": "/books/2"
                }
            },
            "_embedded": {
                "author": {
                    "id": 1,
                    "name": "Riccardo De Martis",
                    "_links": {
                        "self": {
                            "href": "/authors/1"
                        }                   
                    }
                }
            }
        },
        {
            "id": 2,
            "title": "RESTful services",
            "pages": 1200,
            "_links": {
                "self": {
                    "href": "/books/2"
                },
                "prev": {
                    "href": "/books/1"
                }
            },
            "_embedded": {
                "author": {
                    "id": 2,
                    "name": "Someone",
                    "_links": {
                        "self": {
                            "href": "/authors/2"
                        }                   
                    }
                }
            }
        }
    ]
}
```
