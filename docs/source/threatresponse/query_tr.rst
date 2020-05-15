Query Threat Response
=====================

Get Verdicts for an Observable
------------------------------

Extract Observables
^^^^^^^^^^^^^^^^^^^

.. note::

    This step can be skipped if the observable type is known and can be mapped to the `supported observables <https://github.com/threatgrid/ctim/blob/master/src/ctim/schemas/vocabularies.cljc#L241>`_ so you can build your own payload.

Extract observables using:

.. code::

    POST /iroh/iroh-inspect/inspect

Extract Observables API Example
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

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

Deliberate Observables
^^^^^^^^^^^^^^^^^^^^^^

Pass the returned array to:

.. code::

    POST /iroh/iroh-enrich/deliberate/observables

Deliberate Observables API Example
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

API Endpoint Definition:

.. http:example::

    POST https://visibility.amp.cisco.com/iroh/iroh-enrich/deliberate/observables HTTP/1.1
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
          "module": "Talos Intelligence",
          "module-type": "SenderBaseInvestigateModule",
          "data": {
            "verdicts": {
              "count": 1,
              "docs": [
                {
                  "type": "verdict",
                  "disposition": 1,
                  "observable": {
                    "value": "cisco.com",
                    "type": "domain"
                  },
                  "disposition_name": "Clean",
                  "valid_time": {
                    "start_time": "2020-04-28T21:55:32.572Z",
                    "end_time": "2020-05-28T21:55:32.572Z"
                  }
                }
              ]
            }
          }
        },
        {
          "module": "AMP File Reputation",
          "module-type": "POKEDeliberateModule",
          "data": {
            "verdicts": {
              "count": 0,
              "docs": []
            }
          }
        }
      ]
    }

JQ Filters for commonly used values:

- ``.data[].module``
- ``.data[].data.verdicts.docs[].observable.value``
- ``.data[].data.verdicts.docs[].disposition`` or ``.data[].data.verdicts.docs[].disposition_name``

.. note::

    `Disposition mapping <https://github.com/threatgrid/ctim/blob/master/doc/structures/verdict.md#property-disposition_name--dispositionnamestring>`_:  {1 "Clean", 2 "Malicious", 3 "Suspicious", 4 "Common", 5 "Unknown"}

JQ Filters for occasionally used values:

- ``.data[].data.verdicts.docs[].valid_time.start_time``
- ``.data[].data.verdicts.docs[].valid_time.end_time``

Entities that may be returned:

- `Verdicts <https://github.com/threatgrid/ctim/blob/master/doc/structures/verdict.md>`_

Use Cases
^^^^^^^^^

- There are a high number of observables
- Only verdicts are desired
- To reduce the number of observables
- The goal is to indicate which items merit looking into further

Contextualize an Observable
---------------------------

Extract Observables
^^^^^^^^^^^^^^^^^^^

.. note::

    This step can be skipped if the observable type is known and can be mapped to the `supported observables <https://github.com/threatgrid/ctim/blob/master/src/ctim/schemas/vocabularies.cljc#L241>`_ so you can build your own payload.

Extract observables using:

.. code::

    POST /iroh/iroh-inspect/inspect

Extract Observables API Example
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

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

Observe Observables
^^^^^^^^^^^^^^^^^^^

Pass the returned array to:

.. code::

    POST /iroh/iroh-enrich/observe/observables

Observe Observables API Example
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

API Endpoint Definition:

.. http:example::

    POST https://visibility.amp.cisco.com/iroh/iroh-enrich/observe/observables HTTP/1.1
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
          "module": "Talos Intelligence",
          "module-type": "SenderBaseInvestigateModule",
          "data": {
            "verdicts": {
              "count": 1,
              "docs": [
                {
                  "type": "verdict",
                  "disposition": 1,
                  "observable": {
                    "value": "cisco.com",
                    "type": "domain"
                  },
                  "judgement_id": "transient:f7e85f0e-2886-479c-baa4-6deb84f9bbf7",
                  "disposition_name": "Clean",
                  "valid_time": {
                    "start_time": "2020-04-28T21:58:56.926Z",
                    "end_time": "2020-05-28T21:58:56.926Z"
                  }
                }
              ]
            },
            "judgements": {
              "count": 1,
              "docs": [
                {
                  "valid_time": {
                    "start_time": "2020-04-28T21:58:56.926Z",
                    "end_time": "2020-05-28T21:58:56.926Z"
                  },
                  "schema_version": "1.0.16",
                  "observable": {
                    "value": "cisco.com",
                    "type": "domain"
                  },
                  "type": "judgement",
                  "source": "Talos Intelligence",
                  "disposition": 1,
                  "reason": "Good Talos Intelligence reputation score",
                  "source_uri": "https://www.talosintelligence.com/reputation_center/lookup?search=cisco.com",
                  "disposition_name": "Clean",
                  "priority": 90,
                  "id": "transient:f7e85f0e-2886-479c-baa4-6deb84f9bbf7",
                  "severity": "None",
                  "tlp": "white",
                  "confidence": "High"
                }
              ]
            }
          }
        }
      ]
    }

This returns the ``.data[].module`` and other pieces of data depending on the use case.

Mapping observables to some objects (attack_patterns) requires looking at the relationships and matching the IDs.

May return any of the CTIM entities:

- `Actor <https://github.com/threatgrid/ctim/blob/master/doc/structures/actor.md>`_
- `Attack Pattern <https://github.com/threatgrid/ctim/blob/master/doc/structures/attack_pattern.md>`_
- `Campaign <https://github.com/threatgrid/ctim/blob/master/doc/structures/campaign.md>`_
- `Course of Action <https://github.com/threatgrid/ctim/blob/master/doc/structures/coa.md>`_
- `Feedback <https://github.com/threatgrid/ctim/blob/master/doc/structures/feedback.md>`_
- `Incident <https://github.com/threatgrid/ctim/blob/master/doc/structures/incident.md>`_
- `Indicator <https://github.com/threatgrid/ctim/blob/master/doc/structures/indicator.md>`_
- `Judgement <https://github.com/threatgrid/ctim/blob/master/doc/structures/judgement.md>`_
- `Malware <https://github.com/threatgrid/ctim/blob/master/doc/structures/malware.md>`_
- `Relationship <https://github.com/threatgrid/ctim/blob/master/doc/structures/relationship.md>`_
- `Sighting <https://github.com/threatgrid/ctim/blob/master/doc/structures/sighting.md>`_
- `Tool <https://github.com/threatgrid/ctim/blob/master/doc/structures/tool.md>`_
- `Verdict <https://github.com/threatgrid/ctim/blob/master/doc/structures/verdict.md>`_
- `Vulnerability <https://github.com/threatgrid/ctim/blob/master/doc/structures/vulnerability.md>`_
- `Weakness <https://github.com/threatgrid/ctim/blob/master/doc/structures/weakness.md>`_

Most commonly used entities:

- Verdicts
- Sightings
- Indicators
- Judgements

.. note::

    Targets are found within the Sightings entity

Are there targets in "my" environment?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Return the ``.data[].data.sightings.docs[]?.targets`` and compare returned objects and deduplicate
to get a true unique value.
The same target can be observed for multiple observables ``.data[].data.sightings.docs[]?.observables``.

Use Cases
^^^^^^^^^

- Check for targets from within the returned sightings
- Contextualize an observable as it relates to the Global and Private Threat Intel
- Historical Incidents an Observable has been related to with
- Identify what Campaign(s) an Observable has been used in
- Find Indicators associated with an Observable
- Discover `Observed Relations <https://github.com/threatgrid/ctim/blob/master/doc/structures/sighting.md#propertyrelations-observedrelationobjectlist>`_ for an Observable
    - URLs hosted on a Domain
    - IP Addresses a Domain has resolved to
    - File Names associated with a File Hash
    - File Paths associated with a File Hash
    - Mutexes associated with a File Hash
    - URLs a File Hash was downloaded from
