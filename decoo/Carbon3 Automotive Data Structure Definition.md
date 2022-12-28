---
tags: [decoo]
title: Carbon3 Automotive Data Structure Definition
created: '2022-12-26T12:41:13.396Z'
modified: '2022-12-28T03:02:47.721Z'
---

Carbon3 Automotive Data Structure Definition

## OEM and Site

**automotive_oem**

- `id`: E.g. 'TSL'
- `name`: E.g. 'Tesla'

**automotive_site**

- `id`: E.g. 'TSLSH'
- `name`: E.g. 'Telsa Shanghai'
- `oem_id`: E.g. 'TSL'


## NPI Data

**automotive_product**

- `id`: E.g. 'MDYLR'
- `name`: E.g. 'Model Y Long Range'
- `oem_id`: E.g. 'TSL'


**automotive_product_bom**

- `product_id`
- `part_number`
- `part_name`
- `parent_part_number`
- `material`: ?
- `measurement`: ?
- `extras`: Additional information


**automotive_manufacturing_process**

- `step_name`: ?
- `process_type`: ?
- `measurement`: ?
- `extras`: Additional information


## Product Manufacturing Data

**automotive_serial_attributes**

- `serial_number`
- `part_number`
- `step_name`
- `manufacturing_attributes`: ? (Expand groups / attributes ?)
- `product_attributes`
- `site_id`
- `extras`: Additional information

**automotive_serial_genealogy**

- `serial_number`
- `item_number`: ?
- `parent_serial_number`
- `parent_item_number`: ?
- `site_id`

**automotive_manufacturing_disposal_attributes**

- `step`
- `disposal`: ?
- `manufacturing_attributes`
- `extras`: Additional information


## Product Usage Data

**automotive_running_data**

- `serial_number`
- `model`
- `start_date`
- `end_date`
- `mileage`
- `ghg_emission`

**automotive_fueling_charging_data**

- `serial_number`
- `model`
- `date_time`
- `type`
- `volume`
- `ghg_emission`

**automotive_maintenance_data**

- `serial_number`
- `model`
- `date_time`
- `type`
- `ghg_emission`


