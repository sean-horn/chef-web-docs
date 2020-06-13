+++
title = "azurerm_postgresql_databases resource"
draft = false

[menu]
  [menu.inspec]
    title = "azurerm_postgresql_databases"
    identifier = "inspec/resources/azurerm_postgresql_databases.md azurerm_postgresql_databases resource"
    parent = "inspec/resources"
+++


Use the `azurerm_postgresql_databases` InSpec audit resource to test properties and configuration of Azure PostgreSQL Databases.
<br />

## Azure REST API version

This resource interacts with version `2017-12-01` of the Azure Management API. For more
information see the [Official Azure Documentation](https://docs.microsoft.com/en-us/rest/api/postgresql/databases/listbyserver).

At the moment, there doesn't appear to be a way to select the version of the
Azure API docs. If you notice a newer version being referenced in the official
documentation please open an issue or submit a pull request using the updated
version.

## Availability

### Installation

This resource is available in the `inspec-azure` [resource
pack](https://www.inspec.io/docs/reference/glossary/#resource-pack). To use it, add the
following to your `inspec.yml` in your top-level profile:

    depends:
      inspec-azure:
        git: https://github.com/inspec/inspec-azure.git

You'll also need to setup your Azure credentials; see the resource pack
[README](https://github.com/inspec/inspec-azure#inspec-for-azure).

### Version

This resource first became available in 1.7.0 of the inspec-azure resource pack.

## Syntax

An `azurerm_postgresql_databases` resource block returns all Databases on a PostgreSQL Server, within a Resource Group.

    describe azurerm_postgresql_databases(resource_group: ..., server_name: ...) do
      ...
    end

<br />

## Examples

The following examples show how to use this InSpec audit resource.

### Check PostgreSQL Databases are present

    describe azurerm_postgresql_databases(resource_group: 'resource-group-1', server_name: 'production') do
      it            { should exist }
      its('names')  { should include 'my-database-name' }
    end
<br />

## Filter Criteria

* `azure_postgresql_databases` resources are filterable on all available properties. Below are some examples.

### names

Filters the results to include only those databases that match the given
name. This is a string value.

    describe azurerm_postgresql_databases(resource_group: 'rg', server_name: 'server').where{ name.eql?('production-database') } do
      it { should exist }
    end

## Attributes

- `id`
- `name`
- `type`
- `properties`

### ids
Azure resource ID.

### names
SQL Database name, e.g. `my-sql-database`.

    its('names') { should include 'my-sql-database' }

### type
The type of Resource, typically `Microsoft.Sql/servers/databases`.


### properties
A collection of additional configuration properties related to the PostgreSQL Database.

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers,
please visit our [Universal Matchers page](https://www.inspec.io/docs/reference/matchers/).

### exists

The control will pass if the filter returns at least one result. Use
`should_not` if you expect zero matches.

    describe azurerm_postgresql_databases do
      it { should exist }
    end

## Azure Permissions

Your [Service
Principal](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal)
must be setup with a `contributor` role on the subscription you wish to test.