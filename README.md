# Custom Fedora Silverblue &nbsp; [![bluebuild build badge](https://github.com/nikofabelo/fedora-silverblue-custom/actions/workflows/build.yml/badge.svg)](https://github.com/nikofabelo/fedora-silverblue-custom/actions/workflows/build.yml)

Built with [BlueBuild](https://blue-build.org) and based on the `quay.io/fedora/fedora-silverblue` image.

## Installation

To switch an existing atomic Fedora installation to the latest build:

- First rebase to the unsigned image, to get the proper signing keys and policies installed:
  ```bash
  rpm-ostree rebase ostree-unverified-registry:ghcr.io/nikofabelo/fedora-silverblue-custom:latest
  ```

- Reboot to complete the rebase:
  ```bash
  systemctl reboot
  ```

- Then switch to the signed image, like so:
  ```bash
  rpm-ostree rebase ostree-image-signed:docker://ghcr.io/nikofabelo/fedora-silverblue-custom:latest
  ```

- Reboot again to complete the installation
  ```bash
  systemctl reboot
  ```

The `latest` tag will automatically point to the latest build. That build will still always use the Fedora version specified in `recipe.yml`, so you won't get accidentally updated to the next major version.

## Verification

These images are signed with [Sigstore](https://www.sigstore.dev/)'s [cosign](https://github.com/sigstore/cosign). You can verify the signature by downloading the `cosign.pub` file from this repo and running the following command:

```bash
cosign verify --key cosign.pub ghcr.io/nikofabelo/fedora-silverblue-custom
```
