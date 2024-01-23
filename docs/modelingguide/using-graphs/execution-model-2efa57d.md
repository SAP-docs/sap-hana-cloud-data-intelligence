<!-- loio2efa57d849fa457f8c4a771b9d6d4927 -->

# Execution Model

To avoid problems, such as back pressure and deadlocks, SAP Data Intelligence Modeler executes graphs following an execution model.



<a name="loio2efa57d849fa457f8c4a771b9d6d4927__section_usm_2c4_cxb"/>

## Back Pressure

The Modeler executes operators in all graphs concurrently. Operators communicate with each other by sending data to their outports and receiving data from their inports. When “Back-pressure” between two operators occurs, the Modeler blocks the operator that is trying to send data until the receiving operator reads it. This blocking prevents data from accumulating on a region of the pipeline that produces data faster than other parts can consume.



<a name="loio2efa57d849fa457f8c4a771b9d6d4927__section_u5q_jm2_s3b"/>

## Deadlocks

Back pressure can cause some graphs with cycles to deadlock. A deadlock happens in graphs when there are at least as many messages in the cycle as there are nodes in the cycle.

> ### Example:  
> The following graph has a cycle between operators A, B, and C:
> 
> ```
> A--->B--->C
>      ^    |
>      +----+
> ```
> 
> A smooth execution of a graph with no deadlocks happens when operator A generates just one message and sends it to operator B or operator C. Each time operator B or C receives a message through their inport, they process the message and then send a new message through their outport. This process implies that there's always a single message circulating around the cycle, and no deadlock occurs.
> 
> A deadlock can occur when, instead of operator A feeding just one message into the graph, it produces two messages. When operator A produces two messages, the graph deadlocks because of the following activity:
> 
> -   Operator B is blocked when it tries to send a message to operator C.
> -   Operator C doesn't read from its inport because it's trying to send the message to operator B.
> -   Operator B doesn't read from its inport because it's trying to send the message to operator C.
> 
> The graph can also deadlock under the following circumstances:
> 
> -   Operator A generates only one message.
> -   Operator B outputs two messages for each one message that it receives from Operator A at its input port.



<a name="loio2efa57d849fa457f8c4a771b9d6d4927__section_afl_lm2_s3b"/>

## Sending Data and Mutable Objects

When an operator sends data to another operator, the Modeler doesn't send a copy of the data. Instead, the Modeler sends only a reference to the data. Sending a reference to the data decreases the communication cost.

However, when the graph has mutable objects, it's more secure to send copies of the objects. A mutable object, such as a message data type, is one in which you can modify or edit a value. When you program a script operator and change an object received on input, the object can reflect in other parts of the graph. Therefore, it's safer to make a copy of a mutable object before you change it instead of sending a reference to the data.

