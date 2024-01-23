<!-- loio781938a8d99944d099c94ac813962c34 -->

# Using Python Libraries

To make Python libraries available to your operator, you can add tags to it so that upon graph execution, the appropriate docker image can be chosen.

You can create or extend dockerfiles through the user interface and add tags to associate it with an operator. The following example details the necessary steps.

Suppose that you want to use the numpy library \(version 1.16.1\) on your custom Python operator.

First, create a new dockerfile:

1.  Open the *Repository* tab and select a subfolder.
2.  Right-click the subfolder and select *Create Docker File*.
3.  Provide a name and choose *OK*.

    There are many ways to create a dockerfile that contains Python and the numpy library. For example, you can enter <code>FROM <i class="varname">&lt;public_numpy_docker_image&gt;</i></code> in the first line. If you use a public image, make sure that it also contains the requirements to run the Python subengine, which are: `tornado==6.1.0` and `python3.9`. The tag key-value pairs for the requirements are: `'tornado': '6.1.0'` and `'python39': ''`.

    Alternatively, you can inherit from the default Modeler python3 dockerfile and add numpy to it. In this way, all of the requirements for the standard *Python3 Operator* are already satisfied. The following dockerfile shows one way that you can accomplish this:

    ```
    FROM $com.sap.sles.base
    
    RUN python3.9 -m pip install --user numpy="1.16.1"
    ```

4.  After you write the dockerfile content, add tags on the configuration panel for every relevant resource that this dockerfile offers, in addition to the tags from its parent dockerfile. That is, you don't need to repeat the tags that the parent dockerfile already has. For example, the numpy for python3 dockerfile needs only the following tag `numpy39: 1.16.1`.

    > ### Note:  
    > Make sure you are installing the library for the right version of Python, which is 3.9. Notice that we added the suffix \`36\` to the numpy tag to reflect the Python version where they were installed. This can be useful if, in the future, we create a new subengine that uses a different python version.

5.  The final step is to add the new tag to your operator in the operator editor view. Add the tag `"numpy39": "1.16.1"` to your Python operator. Alternatively, you can also add tags to a group defined on the graph.


For more information, see [Python3 Operator](https://help.sap.com/viewer/9182d964573745e89f523395d7c43e53/Dev/en-US/021180336add475bbd712b0ce5d393c1.html "Use the Generation 1 Python3 operator to define a script that offers convenience functions from API objects, such as callbacks.") :arrow_upper_right: documentation.

**Related Information**  


[Creating Dockerfiles](../creating-dockerfiles/creating-dockerfiles-62d1df0.md "Dockerfiles contain all commands that you call on a command line to assemble a docker image.")

