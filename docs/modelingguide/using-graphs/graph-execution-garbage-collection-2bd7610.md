<!-- loio2bd7610e013d48068d649f333755fec0 -->

# Graph Execution Garbage Collection

To maintain the cluster, the Modeler employs Graph Garbage Collection using the following strategies: time-based and number-based.



Garbage collection settings are in the System Management properties. For a list of all system management properties, see [System Management Properties](https://help.sap.com/docs/SAP_DATA_INTELLIGENCE/ca509b7635484070a655738be408da63/3b07102657de4b8e9bbedc8d0184c3bd.html?version=Cloud) in the *Administration Guide*.

The garbage collector collects the following finished graphs:

-   completed \(always\)
-   dead \(optionally\)
-   paused \(optionally\)

For more information, see [Graph Status](graph-status-090bce6.md).



## Time-Based Strategy

The time-based strategy specifies the time before the garbage collector frees memory used by the finished graphs.


<table>
<tr>
<th valign="top">

Property

</th>
<th valign="top">

Default Value

</th>
<th valign="top">

Result

</th>
</tr>
<tr>
<td valign="top">

Garbage collection time limit for finished graphs.

</td>
<td valign="top">

72 hours

</td>
<td valign="top">

The Modeler collects graphs that have been finished for 3 days.

</td>
</tr>
</table>

The lowest value the Modeler system accepts is 1 minute. If you enter a value lower than 1 minute, the Modeler replaces the value with 1 minute. For more information about the format and layout of the duration, see the [Golang.org Parse Duration official documentation](https://golang.org/pkg/time/#ParseDuration).



<a name="loio2bd7610e013d48068d649f333755fec0__section_mlr_1rm_tkb"/>

## Number-Based Strategy

The number-based strategy limits the number of graphs per user in the Modeler at any time. When the user exceeds the limit, the Modeler removes completed graphs. If the user exceeds the limit and there aren't any finished graphs to be collected, the Modeler waits until finished graphs appear and then collects them.

> ### Note:  
> The number-based strategy prioritizes the removal of completed over dead over paused graphs.


<table>
<tr>
<th valign="top">

Property

</th>
<th valign="top">

Default Value

</th>
<th valign="top">

Result

</th>
</tr>
<tr>
<td valign="top">

Maximum number of graphs per user. Finished graphs will be deleted when exceeded.

</td>
<td valign="top">

50

</td>
<td valign="top">

At most, the Modeler keeps 50 graph executions at a time.

</td>
</tr>
</table>



<a name="loio2bd7610e013d48068d649f333755fec0__section_dch_mrm_tkb"/>

## Collect Dead Graphs

Because dead graphs can collect failure information, you can exclude dead graphs from garbage collection by setting the System Management property *Enable garbage collection for dead graphs*. Use failure information to analyze information about why the graph failed.

If you exclude dead graphs using the time-based strategy, the Modeler ignores dead graphs. In number-based mode, the Modeler doesn't include dead graphs in the graph count.


<table>
<tr>
<th valign="top">

Property

</th>
<th valign="top">

Default Value

</th>
<th valign="top">

Result

</th>
</tr>
<tr>
<td valign="top">

Enable garbage collection for dead graphs.

</td>
<td valign="top">

true

</td>
<td valign="top">

The Modeler collects dead graphs.

</td>
</tr>
</table>



<a name="loio2bd7610e013d48068d649f333755fec0__section_kmj_vhv_vrb"/>

## Collect Paused Graphs

By default, the removal of paused graphs is disabled, because pausing a graph signals the intent to resume it later.

However, if users have forgotten them, pausing graphs leads to the accumulation of many paused graphs over time. To prevent this accumulation, you can optionally enable the collection of paused graphs.

If you disable the collection of pause graphs and you use the time-based strategy, paused graphs are ignored. With the number-based strategy, the Modeler doesn't include paused graphs in the graph count.

> ### Note:  
> Be careful when you turn on the collection of paused graphs because it can cause the Modeler to lose possible valuable data.


<table>
<tr>
<th valign="top">

Property

</th>
<th valign="top">

Default Value

</th>
<th valign="top">

Result

</th>
</tr>
<tr>
<td valign="top">

Enable garbage collection for paused graphs.

</td>
<td valign="top">

false

</td>
<td valign="top">

The Modeler doesn't collect paused graphs.

</td>
</tr>
</table>

Changes to the Garbage Collector System Management parameters can take the system up to 5 minutes to update without restarting the application.

