# Cart Processor

![Build status](https://github.com/projectriff-demo/cart-processor/workflows/CI/badge.svg)


Build the Function:

```
riff function create cart \
  --git-repo https://github.com/projectriff-demo/cart-processor \
  --handler io.projectriff.cartprocessor.CartProcessor \
  --tail
```

Create the Streams:

```
riff streaming stream create cart-events \
    --provider franz-kafka-provisioner \
    --content-type application/json

riff streaming stream create checkout-events \
    --provider franz-kafka-provisioner \
    --content-type application/json

riff streaming stream create orders \
    --provider franz-kafka-provisioner \
    --content-type application/json
```

Create the Processor:

```
riff streaming processor create cart \
    --function-ref cart \
    --input cart-events \
    --input checkout-events \
    --output orders \
    --tail
```
