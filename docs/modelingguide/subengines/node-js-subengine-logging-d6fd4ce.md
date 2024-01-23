<!-- loiod6fd4ced90b24533875ed2de7395f74a -->

# Node.js Subengine Logging

The logging library provides different logging APIs that propagate logging information to the Node.js subengine. In local development that isn't running with Node.js subengine core, the console is used for logging.



<a name="loiod6fd4ced90b24533875ed2de7395f74a__section_nhw_zn1_chb"/>

## Logging Levels

Logging levels use the npm severity ordering, which ascends from the most important to the least important. In the following example, errors are the most important and debug level is the least important:

> ### Example:  
> ```
> 
> {
>   ERROR: 0,
>   WARN: 1,
>   INFO: 2,
>   DEBUG: 3,
> }
> ```



<a name="loiod6fd4ced90b24533875ed2de7395f74a__section_hh3_d41_chb"/>

## Setting Logging Levels

By default, the logging level is set to *INFO*. You can change the log level as shown in the following code snippet:

```
const operator: Operator = Operator.getInstance();
operator.logger.logLevel = "ERROR"; // case insensitive
```



<a name="loiod6fd4ced90b24533875ed2de7395f74a__section_qtc_h41_chb"/>

## Use the Logging API

The logging APIs are directly accessible from the operator instance. The following code snippet shows the logging APIs:

```
const operator: Operator = Operator.getInstance();

// if not running in subengine, log is outputted to console
operator.logger.info("message", ...); // log level INFO
// DEBUG level
operator.logger.debug("message", ...);
// WARNING level
operator.logger.warn("message", ...);
// ERROR level
operator.logger.error("message", ...);
```

You can also create a logger instance in your operators as shown in the following code snippet:

```
import { Logger } from "@sap/vflow-sub-node-sdk";

const logger: Logger = new Logger("LOG_LEVEL");
logger.info("message");
```



<a name="loiod6fd4ced90b24533875ed2de7395f74a__section_kzq_m41_chb"/>

## Log Message Format

The log message accepts zero or more placeholder tokens. The system replaces each placeholder with the converted value from the corresponding argument. The log message is then a `printf`-like format string. For supported placeholders, see [nodejs.org](https://nodejs.org/dist/latest-v8.x/docs/api/util.html#util_util_format_format_args) on the Nodejs.org website.

```
operator.logger.debug("debug message %j", { foo: "bar" });
// 2018-11-22T13:03:01.088Z - debug: Operator "sampleiotdevicegeneratingdata1" (pid: 11912)|debug message { "foo": "bar" }
```

