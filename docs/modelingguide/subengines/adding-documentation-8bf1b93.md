<!-- loio8bf1b93259fa49478d310734b469c1f5 -->

# Adding Documentation

Create the operator documentation in a file named `README.md` in the operator's folder. For example, to create the documentation for the dummy operator `AppendString`, create a new `README.md` file in the following path:

```
{ROOT}/subengines/com/sap/python36/operators/com/mydomain/util/appendString/README.md
```

The documentation is written using Markdown syntax \(more information [here](https://guides.github.com/features/mastering-markdown/)\). You can check the result by right-clicking your operator and choosing *Open Documentation*, in the SAP Data Intelligence Modeler UI.

To add a custom icon for your operator, copy the icon to the operator's folder; for example:

```
{ROOT}/subengines/com/sap/python36/operators/com/mydomain/util/appendString/icon.png
```

Then, make sure that your `_get_operator_info` method sets the `icon.png` file \(or another file\) as the `iconsrc` field, as shown in the following example:

```
def _get_operator_info(self):
        ...
        return OperatorInfo(...,
                            iconsrc="icon.png",
                            ...)
```

Last, you must regenerate the operator's json.

