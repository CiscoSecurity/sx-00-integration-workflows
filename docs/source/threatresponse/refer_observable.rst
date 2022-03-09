Refer "Pivot" Actions
=====================

Extract Observables
^^^^^^^^^^^^^^^^^^^

.. note::

    This step can be skipped if the observable type is known and can be mapped to the `supported observables <https://github.com/threatgrid/ctim/blob/master/src/ctim/schemas/vocabularies.cljc#L254>`_ so you can build your own payload.

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

Refer Observables
^^^^^^^^^^^^^^^^^

Pass the returned array to:

.. code::

    POST /iroh/iroh-enrich/refer/observables

API Example
"""""""""""

API Endpoint Definition:

.. http:example::

    POST https://visibility.amp.cisco.com/iroh/iroh-enrich/refer/observables HTTP/1.1
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
          "id": "ref-talos-search-domain-cisco.com",
          "module": "Talos Intelligence",
          "module-type": "SenderBaseInvestigateModule",
          "title": "Search for this domain",
          "description": "Lookup this domain on Talos Intelligence",
          "url": "https://www.talosintelligence.com/reputation_center/lookup?search=cisco.com",
          "categories": [
            "Talos Intelligence",
            "Search"
          ]
        }
      ]
    }

JQ Filters for commonly used values:

- ``.data[].module``
- ``.data[].url``
- ``.data[].title``

This may return:

- ``.data[].description``

Render ``.data[].title`` link to user in a way that makes sense within the product.

.. Note::

    Open the URL in a new tab when possible.

Use Cases
^^^^^^^^^

- Get the links to pivot into products based on modules
- Streamline user experience when needing to pivot into other products
- To enable someone to pivot to the UI of a product to search for an Observable
- To enable someone to pivot to the UI of a product to lookup or browsed the information about an Observable
