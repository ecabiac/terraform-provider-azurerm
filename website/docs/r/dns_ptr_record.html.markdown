---
layout: "azurerm"
page_title: "Azure Resource Manager: azurerm_dns_ptr_record"
sidebar_current: "docs-azurerm-resource-dns-ptr-record"
description: |-
  Manages a DNS PTR Record.
---

# azurerm_dns_ptr_record

Enables you to manage DNS PTR Records within Azure DNS.

## Example Usage

```hcl
resource "azurerm_resource_group" "test" {
  name     = "acceptanceTestResourceGroup1"
  location = "West US"
}

resource "azurerm_dns_zone" "test" {
  name                = "mydomain.com"
  resource_group_name = "${azurerm_resource_group.test.name}"
}

resource "azurerm_dns_ptr_record" "test" {
  name                = "test"
  zone_name           = "${azurerm_dns_zone.test.name}"
  resource_group_name = "${azurerm_resource_group.test.name}"
  ttl                 = 300
  records             = ["yourdomain.com"]
}
```

## Argument Reference

The following arguments are supported:

* `name` - (Required) The name of the DNS PTR Record.

* `resource_group_name` - (Required) Specifies the resource group where the resource exists. Changing this forces a new resource to be created.

* `zone_name` - (Required) Specifies the DNS Zone where the resource exists. Changing this forces a new resource to be created.

* `ttl` - (Required) The Time To Live (TTL) of the DNS record in seconds.

* `records` - (Required) List of Fully Qualified Domain Names.

* `tags` - (Optional) A mapping of tags to assign to the resource.

## Attributes Reference

The following attributes are exported:

* `id` - The DNS PTR Record ID.

## Import

PTR records can be imported using the `resource id`, e.g.

```shell
terraform import azurerm_dns_ptr_record.test /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/mygroup1/providers/Microsoft.Network/dnszones/zone1/PTR/myrecord1
```
