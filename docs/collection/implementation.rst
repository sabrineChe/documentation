***************************
Collection API Architecture
***************************
The architecture of the Collection API service is illustrated in the figure below. The bottom component is the Collection API core, which includes the collection 
implementation. The service contains various REST APIs responsible for interacting with users and thus enabling collections and collection items management. 
Moreover, the service offers a graphical web frontend in order to visualize managed collections, collection items and relationships between them. The web frontend 
is available under http://{hostname}:{port}/static/overview.html. In addition, an intuitive graphical user interface will be developed in the future by SCC.

.. image:: images/architecture.png
   :width: 600
   
   
+---------+---------+-----------+
| 1       |  2      |  3        |
+---------+---------+-----------+
