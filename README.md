# Vecorel Schema Definition Language (SDL)

As Vecorel is targeting multiple encodings, there's no single solution for validation.
We must define our own validation vocabulary, based on the Vecorel SDL [data types](datatypes.md).
Nevertheless, Vecorel SDL can be translated into JSON Schema.

- Schema identifier: <https://vecorel.org/sdl/v0.2.0/schema.json>
- [Metaschema](https://vecorel.org/sdl/v0.2.0/schema.json) (as JSON Schema)

## Vocabulary

The following keywords are generally supported:

- `type`: The [Vecorel data types](datatypes.md) as a string, **required**.
- `deprecated`: Indicates whether a schema is deprecated.
- `default`: Indicates the default value of a schema.
- `description`: Describes the schema.

At the top-level, you can also indicate the following special properties:

- `$schema`: The schema identifier, see above.
- `required`: The required properties (see `required` for objects below).
- `properties`: The schemas for the properties (see `properties` for objects below).
- `collection`: Specifies whether a property (specified as keys) must be provided only at the collection-level (`true`) or only at the feature-level (`false`). Omit any properties that can be provided at both levels.

Additionally, the following validation vocabulary per data type is defined by JSON Schema.

In principle any keywords available in JSON Schema 2020-12 can be used,
but it is likely unsupported by the Vecorel tooling.

### String data type

- `format` (values: `email`, `idn-email`, `iri`, `uri`, `uuid`)
- `pattern`
- `minLength`
- `maxLength`
- `enum`

### Numerical data type

- `minimum`
- `maximum`
- `exclusiveMinimum`
- `exclusiveMaximum`
- `enum` (for integer data types only)

### Array data type

- `items` (required, object only, sub-schema must be compliant to Vecorel SDL)
- `minItems`
- `maxItems`
- `uniqueItems`
- `contains` (sub-schema must be compliant to Vecorel SDL)

### Object data type

- `required`
- `properties` (sub-schemas must be compliant to Vecorel SDL)
- `additionalProperties`
  (Note: In objects additional properties are disallowed by default, i.e. the default value is `false`.
  In JSON Schema the default value is `true`.
  Sub-schemas must be compliant to Vecorel SDL)
- `patternProperties` (sub-schemas must be compliant to Vecorel SDL)
- `minProperties`
- `maxProperties` (>= 1)

Either `properties`, `additionalProperties` or `patternProperties` must be provided.

### Geometry data type

- `geometryTypes` (not part of JSON Schema):
  A list of allowed geometry types.
  Any of: `Point`, `MultiPoint`, `LineString`, `MultiLineString`, `Polygon`, `MultiPolygon`
