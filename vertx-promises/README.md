# Vertx-Promises

## Vertx Specific Functionality

The main addition to the Vertx version of RxJava-Promises is its ability to be used as a Vertx Handler. 

```java
private Promise<Buffer> readAFile(String filename) {
  final Promise<Buffer> p = Promise.defer();

  vertx.fileSystem().readFile(filname, new Handler<AsyncResult<Buffer>>() {
    @Override
    public void handle(AsyncResult<Buffer> event) {
      if (event.succeeded()) {
        p.fulfill(event.result());
      } else {
        p.reject(event.cause());
      }
    }
  });

  return p;
}
````

In the future there will be a more convenient way of coping with AsyncResult's succeed() value.