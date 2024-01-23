<!-- loiob0166c93f8ab49c681df1628a63e590c -->

# Sending Datatypes to Streaming Analytics Projects

This example graph shows how to send data rows containing various streaming analytics column datatypes to a streaming analytics project.



Input data can be generated in CSV or JSON format by setting the *outputFormat* property on the Data Generator operator and then setting the corresponding value for the 'input format' property on the attached streaming analytics operator. You can also specify the format of the data using the*output format* operator property. Note that when you attach two streaming analytics operators together, you'll need to ensure the output to input formats match.

This example also shows the use of string and message types for input and output ports. Both port types support CSV and JSON data formats.

Finally, the example shows how to batch input and output data. To change the batch size of incoming data, use the *batchSize* property in the Data Generator operator. The attached streaming analytics operator will then automatically process incoming data using this new size. To change the batch size of data being sent from the operator output ports, use the'*output batch size* operator property.

**Related Information**  


[Datatypes](https://help.sap.com/viewer//f1da0b944b1c4eae8137c9f913b66d44/latest/en-US/e79e13026f0f1014a68bb0753a38414a.html)

[SAP HANA Streaming Analytics: Developer Guide](https://help.sap.com/viewer/f1da0b944b1c4eae8137c9f913b66d44/latest/en-US/0189088be76e4675bf0a63b930a68f1d.html)

