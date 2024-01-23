<!-- loio43db62ec91b2473b96b28f40e1fb3cee -->

# Creating Tests

When you create a new operator extending *BaseOperator*, you can also create unit tests using the Python unit testing framework.

We recommend that you create a folder called `test` in your project root \(parallel with the folder "my\_solution" in our sample hierarchy\) and in it, use the same folder structure that you used when creating the operator. For example, for the operator `appendString`, we create the following folders:

```
test/operators/com/mydomain/util/appendString/
```

Create a file named `test_append_string.py` inside the `appendString` folder:

```
import unittest
from Queue import Queue
from operators.com.mydomain.appendString.operator import AppendString

class TestAppendString(unittest.TestCase):

    def testUpper(self):
        op = AppendString.new(inst_id="1", op_id="anything")
        qin1 = Queue(maxsize=1)
        op.inqs["inString"] = qin1
        qout1 = Queue(maxsize=1)
        op.outqs["outString"] = qout1

        input_config = "config_test"
        op.config.stringToAppend = input_config
        op.config.method = "UPPERCASE"

        op.base_init()  # This will execute the _init method and also other things.

        op.start()  # Start the operator's thread.

        try:
            input_str = "input_test|"
            qin1.put(input_str)  # Send data in the 'inString' input port.
            ret = qout1.get()  # Gets data from the 'outString' output port.

            self.assertEqual((input_str + input_config).upper(), ret)  # Verify that the output is equal to the expected result.
        finally:
            op.stop()  # stop the operator no matter what happens. Otherwise the test may hang forever.
```

To run unit tests for all Python files that start with the prefix "test", create a script such as the following:

```
PYSIX_PATH=<PYSIX_SUBENGINE_PATH>  # replace <PYSIX_SUBENGINE_PATH> by the path to your pysix_subengine folder.

SCRIPT_DIR=$(dirname "$0")
cd $SCRIPT_DIR  # changes working dir to the folder where the script is located (which should be the 'test' folder).

SUBENGINE_ROOT=$(realpath ../my_pysolution/vrep/vflow/subengines/com/sap/python36)  # Gets absolute path of python36 folder.

export PYTHONPATH=$PYTHONPATH:$PYSIX_PATH:$SUBENGINE_ROOT  # Append paths to pythonpath.

python3.6 -m unittest discover -s . -p "test*.py" -v

cd -
```

Place the script in the `test` directory that you created.

To check the official documentation of the Python unit test module, see [https://docs.python.org/2/library/unittest.html](https://docs.python.org/2/library/unittest.html).

