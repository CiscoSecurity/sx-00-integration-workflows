.. _investigations:

Pivot into threat response
==========================


.. NOTE::
    When launching investigations from a dynamically built URL, Threat Response populates an ephermal workbench for an analyst to dig in to the observables passed in to the URL. In order for the data to be saved a user must take a snapshot or add the observables to a case.

Launch Investigation From URL
-----------------------------

URL Format
^^^^^^^^^^

Create a URL using the following format:

.. code::

    https://visibility.amp.cisco.com/investigate?q=<STRING>

.. note::

    Open the URL in a new tab when possible.

Use Cases
^^^^^^^^^

- When an easy method for launching an investigation of an observable is desired
- When there is no desire to save the list of observables

Launch Investigation From a Newly Created Casebook
--------------------------------------------------

Interacting with Casebooks is done via the ``private-intel`` URL for the selected region. For North America it is at https://private.intel.amp.cisco.com

.. note:: 

    The complete Casebook API documentation can referenced at https://private.intel.amp.cisco.com/index.html#/Casebook


Create a new casebook
^^^^^^^^^^^^^^^^^^^^^

.. note::

    Creating a casebook requires an API client with the ``casebook`` or ``private-intel`` scope

Use the following to create a new casebook:

.. code::

    POST /ctia/casebook

Example casebook JSON payload:

.. code-block:: JSON

    {
      "description": "Created via the API",
      "schema_version": "1.0.9",
      "observables": [
        {
          "value": "cisco.com",
          "type": "domain"
        }
      ],
      "type": "casebook",
      "short_description": "API Case",
      "title": "Casebook July 26, 2018 11:14 AM",
      "tlp": "amber",
      "timestamp": "2018-07-26T16:14:40.000Z"
    }

New Casebook API Example
^^^^^^^^^^^^^^^^^^^^^^^^

.. http:example::

    POST https://private.intel.amp.cisco.com/ctia/casebook HTTP/1.1
    Authorization: Bearer ${jwt}
    Content-Type: application/json

    {
      "description": "Created via the API",
      "schema_version": "1.0.9",
      "observables": [
        {
          "value": "cisco.com",
          "type": "domain"
        }
      ],
      "type": "casebook",
      "short_description": "API Case",
      "title": "Casebook July 26, 2018 11:14 AM",
      "tlp": "amber",
      "timestamp": "2018-07-26T16:14:40.000Z"
  }

JSON Response:

.. code-block:: JSON

    {
      "description": "Created via the API",
      "schema_version": "1.1.3",
      "observables": [
        {
          "value": "cisco.com",
          "type": "domain"
        }
      ],
      "type": "casebook",
      "short_description": "API Case",
      "title": "Casebook July 26, 2018 11:14 AM",
      "id": "https://private.intel.amp.cisco.com:443/ctia/casebook/casebook-25d3dd3e-661b-4b37-8588-f12685e296aa",
      "tlp": "amber",
      "client_id": "client-d71e4914-e0ed-4673-8879-5c4a44f5e3dd",
      "groups": [
        "f1631ad1-316b-438c-a055-631a63f8b6f6"
      ],
      "timestamp": "2018-07-26T16:14:40.000Z",
      "owner": "e173c521-5c58-4f90-a850-3097a89cf6b8"
    }

Save the ``.id`` in the response from the POST.

Example format of ``.id`` returned:

.. code::

    https://private.intel.amp.cisco.com:443/ctia/casebook/casebook-25d3dd3e-661b-4b37-8588-f12685e296aa

Generate the URL
^^^^^^^^^^^^^^^^

Generate the URL to link to the case using the following format:

.. code::

    https://visibility.amp.cisco.com/investigate?spid=<CASEBOOK_ID_UUID>

Example fully populated URL:

.. code::

    https://visibility.amp.cisco.com/investigate?spid=25d3dd3e-661b-4b37-8588-f12685e296aa

Only the UUID portion ``25d3dd3e-661b-4b37-8588-f12685e296aa`` is required to open a casebook for investigation. The following Python 3 example shows how to obtain the UUID from the URI based ``.id`` returned from the API

.. code::

    from os.path import basename
    from urllib.parse import urlparse

    def uuid_from_url(casebook_id_url):
        return basename(urlparse(casebook_id_url).path).replace("casebook-", "")

.. note::

    Open the URL in a new tab when possible.

Use Cases
^^^^^^^^^

- When there are more than one observables to investigate and it is impossible to generate a URL containing all of them
- When passing the observables via q= that results in a URL that is more than 2,083 characters
- When there is a desire to investigate and save observables

Launch Investigation From an Existing Casebook
----------------------------------------------

Interacting with Casebooks is done via the public-intel URL for the selected region. For North America it is at https://private.intel.amp.cisco.com

.. note:: 

    The complete Casebook API documentation can referenced at https://private.intel.amp.cisco.com/index.html#/Casebook

Search for existing casebooks
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Search for all existing casebooks using this:

.. code::

    GET /ctia/casebook/search?query=*

Get Casebook API Example
^^^^^^^^^^^^^^^^^^^^^^^^

API Endpoint Definition:

.. http:example::

    GET https://private.intel.amp.cisco.com/ctia/casebook/search HTTP/1.1
    Authorization: Bearer ${jwt}
    Content-Type: application/json

JSON Response:

.. code-block:: JSON

   [{
      "description":"This is a second example",
      "schema_version":"1.0.16",
      "observables":[
         {
            "value":"125.65.112.23",
            "type":"ip"
         },
         {
            "value":"4a54655a83b1d539c9d5b65c25d20580",
            "type":"md5"
         }
      ],
      "type":"casebook",
      "short_description":"Investigating another bad thing",
      "title":"My New Second Example Casebook",
      "id":"https://private.intel.amp.cisco.com:443/ctia/casebook/casebook-cb5988fa-4eee-46ca-9b6d-1b9be022fe79",
      "tlp":"amber",
      "groups":[
         "threatgrid:364755"
      ],
      "timestamp":"2020-04-27T20:50:14.769Z",
      "owner":"jwick"
   },
   {
      "description":"This is an example",
      "schema_version":"1.0.16",
      "observables":[
         {
            "value":"125.65.112.23",
            "type":"ip"
         },
         {
            "value":"4a54655a83b1d539c9d5b65c25d20580",
            "type":"md5"
         }
      ],
      "type":"casebook",
      "short_description":"Investigating a bad thing",
      "title":"My New Example Casebook",
      "id":"https://private.intel.amp.cisco.com:443/ctia/casebook/casebook-8b0794e2-bb9b-4ca7-b17d-93a7caa7370f",
      "tlp":"amber",
      "groups":[
         "threatgrid:364755"
      ],
      "timestamp":"2020-04-27T20:48:52.698Z",
      "owner":"jwick"
   }]

Search for a specific observable or string in the name or description of the casebook using this:

.. code::

    GET /ctia/casebook/search?query=<STRING>

Get Specific Observable API Definition
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

JSON Response when <STRING> is "Second":

.. code::

    GET /ctia/casebook/search?query=Second

.. note::

    The query parameter will return hits for the following casebook values ``.description``, ``.external_references.description``, ``.observables[].value``, ``.short_description``, and ``.title``.

Get Specific Casebook API Example
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
API Endpoint Definition:

.. http:example::

    GET https://private.intel.amp.cisco.com/ctia/casebook/search?query=second HTTP/1.1
    Authorization: Bearer ${jwt}
    Content-Type: application/json

.. code-block:: JSON

   {
      "description":"This is a second example",
      "schema_version":"1.0.16",
      "observables":[
         {
            "value":"125.65.112.23",
            "type":"ip"
         },
         {
            "value":"4a54655a83b1d539c9d5b65c25d20580",
            "type":"md5"
         }
      ],
      "type":"casebook",
      "short_description":"Investigating another bad thing",
      "title":"My New Second Example Casebook",
      "id":"https://private.intel.amp.cisco.com:443/ctia/casebook/casebook-cb5988fa-4eee-46ca-9b6d-1b9be022fe79",
      "tlp":"amber",
      "groups":[
         "threatgrid:364755"
      ],
      "timestamp":"2020-04-27T20:50:14.769Z",
      "owner":"jwick"
   }

.. note::

    - Multiple casebooks may be returned as an array. Determine a n number of casebooks to present to the user based on product capabilities.

    - For each casebook presented to the user save .[].title and .[].id for later use.


Example of ``.id`` format
^^^^^^^^^^^^^^^^^^^^^^^^^

Example format of ``.id`` returned from the POST:

.. code::

    https://private.intel.amp.cisco.com:443/ctia/casebook/casebook-25d3dd3e-661b-4b37-8588-f12685e296aa

Generating a URL
^^^^^^^^^^^^^^^^

Generate a URL using the following format:

.. code::

    https://visibility.amp.cisco.com/investigate?spid=<CASEBOOK_ID_UUID>

Example fully populated URL:

.. code::

    https://visibility.amp.cisco.com/investigate?spid=25d3dd3e-661b-4b37-8588-f12685e296aa

Only the UUID portion ``25d3dd3e-661b-4b37-8588-f12685e296aa`` is required to open a casebook for investigation. The following Python 3 example shows how to obtain the UUID from the URI based ``.id`` returned from the API

.. code::

    from os.path import basename
    from urllib.parse import urlparse

    def uuid_from_url(casebook_id_url):
        return basename(urlparse(casebook_id_url).path).replace("casebook-", "")

Present a n number of ``.[].title`` links to the user.

.. note::

    Open the URL in a new tab when possible.

Use Cases
^^^^^^^^^

- When a casebook exists with the observable you would like to investigate
- Integration built to interact with Casebooks natively (replicating what the Browser plugin or casebooks Widget do)
- Threat Hunting based on what other analysts in the organization are investigating
- Looking into casebooks to see what Observables humans may have associated with an Observable of interest but do not have a programmatic connection anywhere, i.e., an analyst has determined an email address and a mutex are part of the same campaign and has stored both in a casebook.
