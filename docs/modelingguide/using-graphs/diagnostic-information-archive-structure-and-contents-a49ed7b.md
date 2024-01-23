<!-- loioa49ed7bfcc0a4f909904937fb846016b -->

# Diagnostic Information Archive Structure and Contents

This is the directory structure and contents of the diagnostic information archive.



<a name="loioa49ed7bfcc0a4f909904937fb846016b__section_dnl_lmv_bhb"/>

## Zip Archive Structure

```
vflow-diagnostic-<timestamp>.zip
├── version.json
├── graphs.json
├── errors.txt
├── api-pods
|   ├── pods.json
|   ├── goroutine.txt
|   ├── <podname>
|   |   └── goroutine.txt
|   |   └── logs-<podname>.txt
|   |   └── pod-<podname>.json
├── <graph-source>-<handle>
|   ├── graph.json
|   ├── execution.json
|   ├── <group-instance-id>
|   |   └── goroutine.txt
|   |   └── heap.txt
|   |   └── logs-<podname>.txt
|   |   └── pod-<podname>.json
...
|   └── <group-instance-id>
|   |   └── goroutine.txt
|   |   └── heap.txt
|   |   └── logs-<podname>.txt
|   |   └── pod-<podname>.json
├── <graph-source>-<handle>
...
```

-   **[version.json File](version-json-file-8b2b278.md "The version.json file contains version information.")**  
The `version.json` file contains version information.
-   **[graphs.json File](graphs-json-file-6088f70.md "The graphs.json file contains brief information about executed
        graphs, including files that are completed and not deleted. ")**  
The `graphs.json` file contains brief information about executed graphs, including files that are completed and not deleted.
-   **[<graph-source\>-<handle\> Folders](graph-source-handle-folders-5b3bda1.md "The graph-source-handle
		folder contains detailed information about graph execution. For example:
			com.sap.demo.datagenerator-9a6eeb59abb242baabb110dba50ae178. ")**  
The <code><i class="varname">&lt;graph-source&gt;</i>-<i class="varname">&lt;handle&gt;</i></code> folder contains detailed information about graph execution. For example: `com.sap.demo.datagenerator-9a6eeb59abb242baabb110dba50ae178`.
-   **[graph.json File](graph-json-file-d12b03d.md "The graph.json file contains the graph definition. ")**  
The `graph.json` file contains the graph definition.
-   **[execution.json File](execution-json-file-8b01d80.md "The execution.json file contains information about the execution
		for a graph, such as groups, pods, processes (operator instances in a graph), and so on. ")**  
The `execution.json` file contains information about the execution for a graph, such as groups, pods, processes \(operator instances in a graph\), and so on.
-   **[events.json File](events-json-file-cee0f07.md "The events.json file contains information about graph events. ")**  
The `events.json` file contains information about graph events.
-   **[<group-instance-id\> Folders](group-instance-id-folders-2bed74e.md "For each instance of a group, a folder is created. ")**  
For each instance of a group, a folder is created.
-   **[logs-<pod-name\>.txt File](logs-pod-name-txt-file-0f4a70f.md "The logs-pod-name.txt file contains logs for a
		specific pod.")**  
The <code>logs-<i class="varname">&lt;pod-name&gt;</i>.txt</code> file contains logs for a specific pod.
-   **[pod-<pod-name\>.json File](pod-pod-name-json-file-aa2fe91.md "The pod-pod-name.json file contains a pod
		description.")**  
The <code>pod-<i class="varname">&lt;pod-name&gt;</i>.json</code> file contains a pod description.
-   **[goroutine.txt File](goroutine-txt-file-11827e0.md "The goroutine.txt file contains pprof output for a
			goroutine profile.")**  
The `goroutine.txt` file contains `pprof` output for a `goroutine` profile.
-   **[<heap.txt\> File](heap-txt-file-21df8e2.md "The heap.txt file contains
			pprof output for a heap profile.")**  
The <code><i class="varname">&lt;heap.txt&gt;</i></code> file contains `pprof` output for a `heap` profile.
-   **[api-pod Folder](api-pod-folder-cb21b4e.md "The api-pod folder contains information about vFlow API nodes. ")**  
The `api-pod` folder contains information about vFlow API nodes.

