<!-- loiod2b70358942743fa88a69683d5384dc3 -->

# Node Data Generator

The Node Data Generator operator mimics an IoT device and provides random data sets.



The random data sets are of the following form:

```
const generateData = () => {
  const deviceID = rndInteger({min: 2, max: 6});
  const temperature = rndFloat({min: 25, max: 26, fixed: 1});
  const humidity = rndFloat({min: 40, max: 60, fixed: 1});
  const co2 = rndFloat({min: 500, max: 600, fixed: 1});
  const co = rndFloat({min: 0.9, max: 1.1, fixed: 1});
  const lpg = rndFloat({min: 23, max: 25, fixed: 1});
  const smoke = rndFloat({min: 50, max: 60, fixed: 1});
  const presence = rndInteger({min: 0, max: 1});
  const light = rndFloat({min: 600, max: 800, fixed: 2});
  const sound = rndFloat({min: 400, max: 500, fixed: 2});
  return `${deviceID}, ${temperature}, ${humidity}, ${co2}, ${co}, ${lpg}, ${smoke}, ${presence}, ${light}, ${sound}`;
};
```

You can modify to your own wishes.



<a name="loiod2b70358942743fa88a69683d5384dc3__section_sqt_54q_n4b"/>

## Configuration Parameters

None.



<a name="loiod2b70358942743fa88a69683d5384dc3__section_xgk_w4q_n4b"/>

## Input

None.



<a name="loiod2b70358942743fa88a69683d5384dc3__section_gqj_x4q_n4b"/>

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

data\_out1

</td>
<td valign="top">

string

</td>
<td valign="top">

A string containing the comma separated random data.

</td>
</tr>
</table>

