<!-- loio6fb5e158accc4c36a9c7a45379f62063 -->

# Executing or Deploying Pipelines

To execute or deploy a pipeline within an ML scenario, you first need to create a configuration:

```py
from sapdi.scenario.configuration import Configuration
config = Configuration.create(bindings = [{'key':'model_name', 'value': "inception", 'type': "parameter"}],  name = "myConfig", pipeline = pipeline, scenario_version = sapdi.get_current_version())
```



<a name="loio6fb5e158accc4c36a9c7a45379f62063__section_ptf_2vc_f3b"/>

## Executing a Pipeline

You use the configuration to execute the pipeline:

```py
e = pipeline.execute(config)
```

While the pipeline is being executed, you can query its status:

```py
e.status # e.g.'RUNNING'
```

Alternatively, you can wait until the execution is complete:

```py
e.wait_for_completion()
```



<a name="loio6fb5e158accc4c36a9c7a45379f62063__section_g35_2vc_f3b"/>

## Deploying a Pipeline

In the same way, you can use the configuration to deploy a pipeline:

```py

from sapdi.scenario.deployment import Deployment
deployment = Deployment.create(config)
```

