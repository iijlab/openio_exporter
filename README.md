# OpenIO Exporter

Prometheus exporter for OpenIO metrics.

## Usage

```
usage: openio_exporter [<flags>]

Flags:
  -h, --help               Show context-sensitive help (also try --help-long and --help-man).
      --web.listen-address=":11010"
                           Address on which to expose metrics and web interface.
      --web.telemetry-path="/metrics"
                           Path under which to expose metrics.
      --openio.process-filter=.*
                           Regex that determines which processes to collect metrics. The target is GROUP column.
      --log.level=info     Only log messages with the given severity or above. One of: [debug, info, warn, error]
      --log.format=logfmt  Output format of log messages. One of: [logfmt, json]
      --version            Show application version.
```

### Example

To monitor only the `meta2` processes, run:
```
openio_exporter --openio.process-filter=meta2
```

### Prerequisites

openio_exporter runs `gridinit_cmd status` when collecting metrics, so the user runs openio_exporter must have permission to run `gridinit_cmd` and its PATH environment variable must be configured properly.

openio_exporter only supports Linux.

## Metrics

Name | Description
-----|------------
openio_process_up | Status of the process (1 = UP, 0 = DOWN).
openio_process_cpu_seconds_total | Total user and system CPU time spent in seconds.
openio_process_virtual_memory_bytes | Virtual memory size in bytes.
openio_process_resident_memory_bytes | Resident memory size in bytes.
openio_process_start_time_seconds | Start time of the process since unix epoch in seconds.

## Development

### Requirements

- Go
- Docker

### Setup the development environment

```
make setup
```

### Building and testing

```
# Build a binary
make

# Run tests
make lint       # Run `golint`
make vet        # Run `go vet`
make test       # Run `go test`
make long-test  # Run a regresssion test
```

### Debugging with a development container

```
# At first, create a container.
cd ./dev
make build && make run
cd ..

# Create a new session in the container.
make attach

# Build a binary.
make
```

```
# After detaching the session, you can stop the container with the following.
make stop
```

```
# You can also reuse the container.
make start
```

```
# If you no longer need the container, you can delete it.
cd ./dev
make rm
```

### Creating a release tar ball using [GoReleaser](https://goreleaser.com/)

```
make dist
```

## License

Copyright (c) IIJ Innovation Institute Inc.

Licensed under The 3-Clause BSD License.
