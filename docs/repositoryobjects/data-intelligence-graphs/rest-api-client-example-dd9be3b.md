<!-- loiodd9be3bc992740a0a3969a8650b92a48 -->

# REST API Client Example

This scenario showcases how to generate a request to be executed by the REST API Client operator and how to handle the response that it provides.



In this example, the `yahoo Finance` API endpoint is used to fetch the current stock price of a specified stock ticker.

Once the data is successfully fetched, it is printed in the terminal operator.



<a name="loiodd9be3bc992740a0a3969a8650b92a48__section_vhj_htf_gxb"/>

## Prerequisites

A HTTP connection with the following configurations:

```
   Host: "query2.finance.yahoo.com",
   Port: 443,
   Protocol: "HTTPS",
   Authentication: "NoAuth",
   Path: "/"
```



<a name="loiodd9be3bc992740a0a3969a8650b92a48__section_f5y_3tf_gxb"/>

## Configure and Run the Graph

To run the graph, it is necessary to provide substitution values for the `TICKER` and `HTTP_CONNECTION`.

Alternatively, the configurations can be manually changed in the graph itself to make them have fixed values.

