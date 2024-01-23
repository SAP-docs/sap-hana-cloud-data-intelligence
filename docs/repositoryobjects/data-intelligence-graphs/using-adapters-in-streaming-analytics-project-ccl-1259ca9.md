<!-- loio1259ca9ee36f4ce69afa829a0072aa61 -->

# Using Adapters in Streaming Analytics Project CCL

This example graph shows how you can send and receive data to and from a streaming analytics operator \(project\) using adapters. You add an adapter to the operator using Continuous Computation Language \(CCL\). With an adapter, all data is sent and received without using any input or output ports. However, you can always add input or output ports as they offer another option to send and receive data.



## Prerequisites

The streaming analytics and SAP HANA Monitor operators in this example require a connection called HANA\_DB1 of type HANA\_DB. This connection is defined in the Connection Manager. Make sure your Connection Manager has this connection configured to point at your SAP HANA tenant database. If you use a different connection name, you'll need to also update the connection properties in the operators and pick your connection name from the drop-down list. Also, if you change the connection name, you'll need to also update the *service* property for the hana\_out and db\_in adapters in the project CCL to ensure they use the new connection name.



<a name="loio1259ca9ee36f4ce69afa829a0072aa61__section_g3f_14y_vgb"/>

## Run the Graph

In your SAP HANA tenant database, run following SQL to initialize the schema and tables required by this example:

```
CREATE SCHEMA STREAMING;

CREATE COLUMN TABLE STREAMING.TRADES
(	ID INTEGER,
	TS BIGINT,
	SYMBOL VARCHAR(16),
	PRICE DECIMAL(20,2),
	VOLUME INTEGER,
	PRIMARY KEY ( ID )
);                

CREATE COLUMN TABLE STREAMING.OLD_TRADES
(	ID INTEGER,
	TS BIGINT,
	SYMBOL VARCHAR(16),
	PRICE DECIMAL(20,2),
	VOLUME INTEGER,
	PRIMARY KEY ( ID )
);

INSERT INTO "STREAMING"."OLD_TRADES"( ID, TS, SYMBOL, PRICE, VOLUME ) VALUES ( 17701, 1543596817578, 'SAP', 30.58, 10166 );
INSERT INTO "STREAMING"."OLD_TRADES"( ID, TS, SYMBOL, PRICE, VOLUME ) VALUES ( 17702, 1543596817678, 'SAP', 81.44, 13897 );
INSERT INTO "STREAMING"."OLD_TRADES"( ID, TS, SYMBOL, PRICE, VOLUME ) VALUES ( 17703, 1543596817778, 'MSFT', 79.85, 10855 );
INSERT INTO "STREAMING"."OLD_TRADES"( ID, TS, SYMBOL, PRICE, VOLUME ) VALUES ( 17704, 1543596817977, 'MSFT', 82.6, 10079 );
INSERT INTO "STREAMING"."OLD_TRADES"( ID, TS, SYMBOL, PRICE, VOLUME ) VALUES ( 17705, 1543596818078, 'IBM', 59.45, 12622 );
INSERT INTO "STREAMING"."OLD_TRADES"( ID, TS, SYMBOL, PRICE, VOLUME ) VALUES ( 17710, 1543596818978, 'MSFT', 42.53, 13409 );
```

To reset a tenant database's contents between test runs, use the following SQL:

```
delete from STREAMING.TRADES;

```

**Related Information**  


[SAP HANA Streaming Analytics: Adapters Guide](https://help.sap.com/viewer/52acc1f6b1d7428caab280d193c820f6/latest/en-US/db1254997e614af7a06e38cb1c24c3ea.html)

[Adding an Adapter to a Project](https://help.sap.com/viewer/f1da0b944b1c4eae8137c9f913b66d44/latest/en-US/e79342a66f0f1014acf6ab890cee7be6.html)

