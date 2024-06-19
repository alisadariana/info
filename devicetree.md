### Check devicetree bindings

make dt_binding_check DT_SCHEMA_FILES=<yaml_file>

### Check dtb against bindings

make CHECK_DTBS=y DT_SCHEMA_FILES=<yaml_file> <dtb_file>
