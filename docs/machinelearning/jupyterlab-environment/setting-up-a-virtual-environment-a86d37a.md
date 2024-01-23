<!-- loioa86d37a3530c48d79c63dd421f3f24db -->

<link rel="stylesheet" type="text/css" href="../css/sap-icons.css"/>

# Setting Up a Virtual Environment

Set up a virtual environment to conduct independent experiments with different machine learning scenarios that require conflicting library versions.



<a name="loioa86d37a3530c48d79c63dd421f3f24db__context_gd3_fvq_fhb"/>

## Context

In some cases, you may want to experiment with machine learning scenarios that use conflicting library versions \(for example, different TensorFlow versions\). To experiment with these scenarios independently of one another, you can set up environments and run each experiment in its own environment.



<a name="loioa86d37a3530c48d79c63dd421f3f24db__steps_nv3_ptq_fhb"/>

## Procedure

1.  Open a new console by opening the file browser \(<span class="SAP-icons"></span>\), clicking the plus button, and selecting the Python 3 \(ipykernel\) console from the *Launcher* tab.

2.  In your new console, run the following code, where *<conda\_env\>* is the name you give to your environment.

    ```
    import json
    
    !conda create --quiet --yes -p $CONDA_DIR/envs/<conda_env> ipython ipykernel kernda
    !ln -s $CONDA_DIR/envs/<conda_env>/bin/pip $CONDA_DIR/bin/pipx
    !conda clean -tipsy
    !mkdir -p /tmp/<conda_env>/
    kernel_cmd = '''{
      "argv": [
        "bash",
        "-c",
        "source /opt/conda/bin/activate /opt/conda/envs/<conda_env> && exec /opt/conda/envs/<conda_env>/bin/python -m ipykernel_launcher -f '{connection_file}' "
      ],
      "display_name": "<conda_env> Kernel",
      "language": "python"
    }'''
    
    kernel_cmd = json.loads(kernel_cmd)
    with open("/tmp/<conda_env>/kernel.json", "w") as file:
        json.dump(kernel_cmd, file)
    
    !jupyter kernelspec install /tmp/<conda_env> --user
    !jupyter kernelspec list
    ```

3.  Refresh your browser to see your new environment.

4.  Optional: You can also create a conda environment in a terminal by modifying the PATH and executing the subsequent commands:

    ```
    export PATH=/opt/AutomatedAnalyticsOem/bin:/opt/conda/bin:/node/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
    conda create --quiet --yes -p $CONDA_DIR/envs/<conda_env> ipython ipykernel kernda
    ln -s $CONDA_DIR/envs/<conda_env>/bin/pip $CONDA_DIR/bin/pipx
    conda clean -tipsy
    mkdir -p /tmp/<conda_env>/
    cat > /tmp/<conda_env>/kernel.json << EOF
    {
      "argv": [
        "bash",
        "-c",
        "source \"/opt/conda/bin/activate\" \"/opt/conda/envs/<conda_env>\" && exec /opt/conda/envs/<conda_env>/bin/python -m ipykernel_launcher -f '{connection_file}' "
      ],
      "display_name": "<conda_env> Kernel",
      "language": "python"
    }
    EOF
    jupyter kernelspec install /tmp/<conda_env> --user
    jupyter kernelspec list
    ```


