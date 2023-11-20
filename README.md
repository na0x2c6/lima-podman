This repository provides the templates to easily set up a [podman](https://podman.io/) runtime environment using lima. It uses the [alpine-lima](https://github.com/lima-vm/alpine-lima) image. Some settings in these templates are derived from [the original podman template](https://github.com/lima-vm/lima/blob/master/examples/podman.yaml).

## Usage

This template can be run directly. You can start rootless and rootful podman environments with the following commands:

Start the _rootless_ podman environment:

```bash
limactl start https://raw.githubusercontent.com/na0x2c6/lima-podman/main/podman.yaml
```

Start the _rootful_ podman environment:

```bash
limactl start https://raw.githubusercontent.com/na0x2c6/lima-podman/main/podman-rootful.yaml
```

If necessary, you can enable vz environments and rosetta by making the following settings in `~/.lima/_config/default.yaml` (this is just using the features of lima and lima-alpine, and nothing special is being done in this repository):

```yaml
vmType: "vz"
mountType: "virtiofs"

rosetta:
  enabled: true
  binfmt: true

networks:
  - vzNAT: true
```

You can utilize the edge version of Podman by configuring the `LIMA_ALPINE_PODMAN_REPOSITORY` environment variable as follows:

```yaml
env:
  LIMA_ALPINE_PODMAN_REPOSITORY: https://dl-cdn.alpinelinux.org/alpine/edge/community
```

## Misc

For stability, this repository includes the following features:

- Increases the version of qemu in the template script.
- Sets the podman database backend to sqlite. This was supported in podman 4.5.0.

The rootless template includes installing [pasta](https://passt.top/passt/about/) and setting [`default_rootless_network_cmd="pasta"`](https://github.com/containers/common/blob/main/docs/containers.conf.5.md#network-table).

## License

This project is licensed under the Apache License 2.0, the same as the [lima-vm project](https://github.com/lima-vm/lima).
