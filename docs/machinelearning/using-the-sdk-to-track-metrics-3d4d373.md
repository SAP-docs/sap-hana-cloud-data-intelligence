<!-- loio3d4d3738ed194d00a3493ece0beacd92 -->

# Using the SDK to Track Metrics

The SAP Data Intelligence SDK helps you to track your data science experiments and report metrics.



<a name="loio3d4d3738ed194d00a3493ece0beacd92__section_rx5_rqs_d3b"/>

## Importing the Tracking Module

To get started with the ML Tracking SDK, import the `tracking` module using the following command.

```py
from sapdi import tracking
```



<a name="loio3d4d3738ed194d00a3493ece0beacd92__section_ysf_sqs_d3b"/>

## Using the Tracking Functionality

The SDK works with a wrapper, in which you create an instance of `MLTrackingSDK`. We recommend that you surround your experiment with `start_run()` and `end_run()` at the beginning and end respectively. When you use `start_run()`, you have the option to specify the name of a run collection, which allows you to group different runs of your experiment, and you can specify the name of the run that is being started. To do so, use:

-   <code>run_collection_name='<i class="varname">&lt;default&gt;</i>'</code> and pass in a string value. The default is None.

-   <code>run_name='<i class="varname">&lt;default&gt;</i>'</code> and pass in a string value. The default is None.


If you don't specify a name for your run collection, the system creates a default one for each source \(that is, notebook or pipeline\). The name of the default run collection is the same as that of the source. These default run collections are shown in the metrics explorer with the suffix *\(Default\)*. If you don't specify a name for a run, the system sets the run ID as the name. You can update the association between the run and the run collection, or update the run name at any time using `update_run_info`.

> ### Example:  
> You are using a Jupyter notebook called “abc” to log runs. You log a few runs with a run collection called “RC1”. You then log a few more runs in a run collection without a name. For the first set of runs, a run collection called “RC1” is created. For the second set of runs, the system creates a default run collection with the name “abc”. In total, two run collections are created.

When you create a run collection, we recommend that you include runs from one source only \(that is, from one notebook or one pipeline\).

If you want to log metrics after `end_run()`, `log_metric` can be called with an associated run ID as an additional parameter but it will be logged with the context that was used to initialize the SDK.

Within your `MLTrackingSDK` instance, you can call the following functions:


<table>
<tr>
<th valign="top">

Function

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

`log_parameters`

</td>
<td valign="top">

You call this function to log parameters or configuration variables. It requires the parameters `name` and `value`. The type of each parameter must be string \(if another type is passed, it will be automatically converted to string\).

`name` has a limit of 256 characters and `value` has a limit of 5000 characters.

> ### Note:  
> Two system-defined parameters are added by the system. The first is `start`, which captures the start time of the run, and the other is `end`, which captures the end time of the run. The keywords `start` and `end` are case-sensitive and reserved. You cannot use these words for other parameter names. If you do so, system-defined parameters will be overwritten, resulting in unexpected behavior.



</td>
</tr>
<tr>
<td valign="top">

`log_metric`

</td>
<td valign="top">

You call this function to log metrics. It requires the parameters `name` and `value`, whereby `value` must be numeric. You can log multiple values to the same `name` by logging multiple metric records \(each for one value\) and using the same `name` for each metric.

If you want to log metrics after `end_run()`, you can call the function with the associated run object as an additional parameter. The metrics are logged with the context used to initialize the SDK.

`name` has a limit of 256 characters and is case-sensitive.

`value` must be in the range between -2.2250738585072014E-308 and 1.7976931348623157E308. If more than one value is given to the same parameter name, only the last value is stored.

</td>
</tr>
<tr>
<td valign="top">

`log_metrics`

</td>
<td valign="top">

You call this function to pass a list of metric items that are to be captured. Each item in the list is a dictionary that has the same parameters as the `log_metric` function. You can log multiple values to the same `name` by logging multiple metric records \(each for one value\) and using the same `name` for each metric.

</td>
</tr>
<tr>
<td valign="top">

`persist_run`

</td>
<td valign="top">

You can call this function to explicitly persist the logged metrics or parameters. In the default configuration, the metrics and parameters are persisted at the end of the run.

> ### Note:  
> Metrics are persisted at the end of a run or when the internal cache has reached 1.5 MB. We recommend that you use `persist_run` only if your use-case requires it \(for example, you need almost real-time tracking\). Otherwise, we recommend that you use the metrics that are persisted at the end of the run.



</td>
</tr>
<tr>
<td valign="top">

`set_tags`

</td>
<td valign="top">

You call this function to set tags under the current run. Tags are user-defined properties that are associated with a run, and are case-sensitive. Each tag is a key\(string\)-value\(string\) pair. Tags can also be used to filter runs. If more than one value is given to the same tag key, only the last value is stored.

> ### Note:  
> One system-define tag is added by the system with the tag-key `runName`, which stores the name of the run. The keyword `runName` is case-sensitive and reserved. You cannot use it as a tag-key for other tags. If you do so, the system-defined tag will be overwritten, resulting in unexpected behavior.



</td>
</tr>
<tr>
<td valign="top">

`set_labels`

</td>
<td valign="top">

You call this function to log labels for the current run. Labels are a set of key-value pairs that are associated with a run. Label keys are case sensitive. Labels can be used to store semantic data or UI formatting data. Runs cannot be filtered by label. If more than one value is given to the same label key, only the last value is stored.

</td>
</tr>
<tr>
<td valign="top">

`delete_runs`

</td>
<td valign="top">

You call this function to delete any persisted metrics. It requires one or more of the following parameters: `scenario`, `scenario_version`, `pipeline`, `execution`, `notebook`, and `run`.

If you specify `notebook`, you must also specify `scenario` or `run`.

`scenario` also enables bulk deletion, in which case the other parameters cannot be specified. To delete multiple scenarios, pass the IDs of each scenario as comma-separated values. For example, `scenario='<id>,<id>,<id>'`.

</td>
</tr>
<tr>
<td valign="top">

`get_runs`

</td>
<td valign="top">

You call this function to fetch the run object that contains the metrics, parameters, tags, and so on. It requires one or more of the parameters `scenario`, `scenario_version`, `pipeline`, `execution`, `notebook`, and `run`.

The SDK creates an ID for the run and returns it as a run object when `start_run()` is called. You can use this object to retrieve the metrics and parameters recorded in this run.

If you specify `notebook`, you must also specify `scenario` or `run`. `Notebook` returns the `Notebook` object. It requires `id` as an argument, where `id` represents the notebook ID. For example, <code>tracking.Notebook(id=<i class="varname">&lt;NOTEBOOK_ID&gt;</i>)</code>. `RUN` returns the `Run` object. It requires `id` as an argument, where `id` represents the run ID. For example, <code>tracking.Run(id=<i class="varname">&lt;RUN_ID&gt;</i>)</code>.

This method returns the two system-defined parameters and the system-defined tag for each run, along with user-defined entries.

</td>
</tr>
<tr>
<td valign="top">

`get_metrics_history`

</td>
<td valign="top">

You call this function to fetch a specific metric or metrics, along with the corresponding values for a run. A maximum of 1000 values can be returned for each metric.

You call this function to fetch a list of persisted metrics that correspond to all values logged for a given metric. Only 1000 entries are allowed per metric.

`get_metrics_history` expects two parameters: `run` and `metrics` \(the list of metric names\).

-   If `metrics` is not given, the function returns a list of metrics objects that correspond to all values logged for each metric.
-   If `runId` is not given, function returns a list of metrics objects for the active run, provided that some metrics are persisted in the database.



</td>
</tr>
<tr>
<td valign="top">

`update_run_info`

</td>
<td valign="top">

You call this function to update the run name, run collection name, or tags for a given run ID. It can be called using the arguments `run_name`, `run_collection_name`, and `tags` before the run becomes active or after it has ended. If a run obejct is not specified, the run that is currently active is updated.

</td>
</tr>
</table>

> ### Example:  
> The code below shows you how you can log one metric at a time.
> 
> ```py
> from sapdi import tracking
> 
> run = tracking.start_run()
> # tracking.start_run(run_collection_name='rc1') # Use this to group different runs under a collection
> 
> params = {
>     'input_size': 784,
>     'hidden_size': 500,
>     'num_classes': 10,
>     'num_epochs': 2,
>     'batch_size': 100,
>     'learning_rate': 0.001,
>     'model_file': 'model.ckpt'
> }
> 
> tracking.log_parameters(params)
> 
> 
> # the experimental code.
> for i in range(params.get('num_epochs')):
>     tracking.log_metric(name='metric_name', value=1)
> 
> # more code
> tracking.set_tags({
>     "tag_key": "tag_value",
>     "tag_key_n": "tag_value_n"
>   })
> tracking.set_labels({
>     "accuracy": {
>       "format_string": "percentage"
>     }})
> 
> # more code
> 
> tracking.end_run()
> ```

> ### Example:  
> The code below shows you how to log multiple metrics, as well as how to fetch and delete metrics.
> 
> ```py
> from sapdi import tracking
> 
> run = tracking.start_run()
> 
> metrics = {
>     'accuracy': 0.89,
>     'cross_entropy': 3.2,
>     'avg_loss': 0.59
> }
> 
> tracking.log_metrics(metrics)
> 
> # more code
> 
> # Mark the end of tracking
> tracking.end_run() # persists the metrics at the end of the run
> 
> # Persisting metrics after the end
> tracking.log_metric('uncertainty', 0.4, run=run)
> 
> # To Fetch payload from API for the current run
> runs = tracking.get_runs(run=run)
> 
> # To Fetch metrics from API by tags(in addition with other parameters)
> runs = tracking.get_runs(run=run, tags = {'tag_key': 'tag_value'})
> **Note**: tag parameter is of type python dictionary, in which key is tag name and value is tag value
> 
> # To Delete all payload for the current run
> tracking.delete_runs(run=run)
> 
> # To Delete run for single/current scenario
> scenario_object = sapdi.get_current_scenario()
> tracking.delete_runs(scenario=scenario_object)
> 
> # To Delete runs for multiple scenarios
> scenario_list = sapdi.list_scenarios()
> tracking.delete_runs(scenario=scenario_list)
> ```

> ### Example:  
> The code below shows you how to log labels for a run.
> 
> ```
> tracking.set_labels({
> "accuracy": {
> "format_string": "percentage"
> }
> “Label_n” : value_n
> })
> ```

> ### Example:  
> The code below shows you how to set and update the run information.
> 
> ```
> # To set run_name or run_collection while starting run
> run = tracking.start_run(run_collection_name='Logistics Regression', run_name='LR_run_5')
> 
> # more code
> 
> # Update run_name or run_collection of current run
> tracking.update_run_info(run_collection_name='Logistics Regression2', run_name='LR_run_6')
> 
> # more code
> 
> tracking.end_run()
> 
> # Update run_name or run_collection after run has ended
> tracking.update_run_info(run=run, run_collection_name='Logistics Regression3', run_name='LR_run_7')
> ```

> ### Example:  
> The code below shows you how to get the metrics history.
> 
> ```py
> from sapdi import tracking
> run = tracking.start_run()
> #logging metrics multiple times
> for i in range(10):
>     tracking.log_metrics({
>         'accuracy': 0.89,
>         'cross_entropy': 3.2,
>         'avg_loss': 0.59
>     })
>     
> tracking.persist_run()
> # Fetch metrics history(of accuracy & avg_loss) while run is active
> metric_history = tracking.get_metrics_history(metrics=['accuracy','avg_loss'])
> # Fetch history all metrics while run is active
> metric_history_all = tracking.get_metrics_history()
> # more code
> # Mark the end of tracking
> tracking.end_run() # persists the metrics at the end of the run
> # Persisting metrics after the end
> tracking.log_metric('uncertainty', 0.4, run=run)
> # To Fetch payload from API for the current run
> runs = tracking.get_runs(run=run)
> # Fetch metrics history(of accuracy & avg_loss) after run has ended
> metric_history = tracking.get_metrics_history(run=runs[0], metrics=['accuracy','avg_loss'])
> # Fetch history all metrics while run after run has ended
> metric_history_all = tracking.get_metrics_history(run=runs[0])
> ```



<a name="loio3d4d3738ed194d00a3493ece0beacd92__section_xtt_gsp_zkb"/>

## See the Tracking SDK in Action

The video below shows an example of how you can track the metrics for predicting house prices using lasso regression and random forest algorithms.



**Related Information**  


[Submit Metrics](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/b792d72b009a41b090c896d374a4dc17.html "The Submit Metrics operator submits your model metrics to the ML Tracking API. The metrics can be viewed in ML Scenario Manager.") :arrow_upper_right:

