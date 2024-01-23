<!-- loio2a647f3e65454a1b9e0b66c393bed530 -->

# Operator Details

Every operator has an ID \(also known as name\) and a title \(also known as the description\). The operator ID is a unique identifier, with a strict format. The operator title is what the graphical interface displays.



<a name="loio2a647f3e65454a1b9e0b66c393bed530__section_vs3_qgy_rvb"/>

## Operator Extensions

All the operators available when creating a graph are known as extensions because they “extend” the base operators.

Base operators are visible when you create a new operator. The extension is expressed by a file in the Modeler file system. This file must be named `operator.json` and its folder hierarchy must match its ID. The Modeler names the file with the extension when you create the operator.

Example:

```
ID: 'com.sap.foo.bar'
Filepath: './operators/com/sap/foo/bar/operator.json'
```



<a name="loio2a647f3e65454a1b9e0b66c393bed530__section_rfn_1ml_f3b"/>

## Operator JSON

The `operator.json` file contains the operator definition, including the graphical interface information. It has the structure listed in the following table.


<table>
<tr>
<th valign="top">

Option

</th>
<th valign="top">

Required

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

`description`

</td>
<td valign="top">

No

</td>
<td valign="top">

The operator title.

</td>
</tr>
<tr>
<td valign="top">

`icon`

</td>
<td valign="top">

Yes

</td>
<td valign="top">

The operator icon, expressed as a Font Awesome icon name that is available at [https://fontawesome.com/icons/](https://fontawesome.com/icons/).

</td>
</tr>
<tr>
<td valign="top">

`iconsrc`

</td>
<td valign="top">

Yes

</td>
<td valign="top">

The path to the SVG icon file. The path is relative to the `operator.json`.

</td>
</tr>
<tr>
<td valign="top">

`component`

</td>
<td valign="top">

Yes

</td>
<td valign="top">

The base operator ID to be extended.

</td>
</tr>
<tr>
<td valign="top">

`inports`

</td>
<td valign="top">

No

</td>
<td valign="top">

An array of input ports.

</td>
</tr>
<tr>
<td valign="top">

`outports`

</td>
<td valign="top">

No

</td>
<td valign="top">

An array of output ports.

</td>
</tr>
<tr>
<td valign="top">

`config`

</td>
<td valign="top">

No

</td>
<td valign="top">

A map of configuration parameters that map a configuration parameter ID to its default value.

</td>
</tr>
<tr>
<td valign="top">

`config.$type`

</td>
<td valign="top">

Yes

</td>
<td valign="top">

A `$type` field that points to its schema.

</td>
</tr>
<tr>
<td valign="top">

`tags`

</td>
<td valign="top">

No

</td>
<td valign="top">

A map of tags that map each tag ID to its default value.

</td>
</tr>
<tr>
<td valign="top">

`enableportextension`

</td>
<td valign="top">

No

</td>
<td valign="top">

A Boolean value that, if set to `true`, allows adding additional ports and configurations to the operator through the UI.

</td>
</tr>
<tr>
<td valign="top">

`extensible`

</td>
<td valign="top">

No

</td>
<td valign="top">

A Boolean value that, if set to `true`, allows a base operator to be extended.

</td>
</tr>
</table>

> ### Note:  
> `subenginestags` don't exist in the file system. They're included on the operator JSON for UI purposes.
> 
> `icon` and `iconsrc` are mutually exclusive; any field can be derived from the base operator \(`component`\).

The `operator.json` results in the following structure:

```
{
    "description": "<operator-title>",
    "icon": "<fontawesome-icon>",
    "iconsrc":"<icon-file>",
    "component": "base-operator-id",
    "inports": [
        {
            "name": "<inport1-id>",
            "type": "<inport1-type>"
        },
        ...
    ],
    "outports": [
        {
            "name": "<outport1-id>",
            "type": "<outport1-type>"
        },
        ...
    ],
    "config": {
        "<config-id>": "<config-value>",
        ...
    },
    "tags": {
        "<tag-id>": "<tag-value>",
        ...
    },
    "enableportextension": <true/false>,
    "extensible": <true/false>,
}
```

> ### Example:  
> ```
> {
>     "iconsrc": "read.svg",
>     "component": "com.sap.storage.read",
>     "config": {
>         "$type": "http://sap.com/vflow/com.sap.storage.read.schema.json#"
>     },
>     "tags": {},
> }
> ```



<a name="loio2a647f3e65454a1b9e0b66c393bed530__section_zjz_vwl_f3b"/>

## Documentation

The operator documentation is a README file in markdown format. If the documentation makes sense only for the extension, the file must be named `README.md` and saved in the same folder as the `operator.json` file.

When you have multiple subengine implementations, where there are multiple `operator.json` files, each implementation must have a README in the same folder as the `operator.json` file.



### README structure

The following code shows the README file structure:

```
<operator-title>
===

<introduction>

<links-to-examples>

Configuration parameters
---

- <configuration-parameter-1>
- <configuration-parameter-2>
- ...

Input
---

- <input-port-1>
- <input-port-2>
- ...

Output
---

- <output-port-1>
- <output-port-2>
- ...
```

If an item list \(parameters or ports\) is empty, the word “None” must be listed.

> ### Example:  
> ```
> Configuration parameters
> ---
> 
> - None
> ```



### Introduction

The introduction text must have the following content:

```
- **configuration-id** 
    (type <configuration-type>, default: <configuration-default>) 
    <!-- mandatory: only if applicable --> mandatory:
    <!-- brief description --> Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
    <!-- if needed, link to document with further description -->
    (Details are described here)[<link-to-config-docs>].

    - ID: `<configuration-id>`
    - Type: `<configuration-type>`
    <!-- Default: a value must be expressed according to its type formatting,
        e.g.:
            string -> `"value"`,
            int -> `42`,
            object -> `{ "k": ["v1, "v2"] }`,
            ...
    -->
    - Default: `<default-configuration-value>`
    <!-- Possible values: only valid for "enum" type -->
    - Possible values:
        - `<value-1>`
        - `<value-2>`
    <!-- Expected input: only valid when the "pattern" is set -->
    - Expected input: `<pattern-regex>`
    <!-- Additional specification fields may be provided -->
```

The Connection Protocol is mandatory and must have the following protocol in the request to service:

-   ID: connProtocol

-   Type: string

-   Default: "HTTP"

-   Possible values:

    -   `"HTTP"`

    -   `"HTTPS"`





### Ports

Ports are identified by a unique ID \(name\). Ports are formatted as follows:

```
- **<port-id>** (type <port-type>): Express the parameter.
    If further is needed, document it in a separate file, and [link]()
    to it in this sentence. External documentation may be linked.
```



<a name="loio2a647f3e65454a1b9e0b66c393bed530__section_q5j_sxl_f3b"/>

## Configuration Schema

When you name parameters, use the same standard you use to name operators.

You must provide a schema for a configuration. The schema contains parameters and further constraints for the UI. You must link a configuration schema in the `operator.json` file as follows:

```
{
    ...
    "config": {
        "$type": "<$id-from-schema>"
    },
}
```

Each parameter in the schema must meet the following criteria:

-   Point to its ID with the object's key.

-   Have a set title.

-   Use the most strict type.

-   Have a validation regex in pattern, if applicable.

-   Be listed as required, if applicable.


Ether write the schema manually or with the help of the *Types* panel of the Modeler application. Save the schema in one of the following ways:

-   As `configSchema.json` in the same `operator.json` folder.

    Consider this method first, and when you use the Modeler application to create.

-   As `schema.json` in the `/types/<operator-id>/schema.json` directory.

> ### Example:  
> The following code shows a brief example of a configuration schema:
> 
> ```
> {
>     "$schema": "http://json-schema.org/draft-06/schema#",
>     "$id": "http://sap.com/vflow/<operator.id>.schema.json",
>     "title": "<schema-title>",
>     "description": "<schema-description>",
>     "type": "object",
>     "properties": {
>         "user": {
>         "title": "User",
>         "type": "string",
>         "secure": true
>         },
>         "password": {
>         "title": "Password",
>         "type": "string",
>         "secure": true,
>         "format": "password"
>         },
>         "fooConnectionID": {
>             "title": "Foo Connection ID",
>             "description": "Connection ID used to connected to Foo",
>             "type": "string",
>             "format": "com.sap.dh.connection.id"
>         },
>         "isFoo": {
>             "title": "Is Foo",
>             "type": "boolean",
>             "description": "Determines if operator is Foo.",
>         },
>         "reqMode": {
>             "title": "Request Mode",
>             "type": "string",
>             "enum": [
>                 "Foo",
>                 "Bar"
>             ]
>         },
>         "noOfReqs": {
>             "title": "Number of Requests",
>             "type": "integer",
>             "description": "Number of Bar requests to be done.",
>             "sap_vflow_constraints": {
>                 "ui_visibility": [
>                     {
>                         "name": "reqMode",
>                         "value": "Bar"
>                     }
>                 ]
>             }
>         },
>         "filepath": {
>             "title": "File path",
>             "type": "string",
>             "description": "File path to save request. Must start with '/'.",
>             "pattern": "^\/.*$"
>         }
>     }
> }
> ```



<a name="loio2a647f3e65454a1b9e0b66c393bed530__section_dqm_gyl_f3b"/>

## Schema Types

The following are the available types for a configuration parameter:

-   `"array"`
-   `"boolean"`
-   `"integer"`
-   `"number"`
-   `"object"`
-   `"string"`

