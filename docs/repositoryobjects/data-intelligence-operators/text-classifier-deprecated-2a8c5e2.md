<!-- loio2a8c5e2f65be476d9218b6732b561bc9 -->

# Text Classifier \(Deprecated\)

This is a pre-trained text classification service.



> ### Note:  
> This operator is deprecated. Please check SAP Note [2739161](https://me.sap.com/notes/2739161) for more information.



The model for the classifier was obtained by training on approximately 300,000 Icecat product texts. The classifier chooses from the following set of 50 categories: all-in-one PCs workstations, LED TVs, NAS and storage servers, PC workstations, USB cables, USB flash drives, antivirus security software, cable interface gender adapters, computer monitors, digital cameras, fiber optic cables, flat panel spare parts, graphics cards, ink cartridges, internal hard drives, keyboards, laser LED printers, laser toner and cartridges, memory modules, mice, mobile phone cases, motherboards, mounting kits, multifunctionals, network switches, networking cables, networking cards, notebook cases, notebook spare parts, notebooks, other, power adapters and inverters, power cables, printer kits, printer scanner spare parts, processors, projection screens, projector mounts, rechargeable batteries, screen protectors, servers, smartphones, software licenses upgrades, solid state drives, tablet cases, tablets, thin clients, uninterruptible power supplies, warranty and support extensions, washing machines.



<a name="loio2a8c5e2f65be476d9218b6732b561bc9__section_zgh_xbg_b3b"/>

## Input


<table>
<tr>
<th valign="top">

Parameter

</th>
<th valign="top">

Type

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

input

</td>
<td valign="top">

message

</td>
<td valign="top">

A message whose body is the string to be classified. The header is not required as there are no configuration parameters.

</td>
</tr>
</table>

**Example of input message**


<table>
<tr>
<th valign="top">

header

</th>
<th valign="top">

body

</th>
</tr>
<tr>
<td valign="top">

\{\}

</td>
<td valign="top">

"15 inch lenovo laptop"

</td>
</tr>
</table>

For example, you could use a JS operator, enter the following script to define the input text, and wire this operator to the Functional Service operator:

```
$.addGenerator(gen)

function gen(ctx) {

    var msg = {};
    msg.Body = "15 inch lenovo laptop"
    $.output(msg)
}
```



<a name="loio2a8c5e2f65be476d9218b6732b561bc9__section_kdn_2cg_b3b"/>

## Output


<table>
<tr>
<th valign="top">

Output

</th>
<th valign="top">

Type

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

output

</td>
<td valign="top">

message

</td>
<td valign="top">

The inference result as a JSON string. All 50 categories or labels are listed together with their predicted probability, ordered by descending probability.

</td>
</tr>
</table>

Example:

```
{
  "id": "f09a0cfd-e1bc-4740-5e56-919a94a56d5a",
  "predictions": [
    {
      "results": [
        {
          "label": "notebooks",
          "score": 0.71404
        },
        {
          "label": "digital cameras",
          "score": 0.02382
        },...
      ]
    }
  ],
  "processedTime": "2017-09-29T13:38:27.729971",
  "status": "DONE"
}
```

**Error**: If an error happens due to an input, this port outputs a message. If this port is not connected, a failure will stop the graph with an error.

**Related Information**  


[Text Classification](text-classification-21c882a.md "")

