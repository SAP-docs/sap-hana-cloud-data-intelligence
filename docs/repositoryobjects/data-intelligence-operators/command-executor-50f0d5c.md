<!-- loio50f0d5c1928d44d9947e55db828c8b51 -->

# Command Executor

The Command Executor operator executes the given command for each arrival of a message on the stdin port. The arriving message is provided on standard input. The complete standard error and standard output of the command is available on stderr and stdout respectively after completion of the command.



<a name="loio50f0d5c1928d44d9947e55db828c8b51__section_sq1_nf3_vdb"/>

## Configuration Parameters


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

cmdLine

</td>
<td valign="top">

string

</td>
<td valign="top">

The command line to be executed.

</td>
</tr>
</table>



<a name="loio50f0d5c1928d44d9947e55db828c8b51__section_knq_5f3_vdb"/>

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

`stdin` 

</td>
<td valign="top">

blob

</td>
<td valign="top">

The input for standard input.

</td>
</tr>
</table>



<a name="loio50f0d5c1928d44d9947e55db828c8b51__section_swc_cg3_vdb"/>

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

`stdout` 

</td>
<td valign="top">

blob

</td>
<td valign="top">

The output from standard output.

</td>
</tr>
<tr>
<td valign="top">

`stderr` 

</td>
<td valign="top">

blob

</td>
<td valign="top">

The output from standard error.

</td>
</tr>
</table>

