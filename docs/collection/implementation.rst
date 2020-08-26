++++++++++++++++++++++++++++++++
3. Collection API Implementation
++++++++++++++++++++++++++++++++
*******************************
3.1 Collection API Architecture
*******************************
The architecture of the Collection API service is illustrated in the figure below. The bottom component is the Collection API core, which includes the collection 
implementation. The service contains various REST APIs responsible for interacting with users and thus enabling collections and collection items management. 
Moreover, the service offers a graphical web frontend in order to visualize managed collections, collection items and relationships between them. The web frontend 
is available under http://{hostname}:{port}/static/overview.html. In addition, an intuitive graphical user interface will be developed in the future by SCC.

.. figure:: images/architecture.png
   :align: center
   
   Figure 1: Collection API architecture
   
**************
3.2 Data Model
**************

++++++++++++++++++++++
3.2.1 Service Features
++++++++++++++++++++++
The table below includes the different service-level features this implementation offers.

+--------------------------------------+
| serviceFeatures                      |
+======================================+
| | providesCollectionPids: false      |
| | collectionPidProviderType: null    |
| | enforcesAccess: false              |
| | supportsPagination: true           |
| | asynchronousActions: false         |
| | ruleBasedGeneration: false         |
| | maxExpansionDepth: -1              |
| | providesVersioning: false          |
| | supportedCollectionOperations: null|
| | supportedModelTypes: null          |
+--------------------------------------+

+++++++++++++++++++++++
3.2.2 Collection Object
+++++++++++++++++++++++
The service offers the possibility to create and manage collections and collection items. The figure below includes a data model of a collection, collection item and the relationship between them.

.. figure:: images/collectionDataModel.png
   :width: 650
   :align: center
   
   Figure 2: Collections and collection items

- Collection: includes the following attributes:

+----------------------+------------------------------+---------------------+---------------+
| Property Name        | Description                  | Mandatory/Optional  | Default Value |
+======================+==============================+=====================+===============+
| id                   | identifier for the collection| optional            | UUID          |
+----------------------+------------------------------+---------------------+---------------+
| description          | descriptive metadata about   | optional            | null          |
|                      | the collection               |                     |               |
+----------------------+------------------------------+---------------------+---------------+
| Collection           | define the set of actions    | optional            | –             |
| capabilities         | supported by a collection    |                     |               |
+----------------------+------------------------------+---------------------+---------------+
| Collection           | functional metadata of a     | optional            | –             |
| properties           | collection                   |                     |               |
+----------------------+------------------------------+---------------------+---------------+

1. Collection capabilities: comprise the following attributes, which determine the possible actions on a collection.

+---------------------+------------------------------+---------------------+---------------+
| Property Name       | Description                  | Mandatory/Optional  | Default Value |
+=====================+==============================+=====================+===============+
| id                  | identifier of the collection | (*)                 | –             | 
|                     | capabilities                 |                     |               |
+---------------------+------------------------------+---------------------+---------------+
| isOrdered           | identifies if the collection | optional            | false         |
|                     | items are ordered            |                     |               |
+---------------------+------------------------------+---------------------+---------------+
| appendsToEnd        | For an ordered collection,   | optional            | false         |
|                     | it indicates whether new     |                     |               |
|                     | items are appended to the end|                     |               |
+---------------------+------------------------------+---------------------+---------------+
| supportsRoles       | identifies whether a         | optional            | false         |
|                     | collection supports assigning|                     |               |
|                     | roles to its member items    |                     |               |
+---------------------+------------------------------+---------------------+---------------+
| membershipIsMutable | identifies whether a         | optional            | true          |
|                     | collection membership is     |                     |               |
|                     | mutable                      |                     |               |
+---------------------+------------------------------+---------------------+---------------+
| propertiesAreMutable| identifies whether a         | optional            | true          |
|                     | collection properties are    |                     |               |
|                     | mutable                      |                     |               |
+---------------------+------------------------------+---------------------+---------------+
| restrictedToType    | indicates the type of the    | optional            | null          |
|                     | collection items             |                     |               |
+---------------------+------------------------------+---------------------+---------------+
| maxLength           | indicates the maximum length | optional            | -1            |
|                     | of the collection            |                     |               |
+---------------------+------------------------------+---------------------+---------------+

(*) This value is automatically generated. 

2. Collection properties: include collection’s metadata.

+----------------------+------------------------------+---------------------+---------------+
| Property Name        | Description                  | Mandatory/Optional  | Default Value |
+======================+==============================+=====================+===============+
| id                   | identifier of the collection | (*)                 | –             | 
|                      | properties                   |                     |               |
+----------------------+------------------------------+---------------------+---------------+
| dateCreated          | the date the collection was  | (*)                 | –             |
|                      | created                      |                     |               |
+----------------------+------------------------------+---------------------+---------------+
| ownership            | identifies the owner of the  | optional            | null          |
|                      | collection                   |                     |               |
+----------------------+------------------------------+---------------------+---------------+
| license              | identifies the license that  | optional            | null          |
|                      | applies to the collection    |                     |               |
+----------------------+------------------------------+---------------------+---------------+
| modelType            | identifies the model that    | optional            | null          |
|                      | the collection adheres to    |                     |               |
+----------------------+------------------------------+---------------------+---------------+
| hasAccessRestrictions| indicates whether the        | optional            | true          |
|                      | collection has access        |                     |               |
|                      | restrictions                 |                     |               |
+----------------------+------------------------------+---------------------+---------------+
| memberOf             | includes a list of collection| (*)                 | –             |
|                      | identifiers to which this    |                     |               |
|                      | collection belongs           |                     |               |
+----------------------+------------------------------+---------------------+---------------+
| descriptionOntology  | identifies the ontology used | optional            | null          |
|                      | for descriptive metadata     |                     |               |
+----------------------+------------------------------+---------------------+---------------+

(*) This value is automatically generated. 

- Collection Item: In order to create a new collection item, the following attributes are expected to be given by the user:

+----------------------+---------------------------------+---------------------+---------------+
| Property Name        | Description                     | Mandatory/Optional  | Default Value |
+======================+=================================+=====================+===============+
| id                   | identifier for the member       | optional            | UUID          | 
+----------------------+---------------------------------+---------------------+---------------+
| location             | location at which the item      | mandatory           | –             |
|                      | data can be retrieved           |                     |               |
+----------------------+---------------------------------+---------------------+---------------+
| description          | human readable description      | optional            | null          |
+----------------------+---------------------------------+---------------------+---------------+
| datatype             | URI of the data type of this    | mandatory           | –             |
|                      | item. If the value of the       |                     |               |
|                      | “restrictedToType” of the       |                     |               |
|                      | collection is not null, then    |                     |               |
|                      | the datatype of the member      |                     |               |
|                      | should have the same value as   |                     |               |
|                      | the “restrictedToType”          |                     |               |
+----------------------+---------------------------------+---------------------+---------------+
| ontology             | URI of an ontology model        | optional            | null          |
|                      | class that applies to this      |                     |               |
|                      | item                            |                     |               |
+----------------------+---------------------------------+---------------------+---------------+
| mappings             | Collection item metadata        | optional            | true          |
+----------------------+---------------------------------+---------------------+---------------+

1. Mappings: include the following attributes:

+----------------------+------------------------------+---------------------+---------------+
| Property Name        | Description                  | Mandatory/Optional  | Default Value |
+======================+==============================+=====================+===============+
| role                 | the role of this item inside | optional            | null          |
|                      | the collection               |                     |               |  
+----------------------+------------------------------+---------------------+---------------+
| index                | the position of the item in  | optional            | 0             |
|                      | the collection               |                     |               |
+----------------------+------------------------------+---------------------+---------------+
| dateAdded            | the date the item was added  | (*)                 | –             |
|                      | to the collection            |                     |               |
+----------------------+------------------------------+---------------------+---------------+
| dateUpdated          | URI of the data type of this | (*)                 | –             |
|                      | the date the item’s metadata |                     |               |
|                      | were last updated            |                     |               |
+----------------------+------------------------------+---------------------+---------------+

(*) This value is automatically generated.
