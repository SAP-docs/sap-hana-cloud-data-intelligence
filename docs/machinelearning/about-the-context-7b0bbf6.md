<!-- loio7b0bbf6724f6433791d8b1d8baba1e6e -->

# About the Context

When working with an ML scenario, the context is already established as we are working within it. To retrieve the attributes of an ML scenario, simply access them as properties of the scenario object:

```
import sapdi
s = sapdi.get_current_scenario()
print(s.name)
```

