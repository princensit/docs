# Error Code Handling

Gist:
Use three simple, common response codes indicating 
1. success
2. failure due to client-side problem
3. failure due to server-side problem

Start with 3 HTTP status codes: 200, 400 and 500. If there is any requirement of authorization in API, then use 401 HTTP status code. 4 status code should be sufficient and if needed more, then go max to 8 HTTP status codes.

200 - OK
400 - Bad Request (Client Error) - A json with error details should return to the client
401 - Unauthorized
500 - Internal Server Error - A json with an error should return to the client only when there is no security risk by doing that.

Use error code and error message in Response wrapper class so that it becomes easy for developer to debug.

```
@Data
public final class Response<T> {
   private final T response;
   private final Error error;
}

@Data
public final class Error {
   private final Integer code;
   private final String message;
}
```

Reference:  https://blog.restcase.com/rest-api-error-codes-101/
