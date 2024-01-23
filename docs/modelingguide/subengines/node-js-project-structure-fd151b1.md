<!-- loiofd151b16c4cd4541b30363d5688416d4 -->

# Node.js Project Structure

To deploy a Node.js operator to an To deploy your operator later to a different SAP Data Intelligence system, create a project structure.

Structure your Node.js project as in the following script:

```
|- my_solution/
    |- vsolution.json
    |- vrep/vflow/
        |- subengines/com/sap/node/operators/
            |-- example
               |-- operator.json
               |-- script.js
               |-- icon.svg
```

Before you deploy this project structure to a different SAP Data Intelligence system, you must first archive it. To create an archive, use the tar archiver \(on macOS and Linux\) as in the following script:

```
tar -C <path to my_solution> -czf my_solution.tar.gz
```

> ### Note:  
> To verify the structure of your archive, ensure that the folder `vrep` is at the top level of the archive, beside the file '`vsolution.json`'.

