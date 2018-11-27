# Java Related Docs


# Exception Handling

Why unchecked exceptions?
1. To allow developers fine-grained control over the errors they want to handle without forcing them to handle exceptional cases they aren't concerned about (and making their code overly verbose)
2. To prevent scalability issues inherent with checked exceptions in large applications

In general, checked exceptions work well on small scales, but can become troublesome as applications grow and become more complex.

Two types of unchecked exceptions:
1. ServiceException (and Subclasses)
2. ClientException

## ServiceException (and Subclasses):
This exception represents an error response from your service. For some cases, a subclass is thrown to allow developers fine-grained control over handling error cases through catch blocks.

When you encounter an ServiceException, you know that your request was successfully sent to the service but couldn't be successfully processed. This can be because of errors in the request's parameters or because of issues on the service side.

ServiceException provides you with information such as:
1. Returned HTTP status code
2. Returned error code
3. Detailed error message from the service
4. Request ID for the failed request

## ClientException:
It indicates that a problem occurred inside the Java client code, either while trying to send a request to service or while trying to parse a response from server.

It is generally more severe than ServiceException, in a way that client is prevented for making call to server. For example this exception is thrown when there is no network connection available.

Ex-  
```
public class WalletClientException extends { }
```

Reference: https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-exceptions.html

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
