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
