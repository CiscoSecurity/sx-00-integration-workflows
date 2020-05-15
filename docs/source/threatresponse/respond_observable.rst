Response Actions
================

Extract Observables
^^^^^^^^^^^^^^^^^^^

.. note::

    This step can be skipped if the observable type is known and can be mapped to the `supported observables <https://github.com/threatgrid/ctim/blob/master/src/ctim/schemas/vocabularies.cljc#L241>`_ so you can build your own payload.

Extract observables using:

.. code::

    POST /iroh/iroh-inspect/inspect

API Example
"""""""""""

API Endpoint Definition:

.. http:example::

    POST https://visibility.amp.cisco.com/iroh/iroh-inspect/inspect HTTP/1.1
    Authorization: Bearer ${jwt}
    Content-Type: application/json

    {
      "content": "cisco.com"
    }

JSON Response:

.. code-block:: JSON

    [
      {
        "value": "cisco.com",
        "type": "domain"
      }
    ]

Respond Observable
^^^^^^^^^^^^^^^^^^

Pass the returned array to:

.. code::

    POST /iroh/iroh-response/respond/observables

API Example
"""""""""""

API Endpoint Definition:

.. http:example::

    POST https://visibility.amp.cisco.com/iroh/iroh-response/respond/observables HTTP/1.1
    Authorization: Bearer ${jwt}
    Content-Type: application/json

    [
      {
        "value": "cisco.com",
        "type": "domain"
      }
    ]

JSON Response:

.. code-block:: JSON

    {
      "data": [
        {
          "module": "Umbrella",
          "module_instance_id": "b56d3882-37d8-4c0c-af22-a5ef0cf53bd3",
          "module_type_id": "188d70f7-29d5-5069-9098-d83a3ec8e797",
          "id": "block",
          "title": "Block this domain",
          "description": "Block this domain using Umbrella Enforcement API",
          "url": "/respond/trigger/b56d3882-37d8-4c0c-af22-a5ef0cf53bd3/block?observable_type=domain&observable_value=cisco.com"
        }
      ]
    }

JQ Filters for commonly used values:

- ``.data[].module``
- ``.data[].title``
- ``.data[].url``

Render ``.data[].title`` link to user in a way that makes sense within the product. When this is
clicked authenticate using a token.

For example:

Example with parameters:
``<a href="{{host}} + {{$.data[].url}}">{{.data[].title}}</a>``

Example with parameter substitution:
``<a href="https://visibility.amp.cisco.com/respond/trigger/b56d3882-37d8-4c0c-af22-a5ef0cf53bd3/block?observable_type=domain&observable_value=cisco.com">Block this domain</a>``