## SpringBoot

**@RestControllerAdvice的优先级要比在代码中的try catch的优先级要高**

```java
@Slf4j
@RestControllerAdvice
public class ExceptionAdviceCore extends ResponseEntityExceptionHandler {

    @ExceptionHandler(ServiceException.class)
    public ResponseVO<T> serviceExceptionAdvice(ServiceException serviceException) {
        log.error("controller serviceException error ", serviceException);
        return ResponseHelper.error(serviceException.getMsg());
    }
}
```

```java
@PostMapping("/v1/queryOperationActivityInfoList")
public ResponseVO queryOperationActivityInfoList(@RequestBody OperationActivityInfoDto operationActivityInfo, HttpServletRequest request) {
        try {
            return ResponseHelper.success(operationActivityInfoService.queryOperationActivityInfoList(operationActivityInfo, request));
        } catch (ServiceException e) {
            log.error("分页条件查询运营-活动管理异常！ex={}", e.getMessage(), e);
            return ResponseHelper.error(e.getMessage());
        }
}
```

以上代码是不会执行到

```java
log.error("分页条件查询运营-活动管理异常！ex={}", e.getMessage(), e);
```