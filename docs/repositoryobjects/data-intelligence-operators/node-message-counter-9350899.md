<!-- loio9350899de3e84f50b7f952ba187b9bd3 -->

# Node Message Counter

The Node Message Counter operator implements a message counter using Node.js. You can adapt it to your own wishes.



## How the Counter Works

The example script counts the number of message on the input port and sends the number down the output port.

```
const SDK = require("@sap/vflow-sub-node-sdk");
const operator = SDK.Operator.getInstance();
let counter = 0;

/**
 * Receives messages on port "in1",
 * increases a counter and forwards the counter value
 * to port "out1".
 */
operator.getInPort("in1").onMessage((msg) => {
  // The content of the actual message is ignored.
  // We will only count the number of messages here.
  counter++;
  operator.getOutPort("out1")
    .send(counter.toString());
});

/**
 * A keep alive hook for the node process.
 * (Operator shutdown is built in to the SDK)
 * @param tick length of a heart beat
 */
function keepAlive(tick) {
  setTimeout(() => {
    keepAlive(tick);
  }, tick);
}

// Here we keep the operator alive in 2sec ticks
keepAlive(1000);

// You can add a shutdown handler if there is something to clean up.
// const handler = (cb: (err?: Error) => void): void => {
//      do something …
//  cb(…); // callback with void or an error
// };
// operator.addShutdownHandler(handler);

```



<a name="loio9350899de3e84f50b7f952ba187b9bd3__section_lqc_y4w_n4b"/>

## Configuration Parameters

None.



<a name="loio9350899de3e84f50b7f952ba187b9bd3__section_tb5_z4w_n4b"/>

## Input


<table>
<tr>
<th valign="top">

Input

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

in1

</td>
<td valign="top">

string

</td>
<td valign="top">

The incoming data.

</td>
</tr>
</table>



<a name="loio9350899de3e84f50b7f952ba187b9bd3__section_whg_fpw_n4b"/>

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

out1

</td>
<td valign="top">

string

</td>
<td valign="top">

The number of messages since start as a string.

</td>
</tr>
</table>

