---
# ----------------------------------------------------------------------------
#
#     ***     AUTO GENERATED CODE    ***    Type: MMv1     ***
#
# ----------------------------------------------------------------------------
#
#     This file is automatically generated by Magic Modules and manual
#     changes will be clobbered when the file is regenerated.
#
#     Please read more about how to change this file in
#     .github/CONTRIBUTING.md.
#
# ----------------------------------------------------------------------------
subcategory: "Identity-Aware Proxy"
layout: "google"
page_title: "Google: google_iap_client"
sidebar_current: "docs-google-iap-client"
description: |-
  Contains the data that describes an Identity Aware Proxy owned client.
---

# google\_iap\_client

Contains the data that describes an Identity Aware Proxy owned client.

~> **Note:** Only internal org clients can be created via declarative tools. External clients must be
manually created via the GCP console. This restriction is due to the existing APIs and not lack of support
in this tool.


To get more information about Client, see:

* [API documentation](https://cloud.google.com/iap/docs/reference/rest/v1/projects.brands.identityAwareProxyClients)
* How-to Guides
    * [Setting up IAP Client](https://cloud.google.com/iap/docs/authentication-howto)

~> **Warning:** All arguments including `secret` will be stored in the raw
state as plain-text. [Read more about sensitive data in state](/language/state/sensitive-data.html).

## Example Usage - Iap Client


```hcl
resource "google_project" "project" {
  project_id = "tf-test%{random_suffix}"
  name       = "tf-test%{random_suffix}"
  org_id     = "123456789"
}

resource "google_project_service" "project_service" {
  project = google_project.project.project_id
  service = "iap.googleapis.com"
}

resource "google_iap_brand" "project_brand" {
  support_email     = "support@example.com"
  application_title = "Cloud IAP protected Application"
  project           = google_project_service.project_service.project
}

resource "google_iap_client" "project_client" {
  display_name = "Test Client"
  brand        =  google_iap_brand.project_brand.name
}
```

## Argument Reference

The following arguments are supported:


* `display_name` -
  (Required)
  Human-friendly name given to the OAuth client.

* `brand` -
  (Required)
  Identifier of the brand to which this client
  is attached to. The format is
  `projects/{project_number}/brands/{brand_id}/identityAwareProxyClients/{client_id}`.


- - -



## Attributes Reference

In addition to the arguments listed above, the following computed attributes are exported:

* `id` - an identifier for the resource with format `{{brand}}/identityAwareProxyClients/{{client_id}}`

* `secret` -
  Output only. Client secret of the OAuth client.
  **Note**: This property is sensitive and will not be displayed in the plan.

* `client_id` -
  Output only. Unique identifier of the OAuth client.


* `client_id`: The OAuth2 ID of the client.

## Timeouts

This resource provides the following
[Timeouts](/docs/configuration/resources.html#timeouts) configuration options:

- `create` - Default is 20 minutes.
- `delete` - Default is 20 minutes.

## Import


Client can be imported using any of these accepted formats:

```
$ terraform import google_iap_client.default {{brand}}/identityAwareProxyClients/{{client_id}}
$ terraform import google_iap_client.default {{brand}}/{{client_id}}
```
