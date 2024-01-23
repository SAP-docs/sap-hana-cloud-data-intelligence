<!-- loiob81ccec0d40c469b959bdee8b6302857 -->

<link rel="stylesheet" type="text/css" href="../css/sap-icons.css"/>

# Comparing Runs

The metrics explorer lets you compare runs using the visual board. You can view run data in a table or create charts to analyze them graphically.



## Procedure

1.  Start the metrics explorer and select the run collections that contain the runs you want to compare.

    You can compare runs from different scenarios by adding run collections from these scenarios to the list.

2.  Select the runs that you want to compare and click *Open Visual Board*.

    The *Source Runs* tab of the visual board appears showing the run data in a table.

3.  To show the data on a chart:

    1.  Switch to the *Canvas* tab and click *Add Chart*.

    2.  Select the type of chart that you want to create:

        -   *Metric over RunIDs* shows one metric across multiple runs.
        -   *Metric over Params across multiple Runs* shows one metric plotted against a parameter across different runs. This information can be helpful if you are fine-tuning your hyperparameters, for example.
        -   *Metric over time/steps for a single Run* shows how a metric value changes over time.

    3.  Enter the information necessary for your selected chart type and click create.

        The metrics explorer generates the chart and adds it to the visual board. You can click the data points on each chart to view further information.

    4.  **Optional:** Click <span class="SAP-icons"></span> \(Export as PDF\) to download the canvas to your local file system.

        > ### Caution:  
        > If you use your browser's back button or navigate to another application within SAP Data Intelligence, your canvas will be lost. You can, however, toggle between the *Source Runs* and *Canvas* views without losing your changes.



