<!-- loio28a448b0a81a422ebc92269e879f2b72 -->

# Port Data

Port types are not known at compile time. The subengine uses the handle, `v2_datum_t` to carry the generic inputs and outputs between the operators. The `v2_datum_t` handle is a reference-counted handle to an underlying piece of data.

Also, because this is a pure C API, you cannot use constructors and destructors to acquire and release these handles. Therefore, we recommend that you follow these guidelines:

-   If you get a datum as a parameter in the port handler, do not release it. The engine does that.
-   If you create a datum using the `v2_datum_create` set of functions, release it before it gets out of scope. Not releasing it may result in memory leaks. It is also important to release it even if you output the datum because this datum is going to be given to the next operator downstream, and the call to `v2_process_output` increases its reference count by one. This is similar to making a copy of a `std::shared_ptr`.

    > ### Tip:  
    > You can explicitly increase reference count of datum by calling `v2_datum_acquire`. This increase can be useful if you want to store a datum given to a port handler. But, do not forget to release it later.




<a name="loio28a448b0a81a422ebc92269e879f2b72__section_ftx_hzq_zcb"/>

## Data Types

A datum may contain any one of the following types:


<table>
<tr>
<th valign="top">

Modeler type

</th>
<th valign="top">

C type

</th>
<th valign="top">

ID `( v2_type_t )` 

</th>
<th valign="top">

Size \(bytes\)

</th>
</tr>
<tr>
<td valign="top">

`string` 

</td>
<td valign="top">

`char*` 

</td>
<td valign="top">

`V2_TYPE_STRING` 

</td>
<td valign="top">

Length of the string

</td>
</tr>
<tr>
<td valign="top">

`int64` 

</td>
<td valign="top">

`int64_t` 

</td>
<td valign="top">

`V2_TYPE_INT64` 

</td>
<td valign="top">

8

</td>
</tr>
<tr>
<td valign="top">

`float64` 

</td>
<td valign="top">

`double` 

</td>
<td valign="top">

`V2_TYPE_DOUBLE` 

</td>
<td valign="top">

8

</td>
</tr>
<tr>
<td valign="top">

`blob` 

</td>
<td valign="top">

`blob` 

</td>
<td valign="top">

`V2_TYPE_BLOB` 

</td>
<td valign="top">

Size of the blob

</td>
</tr>
<tr>
<td valign="top">

`uint64` 

</td>
<td valign="top">

`uint64_t` 

</td>
<td valign="top">

`V2_TYPE_UINT64` 

</td>
<td valign="top">

8

</td>
</tr>
<tr>
<td valign="top">

`message` 

</td>
<td valign="top">

`v2_message_t` 

</td>
<td valign="top">

`V2_TYPE_MESSAGE` 

</td>
<td valign="top">

0 \(Size of a message is only known when it is serialized, so it cannot be queried\).

</td>
</tr>
<tr>
<td valign="top">

`byte` 

</td>
<td valign="top">

`char` 

</td>
<td valign="top">

`V2_TYPE_BYTE` 

</td>
<td valign="top">

1

</td>
</tr>
<tr>
<td valign="top">

User-defined data types

</td>
<td valign="top">

`void`\*

</td>
<td valign="top">

`V2_TYPE_CUSTOM` 

</td>
<td valign="top">

0 \(Engine does not know the size of user-defined data types.\)

</td>
</tr>
</table>

For each data type, the ID column in the table shows the return value of `v2_datum_get_type`. This allows you to have generic operators \(for example, ports with type `any`\) that can check their input type at runtime.

The Size column in the table shows the return value of `v2_datum_get_size`.

> ### Restriction:  
> Array types are not supported in the current version.



<a name="loio28a448b0a81a422ebc92269e879f2b72__section_xcg_h1r_zcb"/>

## Ownership

Whenever the reference count of datum reaches zero, the engine deallocates the memory that belongs to the datum. For `string`, `blob`, `message`, and custom types this behavior can have one further consequence: whether or not to free the memory associated with the data itself. So, when creating a datum from one of those types, you can choose whether or not you want it to own the data:

-   A nonowning datum is created using the `v2_datum_from_<type>` functions, which do not deallocate the given data pointer. Thus, ensure that the functions remain available throughout the lifetime of the datum. This behavior is typical of static lifetime variables. For example:

    ```
    const char* YES = "yes";
    const char* NO  = "no";
    
    // A port handler
    const char* is_even_input( v2_process_t proc, v2_datum_t datum )
    {
      int64_t i = v2_datum_get_int64( datum );
      v2_datum_t out;
      if ( i % 2 ) // not even
        out = v2_datum_from_string( NO, 2 );
      else
        out = v2_datum_from_string( YES, 3 );
      v2_process_output( proc, "outEven", out );
      // Release local handle
      v2_datum_release( out );
      return NULL;
    }
    ```

-   An owning datum is created using the `v2_datum_own_<type>` functions. These functions take not only the pointer to the data, but also a "destructor" function pointer, which will be invoked with the data pointer as the argument. For example, an operator that concatenates the strings it receives two by two:

    ```
    // Port handler
    const char* concat_on_input( v2_process_t proc, v2_datum_t datum )
    {
      v2_datum_t previous = (v2_datum_t)v2_process_get_user_data( proc );
    
      if ( previous == NULL ) {
        // Store this datum for later use
        v2_process_set_user_data( proc, datum );
        // Let the engine know we've just stored an additional
        // reference to this datum
        v2_datum_acquire( datum );
      } else {
        char*    prev_str  = v2_datum_get_string( previous );
        uint64_t prev_size = v2_datum_get_size( previous );
    
        char*    curr_str  = v2_datum_get_string( datum );
        uint64_t curr_size = v2_datum_get_size( datum );
    
        // Allocate enough memory for both strings together. Null-terminating it
        // is optional, since we provide its length to v2_datum_own_string.
        uint64_t out_size = prev_size + curr_size;
        char* out_string = (char*)malloc( out_size );
        // Copy them to out_string
        strncpy( out_string, prev_str, prev_size );
        strncpy( out_string + prev_size, curr_str, curr_size );
    
        // Since out_string is on the heap, we need an owning datum
        // so it will call `free` on the string once its done.
        v2_datum_t out = v2_datum_own_string( out_string, out_size, free );
        v2_process_output( proc, "output", out );
        // Cleanup
        v2_datum_release( out );
        v2_datum_release( previous );
        v2_process_set_user_data( proc, NULL );
      }
    
      return NULL;
    }
    ```


> ### Note:  
> The datum never makes a copy of the data you provide regardless of the ownership. It only stores the given pointer.

> ### Note:  
> Both datum constructors for type string require the length of the string as a parameter. This requirement not only ensures safety \(if the string is not null-terminated, buffer overruns might occur\), but also enables different datum objects to point to different substrings of the same string without making any copies.



<a name="loio28a448b0a81a422ebc92269e879f2b72__section_om3_cbr_zcb"/>

## User-defined Types

Declare the Modeler name for a user-defined types in the `meta.json` file that is under the root directory of the subengine. Typically, `it is <repo-root>/subengines/<sub-engine-id>/meta.json`.

For example, if you are creating image-processing operators, you may want to define your own "image" type. This user-defined type helps the data to flow among such operators without having to conform to the standard types in the modeler. In this example, your `meta.json` might look like this:

```
{
  "versions": ["1.0"],
  "types": ["image"]
}
```

Adding a type to `meta.json` enables the main engine to recognize its existence and accept graphs that use these types as valid.

> ### Remember:  
> The underlying structure of this type is completely unknown to both the main engine and the subengine. Thus, you cannot convey user-defined types between two operators pertaining to different subengines.

