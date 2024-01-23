<!-- loiod9a3063ec31841cdbdd64c8847dcc67e -->

# Referencing Parent Docker Images

To create a new Docker image, SAP Data Intelligence Modeler allows you to reference a parent Docker image, which can be an existing Dockerfile from the repository or a prebuilt Docker image.

In a Dockerfile, use the `FROM` instruction to specify the parent Docker image from which to build a new image. The following sections contain information about each type of parent Docker image to use, and includes the method with additional considerations.



<a name="loiod9a3063ec31841cdbdd64c8847dcc67e__section_unw_24z_gxb"/>

## Use an Existing Dockerfile with the '$' Symbol.



### Parent Docker Image

Existing Dockerfile



### Method

`FROM $`



### Details

Use the '$' symbol to name an existing Dockerfile from the repository. The '$' symbol provides inheritance of the tags and the resource limits of the referenced Dockerfile. The inheritance is transitive; the Docker image can inherit from a Dockerfile that already inherits from another Dockerfile. The inheritance ends when the system encounters either a reference to a custom Dockerfile or a '$' reference.

When you build a Dockerfile that uses inheritance, the system builds all necessary images in the inheritance chain as needed. However, you can't reference a specific version of the parent Docker image directly using the '$' symbol because the topmost Dockerfile in the inheritance chain has already defined the version of the parent Docker image to use. For more information about inheritance, see [Dockerfile Inheritance](dockerfile-inheritance-d49a07c.md).

> ### Note:  
> Compared to the '§' symbol, the '$' symbol references another Dockerfile and not a prebuilt Docker image.

In the following Dockerfile example, the Dockerfile inherits all properties from the existing Dockerfile `com.sap.sles.base`. The definition of the referenced Dockerfile is in the repository at `com/sap/sles/base`. The new parent Docker image inherits all tags and resource limits of the referenced Dockerfile.

> ### Example:  
> ```
> FROM $com.sap.sles.base
> ...
> 
> ```

> ### Note:  
> If you want to specify a specific version of the parent Docker image, use the '§' symbol method, which bases your Docker image on a prebuilt Docker image.



### Considerations for Using an Existing Dockerfile


<table>
<tr>
<th valign="top">

Advantages

</th>
<th valign="top">

Disadvantages

</th>
</tr>
<tr>
<td valign="top">

-   Ready to use
-   Inherited tags from parent Docker image
-   Automatic updates
-   Few customizations needed



</td>
<td valign="top">

No control over updates

</td>
</tr>
</table>



<a name="loiod9a3063ec31841cdbdd64c8847dcc67e__section_xd1_g4z_gxb"/>

## Use a Prebuilt Docker Image with the '§' Symbol



### Parent Docker Image

Prebuilt Docker image



### Method

`FROM §`



### Details

SAP Data Intelligence includes prebuilt Docker images with the software package and stores the images in the Docker registry. The '§' symbol is a placeholder for the SAP Data Intelligence Docker registry address. In the Dockerfile, enter the name and version of the parent Docker image after the location.

> ### Note:  
> Compared to the '$' symbol, the '§' symbol references a prebuilt Docker image and not another Dockerfile.

The following example Dockerfile references the address for the Docker registry that contains the prebuilt Docker image and version <code>vflow-customer-sles:<i class="varname">&lt;version&gt;</i></code>:

> ### Example:  
> ```
> FROM §/com.sap.datahub.linuxx86_64/vflow-customer-sles:<version>
> ...
> 
> ```

> ### Note:  
> When you reference a specific version, there's a risk that the image isn't available over time. However, SAP guarantees certain versions and duration of availability of the Docker image `vflow-customer-sles`. For details, see [3320629](https://me.sap.com/notes/3320629). SAP recommends that you check this SAP Note before every system upgrade.



### Considerations for Using a Prebuilt Docker Image


<table>
<tr>
<th valign="top">

Advantages

</th>
<th valign="top">

Disadvantages

</th>
</tr>
<tr>
<td valign="top">

-   Explicit image URL
-   Controllable updates



</td>
<td valign="top">

-   SAP controls the image updates
-   Tags are provided on inheriting image
-   More customizations needed



</td>
</tr>
</table>



<a name="loiod9a3063ec31841cdbdd64c8847dcc67e__section_e13_h4z_gxb"/>

## Use a Prebuilt Image from a Custom Docker Registry



### Parent Docker Image

Prebuilt Docker image from custom Docker registry



### Method

`FROM`



### Details

Use this method to create a new Docker image based on a prebuilt image that you store in a custom Docker registry.

In the following example, the Dockerfile references a prebuilt Docker image, `my-image:1.0.0`, from a custom Docker registry, <code><i class="varname">&lt;custom-registry&gt;</i></code>:

> ### Example:  
> ```
> FROM <custom-registry>/my-image:1.0.0
> ...
> ```

For details on how to configure a custom Docker registry, see [Manage Modeler Custom Registry Secret](https://help.sap.com/docs/SAP_DATA_INTELLIGENCE/ca509b7635484070a655738be408da63/f91ebfeccb3d434980e33f856f1fcb5a.html?version=Cloud).



### Considerations for Using a Prebuilt Image From a Custom Docker Registry


<table>
<tr>
<th valign="top">

Advantages

</th>
<th valign="top">

Disadvantages

</th>
</tr>
<tr>
<td valign="top">

-   Full control over image content \(except for SAP requirements\)
-   Full control over image lifecycle \(except for SAP requirement changes\)



</td>
<td valign="top">

-   Greater initial effort
-   Required to provide operator and subengine requirements to use SAP standard
-   Manual updates
-   No SAP testing



</td>
</tr>
</table>

