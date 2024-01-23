<!-- loio9b6f3b037d884a7fad37ebeba2cba15e -->

# subengine.h

Establishes the core set of functions for the subengine interface.



<a name="loio9b6f3b037d884a7fad37ebeba2cba15e__section_ocf_frg_fdb"/>

## Macros

`#define V2_TYPE_ARRAY 0x0B`

`#define V2_TYPE_BLOB 0x03`

`#define V2_TYPE_BOOL 0x08`

`#define V2_TYPE_CUSTOM 0x07`

`#define V2_TYPE_DOUBLE 0x02`

`#define V2_TYPE_INT64 0x01`

`#define V2_TYPE_MAP 0x0A`

`#define V2_TYPE_MESSAGE 0x05`

`#define V2_TYPE_NULL 0x09`

`#define V2_TYPE_STRING 0x00`

`#define V2_TYPE_UINT64 0x04`



<a name="loio9b6f3b037d884a7fad37ebeba2cba15e__section_ct1_grg_fdb"/>

## Typedef


<table>
<tr>
<th valign="top">

Typedef

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

`typedef void* v2_context_t` 

</td>
<td valign="top">

Handle to the internal data that the engine may need to relay from the init\(\) function to some other with the help from the plugin .

</td>
</tr>
<tr>
<td valign="top">

`typedef struct v2_datum* v2_datum_t` 

</td>
<td valign="top">

Handle to a piece of data exchanged between two ports.

> ### Note:  
> A datum can hold any of the types known to the engine or a pointer to a user-defined type. In the latter, the datum should not cross the subengine boundaries, as there is no guarantee that other subengines or the main engine will recognize this type.



</td>
</tr>
<tr>
<td valign="top">

`typedef void* v2_map_t` 

</td>
<td valign="top">

Handle to a JSON-like object, which is a mapping of `const char*` keys to `v2_value_t`.

</td>
</tr>
<tr>
<td valign="top">

`typedef void* v2_message_t` 

</td>
<td valign="top">

Handle to a message, when the data type transferred between ports of type "`message`".

</td>
</tr>
<tr>
<td valign="top">

`typedef void* v2_process_t` 

</td>
<td valign="top">

Handle to a process \(a running instance of an operator\), which is created internally by the engine and supplied to the plugin in a call to the init handler of the operator.

</td>
</tr>
<tr>
<td valign="top">

`typedef void* v2_value_t` 

</td>
<td valign="top">

Handle to a JSON-like value.

This can contain one of the following:

-   string \(`const char*`\)
-   integer \(`int64_t`\)
-   decimal \(`double`\)
-   byte \(`char`\)
-   null \(see v2\_value\_is\_null\(\)\)
-   object \(`v2_map_t`\)
-   array \(`v2_array_t`\)



</td>
</tr>
</table>



<a name="loio9b6f3b037d884a7fad37ebeba2cba15e__section_tmd_hrg_fdb"/>

## Functions

-   **`V2_EXPORT v2_datum_t v2_datum_acquire (v2_datum_t datum)`**

    *Use:*

    Notifies that a new handle to `datum` is being held, incrementing its \(handle\) internal reference counter.

    *Description:*

    If `datum` were an `std::shared_ptr`, this function would be analogous to the copy constructor.

    *Returns*

    `datum` 

    > ### Note:  
    > Every call to acquire must be paired with a call to release. If it is not paired, the memory for the datum will be leaked.

-   **`V2_EXPORT v2_datum_t v2_datum_copy (v2_datum_t datum)`**

    *Use:*

    Creates a new datum that contains a copy of the value of the `datum`.

    *Description:*

    If `datum` contains a string, blob, or message, a deep copy will be made and the resulting datum will own this copy.

    If `datum` contains custom data, this function will raise an error. To make a copy of a custom type:

    ```
    void* ptr = v2_datum_get_custom( my_datum );
    void* ptr_copy = copy_my_type( (my_type*)ptr );
    v2_datum_t my_datum_copy = v2_datum_own_custom( ptr_copy, free_my_type );
    ```

    Here, it is assumed that `copy_my_type` allocates a new `my_type` value that can later be deallocated with `free_my_type`.

    > ### Remember:  
    > Release the returned datum \(even if it was outputted\) once you are done with it. See, v2\_datum\_release\(\).

-   **`V2_EXPORT v2_datum_t v2_datum_from_blob (void * buf, uint64_t size )`**

    *Use:*

    Creates a nonowning datum that refers to an existing blob.

    *Description:*

    The blob will not be copied and will not be deallocated when the datum is destroyed.

    > ### Remember:  
    > Release the returned datum \(even if it was outputted\) once you are done with it. See, v2\_datum\_release\(\).

-   **`V2_EXPORT v2_datum_t v2_datum_from_byte (char b)`**

    *Use:*

    Creates a datum containing a byte.

    > ### Remember:  
    > Release the returned datum \(even if it was outputted\) once you are done with it. See, v2\_datum\_release\(\).

-   **`V2_EXPORT v2_datum_t v2_datum_from_custom (void * ptr)`**

    *Use:*

    Creates a nonowning datum that refers to a user-defined area in the memory.

    *Description:*

    The contents of this area will not be copied and the area will not be deallocated when the datum is destroyed.

    > ### Remember:  
    > Release the returned datum \(even if it was outputted\) once you are done with it. See, v2\_datum\_release\(\).

-   **`V2_EXPORT v2_datum_t v2_datum_from_double (double d)`**

    *Use:*

    Creates a datum containing a `double`.

    > ### Remember:  
    > Release the returned datum \(even if it was outputted\) once you are done with it. See, v2\_datum\_release\(\).

-   **`V2_EXPORT v2_datum_t v2_datum_from_int64 (int64_t i)`**

    *Use:*

    Creates a datum containing an `int64_t`.

    > ### Remember:  
    > Release the returned datum \(even if it was outputted\) once you are done with it. See, v2\_datum\_release\(\).

-   **`V2_EXPORT v2_datum_t v2_datum_from_message (v2_message_t message)`**

    *Use:*

    Creates a nonowning datum that refers to an existing message.

    *Description:*

    The message will not be copied and will not be deallocated when the datum is destroyed.

    > ### Remember:  
    > Release the returned datum \(even if it was outputted\) once you are done with it. See, v2\_datum\_release\(\).

-   **`V2_EXPORT v2_datum_t v2_datum_from_string (char * s, uint64_t size)`**

    *Use:*

    Creates a nonowning datum that refers to an existing string.

    *Description:*

    The string will not be copied and it will not be deallocated when the datum is destroyed.

    *Parameters*

    `[in] s`: pointer to the start of the string

    `[in] size`: the size of the string in bytes, excluding the terminating null byte

    > ### Remember:  
    > Release the returned datum \(even if it was outputted\) once you are done with it. See, v2\_datum\_release\(\).

-   **`V2_EXPORT v2_datum_t v2_datum_from_uint64 (uint64_t u)`**

    *Use:*

    Creates a datum containing a `uint64_t`.

    > ### Remember:  
    > Release the returned datum \(even if it was outputted\) once you are done with it. See, v2\_datum\_release\(\).

-   **`V2_EXPORT void* v2_datum_get_blob (v2_datum_t datum)`**

    *Use:*

    Returns `datum` as a blob.

    *Description:*

    This function will not check if the contained data is a blob \(see, v2\_datum\_get\_type\(\)\). Also, you can use v2\_datum\_get\_size\(\) to get the size of the blob.

-   **`V2_EXPORT char* v2_datum_get_byte (v2_datum_t datum)`**

    *Use:*

    Returns `datum` as a byte.

    *Description:*

    This function will not check if the contained data is a byte \(see, v2\_datum\_get\_type\(\)\).

-   **`V2_EXPORT void* v2_datum_get_custom (v2_datum_t datum)`**

    *Use:*

    Returns `datum` as custom data.

    *Description:*

    This function will not check if the contained data is a custom pointer \(see, v2\_datum\_get\_type\(\)\).

-   **`V2_EXPORT double* v2_datum_get_double (v2_datum_t datum)`**

    *Use:*

    Returns `datum` as a `double`.

    *Description:*

    This function will not check if the contained data is a `double` \(see, v2\_datum\_get\_type\(\)\).

-   **`V2_EXPORT int64_t* v2_datum_get_int64 (v2_datum_t datum)`**

    *Use:*

    Returns `datum` as an `int64_t`.

    *Description:*

    This function will not check if the contained data is an `int64_t` \(see, v2\_datum\_get\_type\(\)\).

-   **`V2_EXPORT v2_message_t v2_datum_get_message (v2_datum_t datum)`**

    *Use:*

    Returns `datum` as a message.

    *Description:*

    This function will not check if the contained data is a message \(see, v2\_datum\_get\_type\(\)\).

-   **`V2_EXPORT uint64_t v2_datum_get_size (v2_datum_t datum)`**

    *Use:*

    Returns the size in bytes of the data held by the datum.

    *Description:*

    The return value for each contained type is:

    -   `V2_TYPE_STRING`: the length of the string in bytes, excluding the terminating null byte.
    -   `V2_TYPE_INT64`: 8
    -   `V2_TYPE_DOUBLE`: 8
    -   `V2_TYPE_BLOB`: the size of the blob in bytes.
    -   `V2_TYPE_UINT64`: 8
    -   `V2_TYPE_MESSAGE`: 0 \(only known when the message is serialized\)
    -   `V2_TYPE_BYTE`: 1
    -   `V2_TYPE_CUSTOM`: 0 \(not known by the engine\)

-   **`V2_EXPORT char* v2_datum_get_string (v2_datum_t datum)`**

    *Use:*

    Returns `datum` as a null-terminated string.

    *Description:*

    This function will not check if the contained data is a string \(see, `v2_datum_get_type()`\). Also, you can use `v2_datum_get_size()` to get the size of the string \(not including the terminating null byte\).

-   **`V2_EXPORT v2_type_t v2_datum_get_type (v2_datum_t datum)`**

    *Use:*

    Returns a `v2_type_t` constant that describes the type held by `datum`.

    *Description:*

    The possible values are:

    -   `V2_TYPE_STRING`
    -   `V2_TYPE_INT64`
    -   `V2_TYPE_DOUBLE`
    -   `V2_TYPE_BLOB`
    -   `V2_TYPE_UINT64`
    -   `V2_TYPE_MESSAGE`
    -   `V2_TYPE_BYTE`
    -   `V2_TYPE_CUSTOM`

-   **`V2_EXPORT uint64_t* v2_datum_get_uint64 (v2_datum_t datum)`**

    *Use:*

    Returns `datum` as a `uint64_t`.

    *Description:*

    This function will not check if the contained data is a `uint64_t` \(see, `v2_datum_get_type()`\).

-   **`V2_EXPORT v2_datum_t v2_datum_own_blob (void * buf, uint64_t size, v2_destructor_t destructor)`**

    *Use:*

    Creates a datum that takes ownership of an existing blob.

    *Description:*

    The blob is not copied, and it will be deallocated when the data is destroyed by calling `destructor(s)`.

    > ### Remember:  
    > Release the returned datum \(even if it was outputted\) once you are done with it. See, v2\_datum\_release\(\).

-   **`V2_EXPORT v2_datum_t v2_datum_own_custom (void * ptr, v2_destructor_t destructor)`**

    *Use:*

    Creates a datum that takes ownership of a user-defined area in the memory.

    *Description:*

    The contents of this area will not be copied, and the area will be deallocated when the data is destroyed by calling `destructor(s)`.

    > ### Remember:  
    > Release the returned datum \(even if it was outputted\) once you are done with it. See, v2\_datum\_release\(\).

-   **`V2_EXPORT v2_datum_t v2_datum_own_message (v2_message_t message)`**

    *Use:*

    Creates a datum that takes ownership of an existing message.

    *Description:*

    The message will not be copied, and the message will be deallocated when the data is destroyed by calling `destructor(s)`.

    > ### Remember:  
    > Release the returned datum \(even if it was outputted\) once you are done with it. See, v2\_datum\_release\(\).

-   **`V2_EXPORT v2_datum_t v2_datum_own_string (char * s, uint64_t size, v2_destructor_t destructor)`**

    *Use:*

    Creates a datum that takes ownership of an existing string.

    *Description:*

    The string will not be copied, and the string will be deallocated when the data is destroyed by calling `destructor(s)`.

    > ### Remember:  
    > Release the returned datum \(even if it was outputted\) once you are done with it. See, v2\_datum\_release\(\).

-   **`V2_EXPORT void v2_datum_release (v2_datum_t datum)`**

    *Use:*

    Notifies that the handle `datum` is being released.

    *Description:*

    After this call, it cannot be guaranteed that the actual data underlying the handle will be available. Therefore, you should no longer use `datum`. If `datum` were an `std::shared_ptr`, this function would be analogous to the destructor.

    > ### Note:  
    > Every call to `v2_datum_acquire, v2_datum_from_*, v2_datum_own_*`, or `v2_datum_copy` must be paired with a call to release, if not the memory for the datum will be leaked. If you output such a datum before releasing, the engine will ensure that it survives the call to release and that the downstream operators have access to it.

-   **`V2_EXPORT void v2_log_debug_string (const char * str)`**

    *Use:*

    Logs the debug information.

    *Description:*

    If either the main engine was run in debug mode, or if the subengine was forced into debug mode by the `run.sh` script, then this debug information will show up in the output of the main engine,

-   **`V2_EXPORT void v2_log_fatal_string (const char * str)`**

    *Use:*

    Logs a string as a fatal error that will cause the main engine to terminate the subengine, its graph, and processes.

-   **`V2_EXPORT void v2_message_destroy (v2_message_t msg)`**

    *Use:*

    Frees the memory associated with a message.

    *Description:*

    Call this function only if you obtained the message using `v2_message_create()`.

-   **`V2_EXPORT v2_value_t v2_message_get_attribute (v2_message_t msg, const char * key)`**

    *Use:*

    Returns the value associated to a message attribute.

    *Description:*

    This is a convenience for `v2_map_find( v2_message_get_attributes( msg ), key )`.

-   **`V2_EXPORT void v2_message_set_body (v2_message_t msg, v2_datum_t body)`**

    *Use:*

    Sets the message body by releasing the previous one \(if any\) and by calling `v2_datum_acquire( body )`.

-   **`V2_EXPORT void v2_operator_add_input (v2_operator_t op, const char * port_id, const char * port_type)`**

    *Use:*

    Adds an input port called `port_id` to `op`.

    *Description:*

    `port_type` is a null-terminated string describing the type accepted by the port. The possible port types are:

    -   "`string`"
    -   "`blob`"
    -   "`int64`"
    -   "`uint64`"
    -   "`float64`"
    -   "`message`"
    -   "`byte`"
    -   anything else will be regarded as a custom \(user-defined\) type, which can be conveyed between any two operators, provided they are both implemented by the same subengine.

-   **`V2_EXPORT void v2_operator_add_output (v2_operator_t op, const char * port_id, const char * port_type)`**

    *Use:*

    Adds an output port called `port_id``op`.

    *Description:*

    `port_type` will be treated as described in `v2_operator_add_input()`.

-   **`V2_EXPORT v2_array_t v2_operator_config_add_array (v2_operator_t op, const char * key)`**

    *Use:*

    Creates and returns a JSON array configuration value named `key` to `op`.

    *Description:*

    You can modify the returned array to customize the initial value for this property.

    > ### Caution:  
    > The array may be relocated in memory in a subsequent call to `v2_operator_config_add_*`. Thus, ensure you are modifying it immediately after obtaining it. Do not store the array for later use.

-   **`V2_EXPORT v2_map_t v2_operator_config_add_map (v2_operator_t op, const char * key)`**

    *Use:*

    Creates and returns a JSON object configuration value named `key` to `op`.

    *Description:*

    You can modify the returned map to customize the initial value for this property.

    > ### Note:  
    > The map may be relocated in memory in a subsequent call to `v2_operator_config_add_*`. Thus, ensure you are modifying it immediately after obtaining it. Do not store the array for later use.

-   **`V2_EXPORT void v2_operator_config_add_string (v2_operator_t op, const char * key, const char * default_value)`**

    *Use:*

    Adds a string configuration value named `key` to `op`.

    *Description:*

    `default_value` must be a null-terminated string containing the initial value for this property.

-   **`V2_EXPORT v2_operator_t v2_operator_create (v2_context_t ctx, const char * id, const char * name, v2_init_handler_t init)`**

    *Use:*

    Creates an operator.

    *Parameters*

    `[in] ctx`: the context handle supplied to the init\(\) function

    `[in] id`: the operator ID

    `[in] name`: the operator name, which will be visible on the GUI

    `[in] init`: the callback function that the engine will call when a process is instantiated from this operator.

    *Description:*

    The init handler can \(not necessarily in this order\):

    -   Access configuration values: use the `v2_process_get_config_*` set of functions to get the actual configuration values for your process. These values remain available throughout the lifetime of the processes, but the init handler is usually the first \(rarely\) place where they are read.
    -   Set input handlers: if your operator has input ports, the process is expected to set a handler for each of them \(see, `v2_process_set_port_handler()`\). It is not an error to leave a port unhandled, provided it is never connected. It is also possible to conditionally set input handlers depending on the configuration values.

        > ### Note:  
        > Connected ports that are unhandled results in an error and cause the engine to stop.

    -   Set the shutdown handler: if your operator needs to clean up after running. This callback will be invoked by the engine when the graph is stopped. This is also usually the place to release resources acquired in the init handler.

-   **`V2_EXPORT void v2_operator_set_visibility (v2_operator_t op, int visible)`**

    *Use:*

    Sets whether or not `op` should be visible.

    *Description:*

    Visible components have their JSON descriptions automatically generated by the subengine so that they show up on the user interface.

-   **`V2_EXPORT void v2_process_add_timed_handler (v2_process_t proc, const char * name, v2_timed_handler_t handler, uint64_t repeat, uint64_t interval_ms)`**

    *Use:*

    Adds a timed handler.

    *Parameters*

    `[in] proc`

    `[in] name`: an optional name for the handler \(for clearer logging\). It can be NULL or empty too. It does not have to be unique.

    `[in] handler`: the callback function

    `[in] repeat`: the number of times the handler is to be called, or zero for unlimited \(as long as the graph is running\).

    `[in] interval_ms` the period in milliseconds for the timer

-   **`V2_EXPORT double v2_process_config_get_double (v2_process_t proc, const char * key)`**

    *Use:*

    Returns the final value for a `double` configuration property.

    > ### Note:  
    > Properties originally declared with `v2_operator_config_add_int64()` can also be retrieved using this function. It automatically converts the integer to double.

-   **`V2_EXPORT v2_bool_t v2_process_config_is_null (v2_process_t proc, const char * key)`**

    *Use:*

    Returns whether the final value for a configuration property is the JSON keyword `null`.

-   **`V2_EXPORT const char* v2_process_get_id (v2_process_t proc)`**

    *Use:*

    Returns the process ID, which uniquely identifies it in the graph.

    > ### Remember:  
    > This is not the same as the operator ID.

-   **`V2_EXPORT void v2_process_output (v2_process_t proc, const char * port_id, v2_datum_t data)`**

    *Use:*

    Sends output to a port.

    *Description:*

    This call will block until the destination \(the process downstream\) is ready to consume.

-   **`V2_EXPORT void v2_process_set_port_handler (v2_process_t proc, const char * port_id, v2_port_handler_t handler)`**

    *Use:*

    Sets a callback function to be invoked when the input port named `port_id` receives data.

    *Description:*

    Calls to `handler` will be made sequentially, never concurrently. Successive calls to this function replace the currently set handler.

-   **`V2_EXPORT void v2_process_set_user_data (v2_process_t proc, void * data)`**

    *Use:*

    Stores a user-supplied pointer.

    *Description:*

    This function is useful if you need each instance of an operator to carry some individual information \(for example, a file descriptor, a connection object, and so on\). The initial value is `NULL`.

-   **`V2_EXPORT v2_array_t v2_value_get_array (v2_value_t v)`**

    *Use:*

    Returns the array contained in `v`.

    *Description:*

    If `v` does not contain an array, it will raise an error.

-   **`V2_EXPORT v2_bool_t v2_value_get_bool (v2_value_t v)`**

    *Use:*

    Returns the boolean contained in `v`.

    *Description:*

    If `v` does not contain a boolean, it will raise an error.

-   **`V2_EXPORT double v2_value_get_double (v2_value_t v)`**

    *Use:*

    Returns the decimal contained in `v`.

    *Description:*

    If `v` does not contain a decimal, it will raise an error.

-   **`V2_EXPORT int64_t v2_value_get_int64 (v2_value_t v)`**

    *Use:*

    Returns the integer contained in `v`.

    *Description:*

    If `v` does not contain an integer, it will raise an error.

-   **`V2_EXPORT v2_map_t v2_value_get_map (v2_value_t v)`**

    *Use:*

    Returns the object contained in `v`.

    *Description:*

    If `v` does not contain an object, it will raise an error.

-   **`V2_EXPORT const char* v2_value_get_string (v2_value_t v)`**

    *Use:*

    Returns the string contained in `v`.

    *Description:*

    If `v` does not contain a string, it will raise an error.

-   **`V2_EXPORT v2_type_t v2_value_get_type (v2_value_t v)`**

    *Use:*

    Returns the type contained in a JSON value.

    *Description:*

    The possible values are:

    -   `V2_TYPE_STRING`
    -   `V2_TYPE_INT64`
    -   `V2_TYPE_DOUBLE`
    -   `V2_TYPE_BOOL`
    -   `V2_TYPE_NULL`
    -   `V2_TYPE_MAP`
    -   `V2_TYPE_ARRAY`


