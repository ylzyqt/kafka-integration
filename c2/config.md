# 2.2：config

### 1: 兼容策略

```
curl -X GET http://localhost:8081/config

修改策略的方法:

curl -X PUT -H "Content-Type: application/json" \
    --data '{"compatibility": "NONE"}' \
    http://localhost:8081/config
```

- Backward compatibility (default): A new schema is backwards compatible if it can be used to read the data written in the latest registered schema.
- Transitive backward compatibility: A new schema is transitively backwards compatible if it can be used to read the data written in all previously registered schemas. Backward compatibility is useful for loading data into systems like Hadoop since one can always query data of all versions using the latest schema.
- Forward compatibility: A new schema is forward compatible if the latest registered schema can read data written in this schema.
- Transitive forward compatibility: A new schema is transitively forward compatible if all previous schemas can read data written in this schema. Forward compatibility is useful for consumer applications that can only deal with data in a particular version that may not always be the latest version.
- Full compatibility: A new schema is fully compatible if it’s both backward and forward compatible with the latest registered schema.
- Transitive full compatibility: A new schema is transitively full compatible if it’s both backward and forward compatible with all previously registered schemas.
- No compatibility: A new schema can be any schema as long as it’s a valid Avro.

