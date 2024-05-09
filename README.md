# fiboa Schema

As fiboa is targeting multiple encodings, there's no single solution for validation.
We must define our own validation vocabulary, based on the fiboa Schema [data types](datatypes.md).
Nevertheless, fiboa Schema can be translated into JSON Schema.

- Schema identifier: `https://fiboa.github.io/schema/v0.1.0/schema.json`
- [Metaschema](https://fiboa.github.io/schema/v0.1.0/schema.json) (as JSON Schema)

## Vocabulary

The following keywords are generally supported:

- `type`: The [fiboa data types](datatypes.md) as a string, **required**.
- `deprecated`: Indicates whether a schema is deprecated.
- `default`: Indicates the default value of a schema.
- `description`: Describes the schema.

At the top-level, you can also indicate the schema language and version:

- `$schema`: The schema identifier, see above.

Additionally, the following validation vocabulary per data type is defined by JSON Schema.

In principle any keywords available in JSON Schema 2020-12 can be used,
but it is likely unsupported by the fiboa tooling.

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

- `items` (required, object only, sub-schema must be compliant to fiboa Schema)
- `minItems`
- `maxItems`
- `uniqueItems`

### Object data type

- `required`
- `properties` (sub-schemas must be compliant to fiboa Schema)
- `additionalProperties`
  (Note: In objects additional properties are disallowed by default, i.e. the default value is `false`.
  In JSON Schema the default value is `true`.)
- `patternProperties`
  (Note: In objects additional properties are disallowed by default, i.e. the default value is `false`.
  In JSON Schema the default value is `true`.)
- `minProperties`
- `maxProperties` (>= 1)

Either `properties`, `additionalProperties` or `patternProperties` must be provided.

### Geometry data type

- `geometryTypes` (not part of JSON Schema):
  A list of allowed geometry types.
  Any of: `Point`, `MultiPoint`, `LineString`, `MultiLineString`, `Polygon`, `MultiPolygon`