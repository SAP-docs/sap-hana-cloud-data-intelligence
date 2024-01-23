<!-- loio6f49ea7835044fa99a7bf397642b2d40 -->

# Jupyter Operator Examples

Use the examples in this topic to help you understand how to work with the Jupyter operator and notebook.



<a name="loio6f49ea7835044fa99a7bf397642b2d40__section_a2j_q45_zyb"/>

## Writing Data to an Output Port

To send data to an output port, call the function `send`.

> ### Example:  
> The following code snippet writes the `data` string object to the output port `out`:
> 
> ```
> # assuming that there is an output port named 'out'
> data="some string"
> send('out', data)
> ```

If the data type of the output string isn't compatible with the SAP Data Intelligence Modeler data type of the output port named `out`, the Modeler issues an error and the graph fails. To choose your port types, see [Correspondence Between Modeler and Python Data Types](correspondence-between-modeler-and-python-data-types-81f40a2.md).



<a name="loio6f49ea7835044fa99a7bf397642b2d40__section_cxw_t45_zyb"/>

## Working with Callbacks

> ### Example:  
> The following code snippet defines a simple function that prints and receives data:
> 
> ```
> def on_data_in(datain):
>     print(datain)
> ```
> 
> Test this function as a callback using the `try_port_callback` function. The function runs the callback once with the data from the specified port.
> 
> > ### Note:  
> > The `try_port_callback` function is available only in interactive mode.
> 
> If an exception happens during the `try_port_callback` function run, the application throws an exception in the notebook kernel, but doesn't affect the graph state. The application prints the exception and the stack trace to the last active cell output:
> 
> ```
> # assuming that there is an input port named 'in'
> try_port_callback('in', on_data_in)
> ```
> 
> > ### Note:  
> > When `on_data_in` calls the `print` function, you can see the received data printed in the last active cell in the Jupyter notebook user interface.
> 
> After you test and adapt the `on_data_in` function to the desired behavior, register the function as a callback for the input port `in` by calling `set_port_callback`. Then, every time there's a new message in the input port `in`, the application calls the callback `on_data_in`:
> 
> ```
> # assuming that there is an input port named 'in'
> set_port_callback('in', on_data_in)
> ```
> 
> If an exception happens during the run of the callback that's registered with the `set_port_callback` function, the application logs an exception in the Python subengine and the graph fails.



### Unregistering a Callback

> ### Example:  
> To unregister a callback so that it no longer runs, use the function `remove_port_callback` with the function as a parameter:
> 
> ```
> remove_port_callback(on_data_in)
> 
> ```



### Registering Callbacks to Multiple Ports

> ### Example:  
> To register a callback to multiple ports, use a function that receives the same number of parameters as the number of ports you register the callback to:
> 
> ```
> def on_multiple_inputs(input1, input2):
>     pass
> 
> # assuming that there are two input ports: 'in1', 'in2'
> set_port_callback(['in1', 'in2'], on_multiple_inputs)
> ```



<a name="loio6f49ea7835044fa99a7bf397642b2d40__section_htr_hp5_zyb"/>

## Run in Productive Mode

Run Jupyter operators in productive mode so that the cells run without any user interaction. Activate the productive mode by setting the Jupyter operator parameter *Productive* to true in the SAP Data Intelligence Modeler application.

When in productive mode, cells tagged as productive are run with no user interaction. In the Jupyter notebook user interface, find a tab on top of each cell. To tag a cell, type the applicable tag in the tab's textbox. For example, type `productive`, choose *Add tag*.

> ### Example:  
> ```
> def my_productive_code(value):
>     send('out', value)
>     
> set_port_callback('in', my_productive_code)
> ```

> ### Note:  
> -   If the productive code references some other code in a cell that isn't marked with the tag `productive`, the application issues a runtime error because the operator ignores non-productive code in this mode, making the graph fail. Therefore, ensure that you mark all relevant code cells as `productive`.
> 
> -   When running in productive mode, you can't access the Jupyter notebook user interface to interact with the cells.
> 
> -   You can't change the run mode at runtime. To change the run mode, stop the graph, set the *Productive* parameter to true \(on\) or false \(off\), and then restart the graph.



<a name="loio6f49ea7835044fa99a7bf397642b2d40__section_ew3_kp5_zyb"/>

## Accessing the Configuration Object

You can set the configuration object in the Jupyter operator configuration. Call `get_config` in the SAP Data Intelligence Modeler application.

> ### Example:  
> To get the location of the current notebook, access the “notebookPath” key from the config object:
> 
> ```
> config = get_config()
> config["notebookPath"]
> ```



<a name="loio6f49ea7835044fa99a7bf397642b2d40__section_jtq_fl1_1zb"/>

## Installing Python Modules

To install Python modules, use the `add_dependency` function.

> ### Example:  
> Use `add_dependency` to install the `h5py` module:
> 
> ```
> add_dependency("h5py")
> 
> ```



<a name="loio6f49ea7835044fa99a7bf397642b2d40__section_s5b_3l1_1zb"/>

## Work with Messages

To access the Message type, call the `Message` function. Access the body and attributes of a message object, `msg`, as `msg.body` and `msg.attributes`, respectively.****

**`Message(body, attributes)`**

```
Args:
    *body (object): body of the message
    attributes(dict(str, object) | None): attributes of the message
```

> ### Example:  
> ```
> msg = Message(None,{"debug": True, "config": {}})
> 
> ```

