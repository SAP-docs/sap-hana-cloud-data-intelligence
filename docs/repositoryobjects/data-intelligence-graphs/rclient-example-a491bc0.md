<!-- loioa491bc04782e40fea2aa8e1255703ce8 -->

# RClient Example

This graph shows the different features of the RClient operator.



This graph has an RClient operator at its center, which has 5 input ports and 4 output ports. The script of this RClient operator shows how to use the following `api` methods: `api$setSwitchCallback`, `api$setPortCallback`, `api$addTimer`, and `api$addShutdownHandler`.



This text assumes the reader has already read the [R Client \(Deprecated\)](../data-intelligence-operators/r-client-deprecated-30423dc.md) operator documention.



<a name="loioa491bc04782e40fea2aa8e1255703ce8__section_cpl_vpf_dfb"/>

## api$setSwitchCallback

First, the following "switch" callback is set for the input port `input5`, and output port `output2`:

```
switchFunc <- function(data) {
    pos <- FALSE
    if (data > 10) {
        pos <- TRUE
    }
    list(switchPosition=pos, output2=toString(data))
}

api$setSwitchCallback(c("input5"), c("output2"), "switchFunc")
```

The argument `data2` from `input5` is of type int64. Every time inport `input5` has data waiting to be read, the `switchFunc` is called with this data as an argument. The switch position will remain in its "off" \(`FALSE`\) state until the incoming data is greater than 10. When data is greater than 10, `pos` will be set to `TRUE`, and the switch position will be moved to its "on" state.

> ### Note:  
> The `switchPosition` parameter name in the returned `list` should always be used in a switch callback function.

As explained in the RClient documentation, the switch "on" position enables all other callbacks associated with other ports. This means that the other callbacks will start reading their input ports only when the inport `input5` receives a value greater than 10.



<a name="loioa491bc04782e40fea2aa8e1255703ce8__section_n15_2qf_dfb"/>

## api$setPortCallback

There are five port callbacks set in the script of the RClient operator. The first two callbacks, `foo` and `bar`, are associated with the same input ports `input1` and `input2`:

```
foo <- function(data1, data2) {
    list(output1=data1 + data2)
}
api$setPortCallback(c("input1", "input2"), c("output1"), "foo")

bar <- function(data1, data2) {
    flag <- (data1*data2) %% (data1 + data2) == 0
    if (!is.na(flag) && flag) {
        print("something") # Will only be printed in the Rserve stdout.
        return(NULL) # skip send to outports in this call
    }
    print("another thing")

    list(output1=data1 * data2, output2=toString(data1 + data2))
}
api$setPortCallback(c("input1", "input2"), c("output1", "output2"), "bar")
```

However, the `foo` sends to outport `output1`, and `bar` sends to outports `output1` and `output2`. As `bar` is registered after `foo`, when data is available in port `input1` and `input2`, the same pair of data will first be used to call `foo` and then used to call `bar`.

The function `bar` shows two interesting features:

-   You can use print\("text"\) to send data to Rserve stdout.

-   If you return\(NULL\), then nothing will be sent to the output ports associated with this callback for this given call. This is useful if you don't want to send anything, for some calls of the callback, to the output ports associated with it.


> ### Note:  
> We send a number to the `output1` port as the port type is int64, and we send a string to `output2` as the port type is string.

The callback `foo2` is on the script just to demonstrate that callbacks associated with different inport groups can send to the same output port. In this case, `bar` and `foo2` both send to `output2`.

```
foo2 <- function(data1) {
    list(output2=paste("concat!", data1))
}
api$setPortCallback(c("input3"), c("output2"), "foo2")
```

The `dataFrameFunc` callback shows that when a message of type table is fed to inport `input4`, then it will be automatically converted to a dataframe object. The value of cell \(1,2\) of the dataframe is multiplied by 10 and then sent to `output3`. The class name of the received data is sent on `output2`.

```
dataFrameFunc <- function(data) {
    data[1,2] <- data[1,2] * 10
    list(output2=class(data), output3=data)
}
api$setPortCallback(c("input4"), c("output2", "output3"), "dataFrameFunc")
```

The table message is built using a Python 3 operator, which has its outport connected to RClient's inport `input4`. Below is the Python code that builds the table message:

```
msg = api.Message([["abc", "defg"], [counter, 10]], {"fieldNames": ["column 1", "column 2"]}, "table")
api.send("output", msg)
counter += 1
```

The `foo3` functions shows that a callback doesn't need to be associated with an output port. `foo3`, in this case, is simply used to update the global variable `counter` \(which is going to be used again by another callback\):

```
counter <<- 0L

foo3 <- function(data1) {
    counter <<- counter + nchar(data1)
}

api$setPortCallback(c("input3"), c(), "foo3")
```



<a name="loioa491bc04782e40fea2aa8e1255703ce8__section_u5q_crf_dfb"/>

## api$addTimer

The script in the RClient operator has two timer callbacks:

```
periodicFunc1 <- function() {
    counter <<- counter + 1L
    list(output1=counter)
}
api$addTimer("1s", c("output1"), "periodicFunc1")

periodicFunc2 <- function() {
    counter <<- counter * 2L
}
api$addTimer("2s", c(), "periodicFunc2")
```

The first increments the `counter` global variable and sends it to `output1` port. The second is not associated with any port and just multiplies the `counter` by 2.



<a name="loioa491bc04782e40fea2aa8e1255703ce8__section_z3z_frf_dfb"/>

## api$addShutdownHandler

There are two shutdown callbacks in the RClient script. Those two will be called in the order they appear below when the graph is graph fails or is scheduled to stop.

```
shutdownFunc <- function() {
    print("shutdown 1 was called")
}
api$addShutdownHandler("shutdownFunc")

shutdownFunc2 <- function() {
    print("shutdown 2 was called")
}
api$addShutdownHandler("shutdownFunc2")
```

