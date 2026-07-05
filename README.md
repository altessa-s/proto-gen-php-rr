# proto-gen-php-rr

Generated PHP bindings (RoadRunner gRPC stubs via
[`spiral/roadrunner-grpc`](https://github.com/roadrunner-server/roadrunner-grpc))
for the [altessa-s/proto](https://github.com/altessa-s/proto) schema.

This repository is auto-generated. Do not edit its files by hand — they are
regenerated from [`altessa-s/proto`](https://github.com/altessa-s/proto) and
pushed automatically on every push to `main` / `develop` and every `vX.Y.Z`
tag. The only hand-maintained file is this `README.md`.

For the classic `grpc/grpc` stubs, see
[`altessa-s/proto-gen-php`](https://github.com/altessa-s/proto-gen-php).

## Installation

Composer, VCS-based:

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
- `spiral/roadrunner-grpc` (`^3.0`)
- `google/protobuf` (`^3.25 || ^4.0`)
- `google/common-protos` (`^4.0`)
- RoadRunner application server with the `grpc` plugin enabled

## Packages

Classes are PSR-4 autoloaded under the `Io\Altessa\` prefix. Service stubs are
emitted as `<Service>Interface.php`, used both by RoadRunner server
implementations and as client contracts.

| Proto package | PHP namespace | Description |
|---|---|---|
| `io.altessa.badrequest.v1` | `Io\Altessa\Badrequest\V1` | `BadRequest` / `FieldViolation` error-detail payload for a `google.rpc.Status` with `INVALID_ARGUMENT`. |
| `io.altessa.serviceinfo.v1` | `Io\Altessa\Serviceinfo\V1` | `ServiceInfo` runtime metadata plus the `ServiceInfoService.GetServiceInfo` introspection RPC. |
| `io.altessa.type.v1` | `Io\Altessa\Type\V1` | General-purpose, domain-neutral value types (`Contact`, `DatePeriod`, `FileRef`, …) reused across services. |

## Usage

Implement the generated service interface on your RoadRunner worker:

```php
use Io\Altessa\Serviceinfo\V1\ServiceInfoServiceInterface;
use Io\Altessa\Serviceinfo\V1\GetServiceInfoRequest;
use Io\Altessa\Serviceinfo\V1\GetServiceInfoResponse;
use Io\Altessa\Serviceinfo\V1\ServiceInfo;
use Spiral\RoadRunner\GRPC\ContextInterface;

final class ServiceInfoService implements ServiceInfoServiceInterface
{
    public function GetServiceInfo(
        ContextInterface $ctx,
        GetServiceInfoRequest $in,
    ): GetServiceInfoResponse {
        $info = (new ServiceInfo())
            ->setServiceName('billing-api')
            ->setFullVersion('1.4.2+build.873');

        return (new GetServiceInfoResponse())->setServiceInfo($info);
    }
}
```

## RoadRunner configuration

The `.proto` source files are shipped under `proto/` alongside the generated
stubs because RoadRunner's gRPC plugin loads them at server startup (its YAML
`grpc.proto:` list takes file paths, not the generated descriptors).

`.rr.yaml`:

```yaml
grpc:
  listen: tcp://0.0.0.0:9001
  proto:
    - "vendor/altessa-s/proto-gen-php-rr/proto/io/altessa/serviceinfo/v1/serviceinfo_service.proto"
```

`io/altessa/badrequest/v1/badrequest.proto` and the value types under
`io/altessa/type/v1/` are message-only schemas and do not need to appear in the
`proto:` list.

## Versioning

Versions track [`altessa-s/proto`](https://github.com/altessa-s/proto): a
`vX.Y.Z` tag on the schema repo produces the same release here, and the
`main` / `develop` branches follow the matching schema branches.

## Contributing

This repository contains generated output only. To change what appears here,
edit the schemas or generation config in
[`altessa-s/proto`](https://github.com/altessa-s/proto); the next sync
regenerates and republishes these bindings.

## License

MIT — see [LICENSE](LICENSE).
