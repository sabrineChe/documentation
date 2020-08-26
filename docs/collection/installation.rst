============
Installation
============

Prerequisites:

* docker (tested with 19.03.8).

| You can create an instance of the collection-api service by running docker:

.. code-block:: bash

  $ docker run -d -p 8080:8080 kitdm/collection-api:latest
  
  Unable to find image 'kitdm/collection-api:latest' locally
  latest: Pulling from kitdm/collection-api
  3192219afd04: Pull complete
  17c160265e75: Pull complete
  cc4fe40d0e61: Pull complete
  9d647f502a07: Pull complete
  [...]
  Status: Downloaded newer image for kitdm/collection-api:latest
  
As soon as the microservice is started, you can browse to http://localhost:8070/swagger-ui.html in order to use the available REST APIs.
