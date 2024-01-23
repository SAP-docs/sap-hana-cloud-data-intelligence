<!-- loio46018e2bed434838926bb9d1906f86b2 -->

# Node.js SDK API Reference

To use the Node.js SDK, use the API commands as described in this reference.




<dl>
<dt><b>

getInstance\(basePath\)

</b></dt>
<dd>

-   basePath `<string>` Optional. The path to the operator descriptor \(operator.json\) directory. Default basePath is the directory where the operator's script file is located.
-   Returns: `<Operator>`



</dd>
<dd>

Creates an operator instance \(singleton\).



</dd>
</dl>


<dl>
<dt><b>

config

</b></dt>
<dd>

-   Returns: `<object>`




</dd>
<dd>

`operator.config` returns the configuration of this operator. If you change this operator in the Modeler application, the command returns the runtime configuration. Otherwise it returns the design time configuration, which is specified in the operator.json.



</dd>
</dl>


<dl>
<dt><b>

addShutdownHandler\(handler\)

</b></dt>
<dd>

-   handler `<Function>` The handler to call before terminating this operator.

-   Returns: `<void>`



</dd>
<dd>

`operator.addShutdownHandler()` adds a shutdown handler when terminating the process. The method accepts a callback function that takes only one optional error parameter, for example, taking an `(err) => ...` callback.

The operator fails when the shutdown handler is not a function or it is undefined.

The following code snippet shows how to use a callback function:

```
const handler = (cb: (err?: Error) => void): void => {
  // do something …
  cb(…); // callback with void or an error
};

const operator: Operator = Operator.getInstance();
operator.addShutdownHandler(handler);
```



</dd>
</dl>


<dl>
<dt><b>

done\(\)

</b></dt>
<dd>

-   Returns: `<void>`




</dd>
<dd>

Terminates the operator process with exit code 0.



</dd>
</dl>


<dl>
<dt><b>

fail\(message\)

</b></dt>
<dd>

-   message `<string>` Error message to write when the operator fails.

-   Returns: `<void>`



</dd>
<dd>

Terminates this operator process with exit code 1, then writes an error message to `process.stderr`.



</dd>
</dl>


<dl>
<dt><b>

getInPort\(name\)

</b></dt>
<dd>

-   `name <string>` The name of the input port.

-   Returns: `<InPort>`



</dd>
<dd>

Finds a single input port by its name and returns the name.

The operator fails if it doesn't find the port.



</dd>
</dl>


<dl>
<dt><b>

getOutPort\(name\)

</b></dt>
<dd>

-   name `<string>` The name of the output port.

-   Returns: `<OutPort>`



</dd>
<dd>

Finds a single output port by its name and returns the name.

The operator fails if it doesn't fine the port.



</dd>
</dl>


<dl>
<dt><b>

getInPorts\(\)

</b></dt>
<dd>

-   Returns: `<Map<string, InPort>>`




</dd>
<dd>

Returns all input ports of this operator. Returns an empty map when it doesn't find any input ports.



</dd>
</dl>


<dl>
<dt><b>

getOutPorts\(\)

</b></dt>
<dd>

-   Returns: <Map<string, OutPort\>\>




</dd>
<dd>

Returns all output ports of this operator. Returns an empty map when it doesn't find any output ports.



</dd><dt><b>

logger

</b></dt>
<dd>

-   Returns: `<Logger>`




</dd>
<dd>

Returns a logger instance to use for logging. For more information, see [Node.js Subengine Logging](node-js-subengine-logging-d6fd4ce.md).



</dd>
</dl>

