Relay API
=========

Requirements
------------
All docs have to contain a schema_version field. Current version can be found at: https://github.com/threatgrid/ctim

All entities should have an id, in your case it’s a transient as it’s not something stored/accessible at some place using HTTP.
A transient is just a string, you need to concatenate transient: with an UUID. For example: transient:616608f4-7658-49f1-8728-d9a3dde849d5.

Sightings need a count field. Example can be found at https://github.com/threatgrid/ctim/blob/master/doc/structures/sighting.md#propertycount-integer

Good Practices When Possible
----------------------------

Sighting.data property, that allows you to add a semi-structured map of key-value pairs. Example can be found at https://github.com/threatgrid/ctim/blob/master/doc/structures/sighting.md#property-data--sightingdatatable-object

Put some of the Indicator explanation in the Sighting description, which is markdown. Example can be found at https://github.com/threatgrid/ctim/blob/master/doc/structures/indicator.md#property-description--markdown-string

Set resolution field to “blocked” if it was blocked. Example can be found at https://github.com/threatgrid/ctim/blob/master/doc/structures/sighting.md#property-resolution--resolution-string

If source for sighting is a distinct appliance (WAF, IDS) Sighting.sensor_object can be set to identify the specific instance that detected.
