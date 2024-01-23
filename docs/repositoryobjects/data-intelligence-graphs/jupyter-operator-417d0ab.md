<!-- loio417d0abcfa364d68baa790b7fe885d04 -->

# Jupyter Operator

This is a template graph for the use of a Jupyter operator in the context of an ML scenario. It allows you to open and run a notebook from a scenario in a pipeline, and it is meant to be modified as needed.



In this particular example, the Jupyter operator has an input port called "in" and an output port called "out", which can be used to communicate with a Terminal operator.

See the pipeline [Jupyter Example](jupyter-example-61af45d.md) and the Jupyter operator documentation for examples of how the operator can be used to interact with data flowing through the graph.



<a name="loio417d0abcfa364d68baa790b7fe885d04__section_owp_fg4_k4b"/>

## Running the Graph

This graph is intended to be used from the Machine Learning Scenario Manager \(MLSM\) app.

Follow the steps below to run the template:

1.  Open MLSM from the SAP DI Launchpad.

2.  Create a scenario.

3.  Create a pipeline and choose the *Jupyter operator* template. DI opens the Modeler app with the template.

4.  Save the graph.

5.  Go back to MLSM and *execute* the pipeline.

6.  When the wizard prompts for a notebook file path, either enter the name of a notebook from your scenario or a new name if you want to create a new notebook \(note that new notebooks are associated with the pipeline but are not registered as part of the scenario\).

7.  Go back to the Modeler.

8.  Right-click on the Jupyter operator and select *Open UI*.

9.  Modify the notebook and pipeline as needed.

    > ### Note:  
    > > ### Note:  
    > 
    > If the operator opened an existing notebook from a scenario, any modifications to the file will be reflected in the original scenario notebook.


