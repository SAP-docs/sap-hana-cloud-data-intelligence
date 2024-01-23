<!-- loio70c7622a03da41efbe2013b141a082ed -->

<link rel="stylesheet" type="text/css" href="../css/sap-icons.css"/>

# Uploading Solution in System Management



## Procedure

1.  First you need to compress your solution to a .tar.gz format: `tar -czf my_pysolution.tar.gz -C my_pysolution/ .`

2.  Log into SAP Data Intelligence System Management as Tenant Administrator.

3.  Choose the *Tenant* tab on the horizontal bar at the top of the screen.

4.  Click *Solutions* tab under Cluster Management and then the :heavy_plus_sign: \(Add Solution\) to create a new solution. Give a name in the *File name* field and find the `my_solution.tar.gz` file in your system and click *Open*.

5.  Add this new layer to an existing strategy or create a new one by clicking the *Strategies* tab.

    If you create a new strategy you will need to associate it with a tenant in the *Tenants* tab.




<a name="loio70c7622a03da41efbe2013b141a082ed__result_d4r_t5m_n2b"/>

## Results

If you log into a user from the tenant that you just associated the strategy containing the new layer, you will be able to see the operators from your solution when you launch a new SAP Data Intelligence Modeler instance or when you restart an existing one.

