<!-- loio542e31ecaf2e4f338302cbedcf08d425 -->

# List of BaseOperator Methods

When subclassing *BaseOperator*, you will need to use a set of methods to set callbacks, send messages, etc. The list below summarizes the *BaseOperator* methods you might need.



> ### Note:  
> Each callback registered in the script runs in a different thread.
> 
> As the script developer, you should handle potential concurrency issues such as race conditions. You can, for instance, use primitives from the Python threading module to get protected against those issues.
> 
> For more information, see the [official documentation at python.org.](https://docs.python.org/3/library/threading.html)


<dl>
<dt><b>

\_get\_operator\_info\(self\)

</b></dt>
<dd>

This method should be overridden by a subclass. It should return the OperatorInfo of this operator. OperatorInfo defines some key features of the operator such as port names and other things.



</dd>
<dd>

Returns:



</dd>
<dd>

OperatorInfo



</dd>
</dl>


<dl>
<dt><b>

\_init\(self\)

</b></dt>
<dd>

This method can be overridden by a subclass. This method will be called after the user defined configurations have already been set. This method will be called for all graph's operators before any operator has been started.



</dd>
</dl>


<dl>
<dt><b>

\_prestart\(self\)

</b></dt>
<dd>

This method can be overridden by a subclass. It should contain code to be executed before the operator's callbacks start being called. The code here should be non-blocking. If it is blocking, the callbacks you have registered will never be called. You are allowed to use the method self.\_send\_message inself.\_prestart. However, bare in mind that other operators will only receive this data sent when their \_prestart have already finished. This is because their callback will only be active after their \_prestart have finished



</dd>
</dl>


<dl>
<dt><b>

shutdown\(self\)

</b></dt>
<dd>

This method can be overridden by a subclass. It should contain code to be executed after the operator's main loop is finished.



</dd>
</dl>


<dl>
<dt><b>

\_send\_message\(self, port, message\)

</b></dt>
<dd>

Puts an item into an output queue.



</dd>
<dd>

Args:



</dd>
<dd>

-   port \(str\): name of output port

-   message \(...\): item to be put




</dd><dt><b>

\_set\_port\_callback\(self, ports, callback\)

</b></dt>
<dd>

This method associate input 'ports' to the 'callback'. The 'callback' will only be called when there are messages available in all ports in 'ports'. If this method is called multiple times for the same group of ports then the old 'callback' will be replaced by a new one. Different ports group cannot overlap.



</dd>
<dd>

Args:



</dd>
<dd>

-   ports \(str|list\[str\]\): input ports to be associated with the callback. 'ports' can be a list of strings with the name of each port to be associated or a string if you want to associate the callback just to a single port.
-   callback \(func\[...\]\): a callback function with the same number of arguments as elements in 'ports'. Also the arguments will passed to 'callback' in the same order of their corresponding ports in the 'ports' list.



</dd>
</dl>


<dl>
<dt><b>

\_remove\_port\_callback\(self, callback\)

</b></dt>
<dd>

Remove the 'callback' function. If it doesn't exist, the method will exit quietly.



</dd>
<dd>

Args:



</dd>
<dd>

-   callback: Callback function to be removed.




</dd>
</dl>


<dl>
<dt><b>

\_add\_periodic\_callback\(self, callback, milliseconds=0\)

</b></dt>
<dd>

Multiple distinct periodic callbacks can be added. If an already added callback is added again, the period 'milliseconds' will be replaced by the new one. If you want two callbacks with identical behavior to be run simultaneously then you will need to create two different functions with identical body.



</dd>
<dd>

Args:



</dd>
<dd>

-   callback \(func\): Callback function to be called every 'milliseconds'.

-   milliseconds \(int|float\): Period in milliseconds between calls of 'callback'. When not specified it is assumed that the period is zero.




</dd>
</dl>


<dl>
<dt><b>

\_change\_period\(self, callback, milliseconds\)

</b></dt>
<dd>

Args:



</dd>
<dd>

-   callback \(func\): Callback for which the period will be changed. If callback is not present on the registry, nothing will happen.

-   milliseconds \(int\\float\): New period in milliseconds.




</dd>
</dl>


<dl>
<dt><b>

\_remove\_periodic\_callback\(self, callback\)

</b></dt>
<dd>

Args:



</dd>
<dd>

-   callback \(func\): Callback function to be removed.




</dd>
</dl>


<dl>
<dt><b>

register\_metric\(self, metric\_type, name, metric\_infos=\[\]\)

</b></dt>
<dd>

Register a new metric and its respective 'MetricInfo' \(to create it check next section\).



</dd>
<dd>

Args:



</dd>
<dd>

-   name \(str\): It is the metric name defined in the operator \(this should be a string without spaces\).

-   metric\_type \(str\): It defines the type of the updated value. They can be 'consumer', 'producer', 'float' or 'int'.

    Consumer and producer aggregators are 'int' and already have the 'metric\_infos' field pre-configured, so these aggregators ignore it.

-   metric\_infos \(list\[MetricInfo\]\): It is the list of information to be presented about a specific metric.

    Returns:

    -   Metric: a metric instance which allows the operator to update its value.





</dd>
</dl>


<dl>
<dt><b>

create\_metric\_info\(self, metric\_type, scale, name, display\_name, unit\)

</b></dt>
<dd>

This method is a helper function to create 'MetricInfo' in order to register metrics for the operator.



</dd>
<dd>

Args:



</dd>
<dd>

-   metric\_type \(str\): It is the metric type and it can be: 'value', 'sum', 'max', 'min', 'count', 'avg', 'rate'.
-   scale \(int\): It is an integer factor that multiplies all 'MetricInfo' output values.
-   name \(str\): It is a metric name following the previous 'Name' pattern.
-   display\_name \(str\): The name displayed to the user \(it should be friendlier\).
-   unit \(str\): It is a string with the metric unit. The following units are pre-configured to scale up when necessary: 'Bytes', 'KB', 'MB', 'GB', 'TB', 'PB', 'Bytes/s', 'KB/s', 'MB/s', 'GB/s', 'TB/s' and 'PB/s'. For example, when a value of unit 'Bytes' reaches '1024' it automatically becomes 'KB'.

    Returns:

    -   MetricInfo





</dd>
</dl>


<dl>
<dt><b>

register\_websocket\_route\(self, path, target, handler\)

</b></dt>
<dd>



</dd>
<dd>

Args:



</dd>
<dd>

-   path \(str\): operator complete url.

-   target \(str\): target path to possible websocket connection to be used.
-   handler \(func\[websocket\_handler\]\): function that will be called with the websocket handler as argument.



</dd>
</dl>


<dl>
<dt><b>

register\_static\_route\(self, path, target\)

</b></dt>
<dd>

Registers a new static route for the operator. This method only works as expected when called during the operator initialization.



</dd>
<dd>

Args:



</dd>
<dd>

-   path \(str\): path for the operator complete url.

-   Registers a new websocket route for the operator. This method only workstarget \(str\): target path to directory whose elements will be served.



</dd>
</dl>


<dl>
<dt><b>

register\_rproxy\_route\(self, path, target\)

</b></dt>
<dd>

Registers a new rproxy route for the operator. This method only works as expected when called during the operator initialization.



</dd>
<dd>

Args:



</dd>
<dd>

-   path \(str\): path from the operator complete url.

-   target \(str\): target url.



</dd>
</dl>

