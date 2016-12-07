# Terraform Docker image with extra providers included

This Terraform image is built directly on the upstream Hashicorp [Terraform image](https://hub.docker.com/r/hashicorp/terraform/) and adds the following providers:
- [localfile provider](https://github.com/bennycornelissen/terraform-provider-localfile)

## How to use
Add the following shell script as an executable script to your `PATH` or add it as a function to your shell:
```
#!/usr/bin/env sh

VERSION="<choose your version>"
IMAGE="docker.tntdigital.io/tnt/terraform:${VERSION}"

docker run --rm -ti -e TF_LOG -e TF_MODULE_DEPTH -e AWS_DEFAULT_REGION -e AWS_ACCESS_KEY_ID -e AWS_SECRET_ACCESS_KEY -e CLOUDFLARE_EMAIL -e CLOUDFLARE_TOKEN $(env | awk '/TF_VAR/ {printf "-e " $0 " "}') -v "${HOME}":"${HOME}" -w "${PWD}" "${IMAGE}" "${@}"
```
