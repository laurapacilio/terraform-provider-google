---
subcategory: "Cloud (Stackdriver) Logging"
page_title: "Google: google_logging_billing_account_exclusion"
description: |-
  Manages a billing_account-level logging exclusion.
---

# google\_logging\_billing\_account\_exclusion

Manages a billing account logging exclusion. For more information see:

* [API documentation](https://cloud.google.com/logging/docs/reference/v2/rest/v2/billingAccounts.exclusions)
* How-to Guides
    * [Excluding Logs](https://cloud.google.com/logging/docs/exclusions)

~> You can specify exclusions for log sinks created by terraform by using the exclusions field of `google_logging_billing_account_sink`

## Example Usage

```hcl
resource "google_logging_billing_account_exclusion" "my-exclusion" {
  name            = "my-instance-debug-exclusion"
  billing_account = "ABCDEF-012345-GHIJKL"

  description = "Exclude GCE instance debug logs"

  # Exclude all DEBUG or lower severity messages relating to instances
  filter = "resource.type = gce_instance AND severity <= DEBUG"
}
```

## Argument Reference

The following arguments are supported:

* `billing_account` - (Required) The billing account to create the exclusion for.

* `name` - (Required) The name of the logging exclusion.

* `description` - (Optional) A human-readable description.

* `disabled` - (Optional) Whether this exclusion rule should be disabled or not. This defaults to
    false.

* `filter` - (Required) The filter to apply when excluding logs. Only log entries that match the filter are excluded.
    See [Advanced Log Filters](https://cloud.google.com/logging/docs/view/advanced-filters) for information on how to
    write a filter.

## Attributes Reference

In addition to the arguments listed above, the following computed attributes are exported:

* `id` - an identifier for the resource with format `billingAccounts/{{billing_account}}/exclusions/{{name}}`

## Import

Billing account logging exclusions can be imported using their URI, e.g.

```
$ terraform import google_logging_billing_account_exclusion.my_exclusion billingAccounts/my-billing_account/exclusions/my-exclusion
```
