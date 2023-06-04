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

For stability, this repository includes the following features:

- Increases the version of qemu in the template script.
- Sets the podman database backend to sqlite. This was supported in podman 4.5.0.

## License

This project is licensed under the Apache License 2.0, the same as the [lima-vm project](https://github.com/lima-vm/lima).
