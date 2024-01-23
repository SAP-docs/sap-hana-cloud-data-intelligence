<!-- loio761715f7f2524b52a4e6c0708160dc5d -->

# Creating a Custom ABAP Operator

This text describes the steps you need to perform in your ABAP-based SAP system to implement your own custom ABAP operator.



## Context

> ### Note:  
> -   Custom operators can only be used together with the Custom ABAP Operator, which is a generation 1 operator in SAP Data Intelligence.
> 
> -   This text describes how to create a custom ABAP operator in the ABAP-based SAP system. For general information about how to work with custom operators, see Creating Operators in the Modeling Guide for SAP Data Intelligence.

For more information, see also the following blog article: [https://blogs.sap.com/2021/06/01/integrating-abap-function-modules-with-sap-data-intelligence/](https://blogs.sap.com/2021/06/01/integrating-abap-function-modules-with-sap-data-intelligence/)

You create custom ABAP operators in the ABAP-based SAP system by implementing a BAdI called BADI\_DHAPE\_ENGINE\_OPERATOR. For each BAdI implementation, a filter must be defined that matches the name of the operator \(example: com.sap.abap.pass\).

The BAdI implementation consists of a class with two methods that must be redefined. The BAdI implementation should extend the abstract class cl\_dhape\_graph\_oper\_abstract.

-   GET\_INFO: Returns metadata about the operator

-   NEW\_PROCESS: Creates a new instance of the operator


The operator instance \(process\) implements the interface if\_dhape\_graph\_process, though it is recommended that the process extends the abstract class cl\_dhape\_graph\_proc\_abstract instead.

**Creating the artefacts for your ABAP operator**: To reduce manual activities to a minimum, there is a framework that supports you in creating all the described artefacts in the ABAP backend. The framework consists of two reports that must be executed in sequence. They are available with SAP S/4HANA 1909 and any SAP NetWeaver-based system with SAP\_BASIS 7.76 and higher or SAP\_ABA 75E and higher.



## Procedure

1.  Execute the DHAPE\_CREATE\_OPERATOR\_CLASS report.

    The report creates the operator implementation class of your custom ABAP operator.

    > ### Note:  
    > If your ABAP-based SAP system is not an S/4HANA System, use report R\_LTAPE\_CREATE\_OPERATOR\_CLASS to create the operator implementation class.

    You must provide the following parameters:

    -   Class name
    -   Operator name in SAP Data Intelligence
    -   Class description

2.  Execute the DHAPE\_CREATE\_OPER\_BADI\_IMPL report.

    > ### Note:  
    > If your ABAP-based SAP system is not an S/4 HANA system, use report R\_LTAPE\_CREATE\_BADI\_IMPL to create the operator implementation class.

    You must provide the following parameters:

    -   Enhancement impl. name

    -   Class description

    -   BAdI Implementation

    -   Reference to impl. class

    -   Operator name \(SAP Data Intelligence\)


    Now the class is created and the two methods GET\_INFO and STEP can be modified according to your needs.

3.  Adapt the GET\_INFO method.

    Adapt the GET\_INFO method template sections of the new operator to meet your requirements:

    -   Change the number, names, and typing of the ports according to your needs \(the structure *ls\_port* in the below template code\).

    -   Add any parameters, if needed \(the structure ls\_prop in the below template code\).


4.  Adapt the *process* local class.

    Inside the process method, you can implement the actual logic that you would like to execute within your custom ABAP operator. Processes use a simple event-based model and can be implemented by redefining one or more of the following methods:

    -   ON\_START: Called once before the graph is started.

    -   ON\_RESUME: Called at least once before the graph is started or resumed.

    -   STEP: Called frequently.

    -   ON\_SUSPEND: Called at least once after the graph is stopped or suspended.

    -   ON\_STOP: Called once after the graph is stopped.


    Additionally, the abstract class provides several helper methods that you can use:

    -   GET\_PORT: Get an input or output port.

    -   GET\_CONF\_VALUE: Get a value from the process configuration properties.





## Example

To become more familiar with the event-based model, use this example implementation:

> ### Sample Code:  
> ```
> CLASS lcl_process DEFINITION
> INHERITING FROM cl_dhape_graph_proc_abstract.
> PUBLIC SECTION.
> METHODS: if_dhape_graph_process~on_resume REDEFINITION.
> METHODS: if_dhape_graph_process~step REDEFINITION.
> PRIVATE SECTION.
> DATA: mo_in TYPE REF TO if_dhape_graph_channel_reader.
> DATA: mo_out TYPE REF TO if_dhape_graph_channel_writer.
> DATA: mv_data TYPE string.
> ENDCLASS.
> CLASS lcl_process IMPLEMENTATION.
> METHOD if_dhape_graph_process~on_resume.
> mo_in = get_port( 'in' )->get_reader( ).
> mo_out = get_port( 'out' )->get_writer( ).
> ENDMETHOD.
> METHOD if_dhape_graph_process~step.
> CHECK mv_alive = abap_true.
> IF mo_in->has_data( ).
> CHECK mo_out->is_blocked( ) <> abap_true.
> mo_in->read_copy( IMPORTING ea_data = mv_data ).
> mo_out->write_copy( reverse( mv_data ) ).
> ELSEIF mo_in->is_closed( ).
> mo_out->close( ).
> mv_alive = abap_false.
> ENDIF.
> rv_progress = abap_true.
> ENDMETHOD.
> ENDCLASS.
> ```

In the ON\_RESUME method, you get the input and output channels of the operator. This only needs to be done once.

> ### Note:  
> If the user tries to get a port that is not defined in GET\_INFO or tries to get a reader for an output port that does not exist, this results in an error.

In the STEP method, the operator first checks if the process is still alive. If this is not the case, no further action is taken.

The operator then checks if there is any data available on the input channel. If this is the case, and if the output channel is not blocked, the operator reads the data from the input channel. Finally, it reverses the data and writes it to the output channel.

Until the data is consumed by a subsequent process, the output is blocked.

If the input is empty and already closed, the system closes the output channel and sets the operator to be no longer alive. Once all operator processes indicate that they are no longer alive, the graph terminates automatically.

The system may temporarily suspend graph execution, for example during a maintenance event. When this happens, you can store any necessary local state by adding it to the io\_saved\_state object that is passed to the ON\_SUSPEND method.

When the graph is resumed later, the same io\_saved\_state object is again passed to the ON\_RESUME method. You can restore the local state as described above.

To get the new operator definition into the repository of SAP Data Intelligence, use custom ABAP operator.

