# proto-gen-php-rr

Generated PHP bindings (RoadRunner gRPC stubs via
[`protoc-gen-php-grpc`](https://github.com/spiral-modules/php-grpc)) for
the shared protobuf schemas defined in
[`altessa-s/proto`](https://github.com/altessa-s/proto). Do not edit
files in this repository by hand — they are regenerated and pushed
automatically on every push to `main` / `develop` and every `vX.Y.Z` tag.

For the classic `grpc/grpc` stubs, see
[`altessa-s/proto-gen-php`](https://github.com/altessa-s/proto-gen-php).

## Install (Composer, VCS-based)

```json
{
    "repositories": [
        {
            "type": "vcs",
            "url": "https://github.com/altessa-s/proto-gen-php-rr"
        }
    ],
    "require": {
        "altessa-s/proto-gen-php-rr": "^0.1"
    }
}
```

Runtime prerequisites:

- PHP 8.1+
- `spiral/roadrunner-grpc` v3+
- `google/protobuf` PHP package
- RoadRunner application server with the `grpc` plugin enabled

## Namespaces

| Proto package | PHP namespace |
|---------------|---------------|
| `io.altessa.badrequest.v1` | `Io\Altessa\Badrequest\V1` |
| `io.altessa.serviceinfo.v1` | `Io\Altessa\Serviceinfo\V1` |

Service stubs are emitted as `<Service>Interface.php` and are used both
by RoadRunner server implementations and as client contracts.

## RoadRunner configuration

The `.proto` source files are shipped under `proto/` alongside the
generated stubs because RoadRunner's gRPC plugin loads them at server
startup (its YAML `grpc.proto:` list takes file paths, not the
generated descriptors).

`.rr.yaml`:

```yaml
grpc:
  listen: tcp://0.0.0.0:9001
  proto:
    - "vendor/altessa-s/proto-gen-php-rr/proto/serviceinfo/v1/serviceinfo_service.proto"
```

`badrequest/v1/badrequest.proto` is a message-only schema and does not
need to appear in the `proto:` list.

## License

MIT — see [LICENSE](LICENSE).
