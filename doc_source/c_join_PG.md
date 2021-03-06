# Querying the Catalog Tables<a name="c_join_PG"></a>


+ [Examples of Catalog Queries](c_join_PG_examples.md)

In general, you can join catalog tables and views \(relations whose names begin with **PG\_**\) to Amazon Redshift tables and views\. 

The catalog tables use a number of data types that Amazon Redshift does not support\. The following data types are supported when queries join catalog tables to Amazon Redshift tables: 

+ bool

+ "char"

+ float4

+ int2

+ int4

+ int8

+ name

+ oid

+ text

+ varchar

If you write a join query that explicitly or implicitly references a column that has an unsupported data type, the query returns an error\. The SQL functions that are used in some of the catalog tables are also unsupported, except for those used by the PG\_SETTINGS and PG\_LOCKS tables\.

For example, the PG\_STATS table cannot be queried in a join with an Amazon Redshift table because of unsupported functions\.

The following catalog tables and views provide useful information that can be joined to information in Amazon Redshift tables\. Some of these tables allow only partial access because of data type and function restrictions\. When you query the partially accessible tables, select or reference their columns carefully\.

The following tables are completely accessible and contain no unsupported types or functions: 

+  [pg\_attribute](http://www.postgresql.org/docs/8.0/static/catalog-pg-attribute.html) 

+  [pg\_cast ](http://www.postgresql.org/docs/8.0/static/catalog-pg-cast.html) 

+  [pg\_depend](http://www.postgresql.org/docs/8.0/static/catalog-pg-depend.html) 

+  [pg\_description ](http://www.postgresql.org/docs/8.0/static/catalog-pg-description.html) 

+  [pg\_locks ](http://www.postgresql.org/docs/8.0/static/view-pg-locks.html) 

+  [pg\_opclass ](http://www.postgresql.org/docs/8.0/static/catalog-pg-opclass.html) 

The following tables are partially accessible and contain some unsupported types, functions, and truncated text columns\. Values in text columns are truncated to varchar\(256\) values\. 

+  [pg\_class](http://www.postgresql.org/docs/8.0/static/catalog-pg-class.html) 

+  [pg\_constraint](http://www.postgresql.org/docs/8.0/static/catalog-pg-constraint.html) 

+  [pg\_database](http://www.postgresql.org/docs/8.0/static/catalog-pg-database.html) 

+  [pg\_group](http://www.postgresql.org/docs/8.0/static/catalog-pg-group.html) 

+  [pg\_language ](http://www.postgresql.org/docs/8.0/static/catalog-pg-language.html) 

+  [pg\_namespace](http://www.postgresql.org/docs/8.0/static/catalog-pg-namespace.html) 

+  [pg\_operator](http://www.postgresql.org/docs/8.0/static/catalog-pg-operator.html) 

+  [pg\_proc](http://www.postgresql.org/docs/8.0/static/catalog-pg-proc.html) 

+  [pg\_settings](http://www.postgresql.org/docs/8.0/static/view-pg-settings.html) 

+  [pg\_statistic](http://www.postgresql.org/docs/8.0/static/catalog-pg-statistic.html) 

+  [pg\_tables](http://www.postgresql.org/docs/8.0/static/view-pg-tables.html) 

+  [pg\_type ](http://www.postgresql.org/docs/8.0/static/catalog-pg-type.html) 

+  [pg\_user](http://www.postgresql.org/docs/8.0/static/view-pg-user.html) 

+  [pg\_views](http://www.postgresql.org/docs/8.0/static/view-pg-views.html) 

The catalog tables that are not listed here are either inaccessible or unlikely to be useful to Amazon Redshift administrators\. However, you can query any catalog table or view openly if your query does not involve a join to an Amazon Redshift table\.

You can use the OID columns in the Postgres catalog tables as joining columns\. For example, the join condition `pg_database.oid = stv_tbl_perm.db_id` matches the internal database object ID for each PG\_DATABASE row with the visible DB\_ID column in the STV\_TBL\_PERM table\. The OID columns are internal primary keys that are not visible when you select from the table\. The catalog views do not have OID columns\.