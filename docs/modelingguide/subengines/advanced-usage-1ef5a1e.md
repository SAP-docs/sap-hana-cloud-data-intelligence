<!-- loio1ef5a1edadfe4747809fe7b35a0564e3 -->

# Advanced Usage

You can create operators without using the Modeler user interface.

> ### Note:  
> This method of creating operators requires that you restart the Modeler instance for the changes to take effect.

The following example assumes that you use a UNIX-like system to develop your operators. To run tests, you must download the `pysix_subengine` package on your local machine.

To download the `pysix_subengine` package, follow these steps:

1.  Log in to SAP Data Intelligence System Management as an administrator.

2.  Click the *File* button.

3.  Click the *Union View* button.

4.  Navigate to `files/vflow/subdevkits` on the file explorer.

5.  Right-click the *pysix\_subengine* folder and select *Export File*.


To create Python 3.9 operators, you must structure your solution \(a package that can be imported by SAP Data Intelligence System Management\) as follows:

```
my_solution/ 
	vrep/vflow/
		subengines/com/sap/python3.9/operators/ 
			myOperator1/
				operator.py
				operator.json
			com/
				mydomain/
					myOperator2/
						operator.py
						operator.json
	vsolution.json
```

The `vsolution.json` file should look like the following:

```
{
    "name": "vsolution_vflow_my_solution",
    "description": "My Solution",
    "license": "my license"
} 
```

> ### Note:  
> Python 2.7 is deprecated as of SAP Data Intelligence 1911; only Python 3.9 is now supported. The creation of new operators based on Python 2.7 is now disabled. Any existing custom operators based on Python 2.7 should be ported to Python 3.9.



<a name="loio1ef5a1edadfe4747809fe7b35a0564e3__section_md2_psp_gjb"/>

## Define the Operator Attributes and Behavior

The `operator.py` script defines both the operator attributes and the operator behavior.

> ### Note:  
> The script must be called `operator.py`.

The following is example code in the `operator.py` file:

```
from pysix_subengine.base_operator import PortInfo, OperatorInfo
from pysix_subengine.base_operator import BaseOperator

# The operator class name (which inherits BaseOperator) should have the same name as
# the operator's folder, except that its first letter should be uppercase.
class AppendString(BaseOperator):
    def __init__(self, inst_id, op_id):
        super(AppendString, self).__init__(inst_id=inst_id, op_id=op_id)

        # Default configuration fields. They will be shown in the UI.
        self.config.stringToAppend = ""
        self.config.method = "NORMAL"

        # Adds a callback '_data_in' that is called every time the
        # operator receives data in the inport 'inString'.
        self._set_port_callback('inString', self._data_in)
        self.__transform_data = None

    # This method is mandatory.
    # The operator.json will be generated based mostly on the OperatorInfo returned by this method.
    def _get_operator_info(self):
        inports = [PortInfo("inString", required=True, type_="string")]
        outports = [PortInfo("outString", required=True, type_="string")]
        return OperatorInfo("Append String",
                            inports=inports,
                            outports=outports,
                            icon="puzzle-piece",
                            tags={"numpy36": "1.16.1"}
                            dollar_type="http://sap.com/vflow/com.mydomain.appendString.schema.json#")
    def _set_websocket(self, handler):
        self.web_handler = handler
        self.web_handler.set_message_callback(self._on_message)

    def _on_message(self, message):
        self.web_handler.write_message(str(message))
        self._send_message("outString", message)

    def _data_in(self, data):
        self.metric.include_value(1)
        self._send_message('outString', self.__transform_data(data + self.config.stringToAppend))

    # Configs set in the UI are already available when this method is called.
    # _init is called before any operator main loop has started.
    def _init(self):
        metric_infos = []
        metric_infos.append(self._registry.create_metric_info(u'count', 1, u'name', u'display_name', u'unit'))
        self.metric = self.register_metric(u"int", u"TEST", metric_infos)

        self.register_websocket_route('/socket', 'test', self._set_websocket)
        self.register_static_route('/ui', 'static')
        self.register_rproxy_route('/rproxy/*path', 'http://localhost:' + str(self.config.port) + '/')
       
    	if self.config.method == "NORMAL":
            self.__transform_data = lambda x: x
        elif self.config.method == "UPPERCASE":
            self.__transform_data = lambda x: x.upper()
        else:
            raise ValueError("Unknown config set in configuration: '%s'." % self.config.method)

    # Called before the operator's main loop execution.
    # Other operators may already have started execution.
    def _prestart(self):
        pass

    # Called when the graph is being terminated.
    def shutdown(self):
        pass
```

Let's examine the script step-by-step. First, look at the class definition:

```
class AppendString(BaseOperator):
```

As you can see, the `AppendString` class extends the built-in `BaseOperator` class.

> ### Note:  
> The class name must have the same name as the folder, except the first letter must be uppercase, while the folder's first letter is lowercase. For example, if the folder is named `appendString`, the class should be named `AppendString`.

Now let's examine each of the methods:

```
def __init__(self, inst_id, op_id):
    super(AppendString, self).__init__(inst_id=inst_id, op_id=op_id)

    # Default configuration fields. They will be shown in the UI.
    self.config.stringToAppend = ""
    self.config.method = "NORMAL"

    # Adds a callback '_data_in' that is called every time the
    # operator receives data in the inport 'inString'.
    self._set_port_callback('inString', self._data_in)
    self.__transform_data = None
```

This method is the class constructor. First it calls `super(AppendString, self).__init__(inst_id=inst_id, op_id=op_id)`.

In the next line, the method creates two new configuration fields called `stringToAppend` and `method`, and the default values `""` and `"NORMAL"` are assigned to it, respectively. All configuration fields that you create appear in the user interface and are configurable by the user. You can always access these values in the script, as we will do soon.

Next, we set a callback called `_data_in`, which is called every time the operator receives data in the inport `inString`. To set the callback, use the method `_set_port_callback` defined by the `BaseOperator` class.

```
def _get_operator_info(self):
    inports = [PortInfo("inString", required=True, type_="string")]
    outports = [PortInfo("outString", required=True, type_="string")]
    return OperatorInfo("Append String",
                        inports=inports,
                        outports=outports,
                        icon="puzzle-piece",
                        tags={"numpy36": "1.16.1"}
                        dollar_type="http://sap.com/vflow/com.mydomain.appendString.schema.json#")
```

All of the operators that you create in this way must always implement the `_get_operator_info` method. The `_get_operator_info` method is used to generate the operator json automatically, so you must specify the operator attributes here. To specify the operator attributes, the method must return an `OperatorInfo` object. The `OperatorInfo` object has the following attributes:

```
class OperatorInfo(object):
    """
    Attributes:
        description (str): Human readable name of the operator.
        icon (str): Icon name in font-awesome.
        iconsrc (str): Path to a icon image. Alternative to the option to a icon from font-awesome.
        inports (list[PortInfo]): List of input ports.
        outports (list[PortInfo]): List of output ports.
        tags (dict[str,str]): Tags for dependencies. dict[library_name, lib_version].
        component (str): This field will be set automatically.
        config (dict[string,any]): This field will be set automatically.
        dollar_type (str): Url to $type schema.json for this operator.
    """
```

You can specify all of the attributes using the `get_operator_info` method. In the example, we specify an input port called *inString* that receives a string, an output port called *outString* that also receives a string, the built-in icon *puzzle-piece* as the operator's icon, and *Append String* as operator description.The *inString* port name is used in the constructor to set the correct callback to the port.

```
def _init(self):
     metric_infos = []
    metric_infos.append(self._registry.create_metric_info(u'count', 1, u'name', u'display_name', u'unit'))
    self.metric = self.register_metric(u"int", u"TEST", metric_infos)

    self.register_websocket_route('/socket', 'test', self._set_websocket)
    self.register_static_route('/ui', 'static')
    self.register_rproxy_route('/rproxy/*path', 'http://localhost:' + str(self.config.port) + '/')
    
	if self.config.method == "NORMAL":
        self.__transform_data = lambda x: x
    elif self.config.method == "UPPERCASE":
        self.__transform_data = lambda x: x.upper()
    else:
        raise ValueError("Unknown config set in configuration: '%s'." % self.config.method)
```

The method is overridden by the `BaseOperator` superclass. The method is called after the user-defined configurations have already been set. The method is called for all graph operators before any operator has been started. Here, we are deciding which `transform_data` function to use based on the `self.config.method` parameter set by the user in the interface. In this method, the user can register metrics \(\`register\_metric\`\) and routes \(\`register\_websocket\_route\`, \`register\_static\_route\` and \`register\_rproxy\_route\`\). It is only possible to register these functionalities using the following function:

```
def _data_in(self, data):
                 self.metric.include_value(1)
                 self._send_message('outString', self.__transform_data(data + self.config.stringToAppend))
```

The function is the callback that we create to handle inputs to the *inString* input port. Here, we append the input data with our `stringToAppend` configuration field, apply the function `` to it, and use the `BaseOperator` `_send_message` method to send the result to our output port *outString*. In addition, we set a new value in the `self.metric` value, because the only `MetricInfo` is of type `cound`, we update the counter of processed strings.

```
def _set_websocket(self, handler):
 self.web_handler = handler
 self.web_handler.set_message_callback(self._on_message)

def _on_message(self, message):
 self.web_handler.write_message(str(message))
 self._send_message("outString", message)

```

The method is overridden by the `BaseOperator` superclass. It contains code that is executed before the operator main loop is started:

```
def _prestart(self):
    pass
```

The method is overridden by the `BaseOperator` superclass. It contains code that is executed after the operator main loop is finished:

```
def shutdown(self):
    pass
```

A list of all methods is available at [List of BaseOperator Methods](list-of-baseoperator-methods-542e31e.md).



## Create an Operator

After you implement the `operator.py` file to define the operator, run a bash script to create the operator.

To create an operator, create a folder \(or a series of folders\) inside the `<ROOT>/subengines/com/sap/python36/operators/` directory, where `<ROOT>` is `my_solution/vrep/vflow` in the example structure. For example, to create an operator with the ID `com.mydomain.util.appendString`, create the folders for the path `<ROOT>/subengines/com/sap/python36/operators/com/mydomain/util/appendString` and place two files inside the last directory: `operator.py` and `operator.json`. To automatically generate the `operator.json` file, run the script `gen_operator_jsons.py`, which is located inside the pysix\_subengine package.

The following bash script shows how you can use `gen_operator_jsons.py` in your solution:

```
SCRIPT_PATH=<PYSIX_SUBENGINE_PATH>/scripts
SUBENGINE_ROOT=<ROOT>/subengines/com/sap/python36
START_DIR=operators
python $SCRIPT_PATH/gen_operator_jsons.py --subengine-root $SUBENGINE_ROOT --start-dir $START_DIR "$@"
```



After you create an operator, restart the Modeler instance for the changes to take effect.

-   **[Using Python Library](using-python-library-4931050.md "")**  

-   **[Adding Documentation](adding-documentation-8bf1b93.md "")**  

-   **[Creating Tests](creating-tests-43db62e.md "When you create a new operator extending BaseOperator, you can
        also create unit tests using the Python unit testing framework.")**  
When you create a new operator extending *BaseOperator*, you can also create unit tests using the Python unit testing framework.
-   **[List of BaseOperator Methods](list-of-baseoperator-methods-542e31e.md "When subclassing BaseOperator, you will need to use a set of
		methods to set callbacks, send messages, etc. The list below summarizes the
			BaseOperator methods you might need.")**  
When subclassing *BaseOperator*, you will need to use a set of methods to set callbacks, send messages, etc. The list below summarizes the *BaseOperator* methods you might need.
-   **[List of BaseOperator Attributes](list-of-baseoperator-attributes-8d84d3f.md "")**  

-   **[List of Metric Methods](list-of-metric-methods-b5ad083.md "")**  

-   **[Logging](logging-603c6d6.md "There are a set of built-in methods to enable logging in the Python subengine. The table
		below summarizes the set of methods you can use to log information.")**  
There are a set of built-in methods to enable logging in the Python subengine. The table below summarizes the set of methods you can use to log information.
-   **[Uploading to SAP Data Intelligence System Management](uploading-to-sap-data-intelligence-system-management-bc4b7f3.md "You can either upload your solution to the SAP Data Intelligence cluster as a
		new solution (need to be logged as an admin) or you can upload your solution into your tenant or user workspace.")**  
You can either upload your solution to the SAP Data Intelligence cluster as a new solution \(need to be logged as an admin\) or you can upload your solution into your tenant or user workspace.

