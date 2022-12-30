---
tags: [decoo]
title: Carbon3 Automotive Data Structure Definition
created: '2022-12-26T12:41:13.396Z'
modified: '2022-12-30T08:46:54.280Z'
---

Carbon3 Automotive Data Structure Definition

- [OEM and Site](#oem-and-site)
- [NPI Data](#npi-data)
- [Product Manufacturing Data](#product-manufacturing-data)
- [Product Usage Data](#product-usage-data)
- [Carbon Inventory](#carbon-inventory)

## Manufacturers and Sites

**automotive_manufacturers**

- `id`: E.g. 'NIO'、'TSL'
- `name`: E.g. 'NIO'、'Telsa'
- `type`: 'OEM' / 'Supplier'
- `created_at`
- `last_updated_at`

**automotive_sites**

- `id`: E.g. 'JAC'
- `name`: E.g. 'JAC Hefei'
- `created_at`
- `last_updated_at`


**automotive_manufacturer_sites**

- `manufacture_id`: E.g. 'NIO'
- `site_id`: E.g. 'JAC'
- `created_at`
- `last_updated_at`


## NPI Data

**automotive_product_type**

- `product_type_id`: E.g. 'ES8P'
- `product_type_name`: E.g. 'ES8 Prime'
- `manufacturer_id`: E.g. 'NIO'
- `site_id`: E.g. 'JAC'
- `top_level_part_number`: Top level part number of a product
- `created_at`
- `last_updated_at`


**automotive_product_type_bom**

- `part_number`
- `part_name`
- `parent_part_number`
- `material`: (Enum type, need define)
- `measurement`: (Enum, need define)
- `extras`: Additional information
- `created_at`
- `last_updated_at`


**automotive_product_manufacturing_process**

- `top_level_part_number`: Top level part number of a product
- `step_name`
- `process_type`: (Enum type, need define)
- `measurement`: (Enum type, need define)
- `extras`: Additional information
- `created_at`
- `last_updated_at`


### Attributes


**automotive_attribute_groups**

- `attribute_group_id`
- `attribute_group_name`
- `attribute_group_description`
- `attribute_group_type`: Manufacturing / Disposal / Running / Fueling / Charging / Maintainance / ...
- `is_enabled`: Whether this group is enabled
- `created_at`
- `last_updated_at`


**automotive_attributes**

- `attribute_id`
- `attribute_name`: E.g. 'COO', 'ROHS', 'Manufacturing Complete', etc
- `attribute_type`: Boolean / Num / Text / Enum / Image
- `attribute_description`
- `group_id`: One attribute could belong to at most one group
- `is_enabled`
- `created_at`
- `last_updated_at`


## Product Manufacturing Data

**automotive_serial_attributes**

- `serial_number`
- `part_number`
- `step_name`
- `attribute_id`
- `attribute_value`
- `extras`: Additional information
- `manufacturer_id`: E.g. 'NIO'
- `site_id`: E.g. 'JAC'
- `created_at`
- `last_updated_at`

**automotive_serial_numbers**

- `serial_number`
- `top_level_part_number`
- `is_disposed`
- `manufacturer_id`: E.g. 'NIO'
- `site_id`: E.g. 'JAC'
- `backflushed`
- `created_at`
- `last_updated_at`

**automotive_serial_genealogy**

- `serial_number`
- `parent_serial_number`
- `manufacturer_id`: E.g. 'NIO'
- `site_id`: E.g. 'JAC'
- `created_at`
- `last_updated_at`

**automotive_engergy_spending**

- `engergy_spending_type`
- `engergy_spending_value`
- `manufacturer_id`: E.g. 'NIO'
- `site_id`: E.g. 'JAC'
- `start_date`
- `end_date`
- `created_at`
- `last_updated_at`

**automotive_hr_operation_data**

- `hr_operation_type`
- `hr_operation_value`: In human count
- `manufacturer_id`: E.g. 'NIO'
- `site_id`: E.g. 'JAC'
- `start_date`
- `end_date`
- `created_at`
- `last_updated_at`


## Product Usage Data

**automotive_running_data**

- `serial_number`
- `part_number`
- `start_date`
- `end_date`
- `mileage`
- `ghg_emission`
- `manufacturer_id`
- `created_at`
- `last_updated_at`


**automotive_fueling_charging_data**

- `serial_number`
- `part_number`
- `date_time`
- `type`
- `volume`
- `ghg_emission`
- `manufacturer_id`
- `created_at`
- `last_updated_at`


**automotive_maintenance_data**

- `serial_number`
- `part_number`
- `date_time`
- `type`
- `ghg_emission`
- `manufacturer_id`
- `created_at`
- `last_updated_at`


## Carbon Inventory

**product_carbon_inventory**

- `serial_number`
- `top_level_part_number`
- `ghg_emission_manufacturing_bom`
- `ghg_emission_manufacturing_process`
- `ghg_emission_hr_operation`
- `manufacturer_id`
- `created_at`
- `last_updated_at`

**manufacturer_carbon_inventory**

- `manufacturer_id`
- `ghg_emission_scope1`
- `ghg_emission_scope2`
- `ghg_emission_scope3`
- `ghg_emission_plc`
- `created_at`
- `last_updated_at`


