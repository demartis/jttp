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
