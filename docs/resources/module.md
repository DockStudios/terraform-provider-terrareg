---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "terrareg_module Resource - terraform-provider-terrareg"
subcategory: ""
description: |-
  Module resource
---

# terrareg_module (Resource)

Module resource

## Example Usage

```terraform
resource "terrareg_namespace" "this" {
  name = "example-namespace"
}
data "terrareg_git_provider" "this" {
  name = "Gitlab"
}

resource "terrareg_module" "example" {
  namespace      = terrareg_namespace.this.name
  name           = "example"
  provider_name  = "aws"

  git_provider_id = data.terrareg_git_provider.this.id
  git_tag_format  = "v{version}"
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `git_tag_format` (String) This value will be converted to the expected git tag for a module version.

The {version} placeholder will be used to generated the git tag when translating the module version to a git tag.
For example, using v{version} will translate to a git tag 'v1.1.1' for module version '1.1.1'
If the git tagging format in use does not contain a full semantic version, use placeholders {major}, {minor} and {patch}
to indicate which values are present in the tag - any missing values will be assumed to be '0'.
For example a git tag format of v{major}.{minor} would interpret a tag v1.2 as a module version 1.2.0,
where as a git tag format v{major}.{patch} would generate a version v1.0.2.

Note that if the {version} placeholder is not used, the module version import API must be provided with the git_tag argument and indexing with version argument is disabled.
- `name` (String) Module name
- `namespace` (String) Namespace of the module
- `provider_name` (String) Module provider

### Optional

- `git_path` (String) Set the path within the repository that the module exists. Defaults to the root of the repository.
- `git_provider_id` (Number) Id of the Git Repository Provider to use for the module.
Set to `null`for Custom.
(See https://github.com/MatthewJohn/terrareg/blob/main/docs/USER_GUIDE.md#git-providers)
- `repo_base_url_template` (String) This URL must be valid for browsing the base of the repository.
It may include templated values, such as: {namespace}, {module}, {provider}.
E.g. https://github.com/{namespace}/{module}-{provider}
NOTE: Setting this field will override the repository provider configuration.
- `repo_browse_url_template` (String) This URL must be valid for browsing the source code of the repository at a particular tag/path.
									  It may include templated values, such as: {namespace}, {module}, {provider}.
									  It must include the following template values: {tag} and {path}
									  E.g. https://github.com/{namespace}/{module}-{provider}/tree/{tag}/{path}
									  NOTE: Setting this field will override the repository provider configuration.
- `repo_clone_url_template` (String) This URL must be valid for cloning the repository.
It may include templated values, such as: {namespace}, {module}, {provider}.
E.g. ssh://git@github.com/{namespace}/{module}-{provider}.git
NOTE: Setting this field will override the repository provider configuration.

### Read-Only

- `id` (String) Full ID of the module

## Import

Import is supported using the following syntax:

```shell
terraform import terrareg_module.example examplenamespace/examplemodule/exampleprovider
```