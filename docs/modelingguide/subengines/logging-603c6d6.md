<!-- loio603c6d6a7d384343b91ac7c593738465 -->

# Logging

There are a set of built-in methods to enable logging in the Python subengine. The table below summarizes the set of methods you can use to log information.




<table>
<tr>
<th valign="top">

Subclassing BaseOperator

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

self.logger.info\(str\)

</td>
<td valign="top">

Log with level *INFO* 

</td>
</tr>
<tr>
<td valign="top">

self.logger.debug\(str\)

</td>
<td valign="top">

Log with level *DEBUG* 

</td>
</tr>
<tr>
<td valign="top">

self.logger.error\(str\)

</td>
<td valign="top">

Log with level *ERROR* 

</td>
</tr>
<tr>
<td valign="top">

self.logger.warning\(str\)

</td>
<td valign="top">

Log with level *WARNING* 

</td>
</tr>
<tr>
<td valign="top">

self.logger.fatal\(str\)

</td>
<td valign="top">

Log with level *FATAL* \(stops the graph\)

</td>
</tr>
<tr>
<td valign="top">

self.logger.critical\(str\)

</td>
<td valign="top">

Log with level *CRITICAL* \(stops the graph\)

</td>
</tr>
</table>

> ### Note:  
> If you want to report an error and stop the graph from inside the operator code, raise an exception instead of logging with the `logger.fatal("")` or `logger.critical("")` command. Using those will have unintended consequences.

> ### Note:  
> If you start a new thread inside your operator then you should capture your exceptions inside this thread and use `self._propagate_exception(e)` function so that the main thread can handle it.

You can check all logs using SAP Data Intelligence Modeler's UI. To do that, you must click the *Trace* tab. You can filter the logging messages by level or you can even search for a specific log. You can also download the logging history as a CSV file.

You can also send the logging messages to SAP Data Intelligence Modeler's external log. To achieve that, open *Trace Publisher Settings*, next to the search bar. Turn on *Trace Streaming* and configure the set of logging messages you want to publish. For example, if you wanted to publish all logging messages which have level *fatal* or *error*, you would have to change *Trace Level* to *ERROR*.

