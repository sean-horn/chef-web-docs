---
resource_reference: true
resources_common_guards: true
resources_common_notification: true
resources_common_properties: true
title: powershell_package_source resource
resource: powershell_package_source
aliases:
- "/resource_powershell_package_source.html"
menu:
  infra:
    title: powershell_package_source
    identifier: chef_infra/cookbook_reference/resources/powershell_package_source
      powershell_package_source
    parent: chef_infra/cookbook_reference/resources
resource_description_list:
- markdown: Use the **powershell_package_source** resource to register a PowerShell
    package repository.
resource_new_in: '14.3'
syntax_full_code_block: |-
  powershell_package_source 'name' do
    provider_name                String # default value: "NuGet"
    publish_location             String
    script_publish_location      String
    script_source_location       String
    source_name                  String # default value: 'name' unless specified
    trusted                      true, false # default value: false
    url                          String
    action                       Symbol # defaults to :register if not specified
  end
syntax_properties_list:
syntax_full_properties_list:
- "`powershell_package_source` is the resource."
- "`name` is the name given to the resource block."
- "`action` identifies which steps Chef Infra Client will take to bring the node into
  the desired state."
- "`provider_name`, `publish_location`, `script_publish_location`, `script_source_location`,
  `source_name`, `trusted`, and `url` are the properties available to this resource."
actions_list:
  :register:
    markdown: Default. Registers and updates the PowerShell package source.
  :unregister:
    markdown: Unregisters the PowerShell package source.
  :nothing:
    shortcode: resources_common_actions_nothing.md
properties_list:
- property: provider_name
  ruby_type: String
  required: false
  default_value: NuGet
  allowed_values: '"NuGet", "PowerShellGet", "Programs", "chocolatey", "msi", "msu",
    "psl"'
  description_list:
  - markdown: The package management provider for the source.
- property: publish_location
  ruby_type: String
  required: false
  description_list:
  - markdown: The URL where modules will be published to for this source. Only valid
      if the provider is `PowerShellGet`.
- property: script_publish_location
  ruby_type: String
  required: false
  description_list:
  - markdown: The location where scripts will be published to for this source. Only
      valid if the provider is `PowerShellGet`.
- property: script_source_location
  ruby_type: String
  required: false
  description_list:
  - markdown: The URL where scripts are located for this source. Only valid if the
      provider is `PowerShellGet`.
- property: source_name
  ruby_type: String
  required: false
  default_value: The resource block's name
  description_list:
  - markdown: The name of the package source.
- property: trusted
  ruby_type: true, false
  required: false
  default_value: 'false'
  description_list:
  - markdown: Whether or not to trust packages from this source.
- property: url
  ruby_type: String
  required: true
  description_list:
  - markdown: The url to the package source.
examples:
---
