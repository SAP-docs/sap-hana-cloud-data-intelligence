<!-- loioce221483e6584583bba61cfa2994ed2f -->

# Setting Values for Configuration Properties

You set the configuration properties at the operator level and each property is associated with a default value.

If you have provided new values to the properties through the user interface of the Modeler application, then the main engine sends the value to the subengine, when you execute the graph. To set an operator configuration property along with its default value, use the `v2_operator_config_add_<type>` set of functions.

Using the `v2_process_t` handle, which is first obtained in the `init` handler of that operator, you can query the actual values for each property by calling the `v2_process_config_get_<type>` functions.

If the defined value for a property does not correspond to its declared value, the engine throws an error for the type mismatch. The only exception is for `double` configurations that can receive an integer value by implicitly converting it to `double` .

