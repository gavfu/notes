---
tags: [decoo]
title: Carbon3 Data Collection SaaS
created: '2022-12-30T03:36:09.155Z'
modified: '2022-12-30T08:59:27.785Z'
---

Carbon3 Data Collection SaaS

- [NPI](#npi)
  - [New Product Type](#new-product-type)
  - [Product Type Bom](#product-type-bom)
  - [Product Manufacturing Process](#product-manufacturing-process)
- [Product Manufacturing Data Collect & Query](#product-manufacturing-data-collect-query)
  - [PAR (Product Attribute Registration)](#par-product-attribute-registration)
  - [PGR (Product Genealogy Registration)](#pgr-product-genealogy-registration)
  - [PAQ (Product Attribute Query)](#paq-product-attribute-query)
- [Product Usage Data Collect](#product-usage-data-collect)
  - [Product Running Data](#product-running-data)
  - [Product Fueling and Charging Data](#product-fueling-and-charging-data)
  - [Product Maintainance Data](#product-maintainance-data)
- [Carbon Inventory Query](#carbon-inventory-query)
  - [Product Carbon Inventory](#product-carbon-inventory)
  - [Manufacturer Carbon Inventory](#manufacturer-carbon-inventory)


# NPI

## New Product Type

### Type

POST

### PATH

/api/v1/product_type/upsert

### Request Body

- product_type_id
- product_type_name
- manufacturer_id
- site_id
- top_level_part_number

## Product Type Bom

### Type

POST

### PATH

/api/v1/product_type/:product_type_id/bom/upsert

### Request Body

- `data`. List of:
  - part_number
  - part_name
  - parent_part_number
  - material
  - measurement


## Product Manufacturing Process

### Type

POST

### PATH

/api/v1/product_type/:product_type_id/manufacturing_process/upsert

### Request Body

- `data`. List of:
  - step_name
  - process_type
  - measurement
  - extras 


# Product Manufacturing Data Collect & Query

## PAR (Product Attribute Registration)

### Type

POST

### PATH

/api/v1/product/:serial_number/attributes/register

### Request Body

- `data`. List of:
  - serial_number
  - part_number
  - step_name
  - attribute_id
  - attribute_value
  - extras
- manufacturer_id
- site_id

## PGR (Product Genealogy Registration)

### Type

POST

### PATH

/api/v1/product/genealogy/register

### Request Body

- `data`. List of:
  - serial_number
  - parent_serial_number
- manufacturer_id
- site_id

## PAQ (Product Attribute Query)

### Type

GET

### PATH

/api/v1/product/:serial_number/attributes

### Path Params

- serial_number


# Product Usage Data Collect

## Product Running Data

### Type

POST

### PATH

/api/v1/product/:serial_number/running_data/report

### Request Body

- part_number
- start_date
- end_date
- mileage
- ghg_emission
- manufacturer_id

## Product Fueling and Charging Data

### Type

POST

### PATH

/api/v1/product/:serial_number/fueling_charging_data/report

### Request Body

- part_number
- date_time
- type
- volume
- ghg_emission
- manufacturer_id


## Product Maintainance Data

### Type

POST

### PATH

/api/v1/product/:serial_number/maintainance_data/report

### Request Body

- part_number
- date_time
- type
- ghg_emission
- manufacturer_id

# Carbon Inventory Query

## Product Carbon Inventory 

### Type

GET

### PATH

/api/v1/product/:serial_number/carbon_inventory

### Path Params

- serial_number

## Manufacturer Carbon Inventory

### Type

GET

### PATH

/api/v1/manufacturer/:manufacturer_id/carbon_inventory

### Path Params

- manufacturer_id
