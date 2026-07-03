# Warehouse Inventory API

## Project Description

The Warehouse Inventory API is a Spring Boot REST API that helps manage warehouse inventory. It allows users to add, view, update, and delete inventory items. The system also uses scheduled tasks to automatically monitor stock levels and create purchase orders when inventory is low.

Features

  Add a new inventory item
  View all inventory items
  View an item by SKU
  Update inventory information
  Delete inventory items
  Store data in a PostgreSQL database
  Run scheduled background tasks

HTTP Methods

POST
Adds a new inventory item.

GET
Returns all inventory items or a single item by SKU.

PUT
Updates an existing inventory item.

DELETE
Removes an inventory item from the warehouse.

## Scheduled Tasks

Task 1
Checks every 2 minutes for items that are below the low stock limit and creates a purchase order.

 Task 2
Checks every 5 minutes for items that are critically low and prints an alert message.

Database

The project uses PostgreSQL with Supabase.

Tables:
- inventory_item
- purchase_order

Team Members

  Eric Karanja
  Rabia Hussain
  Sameen Khan
  Akhi Alam
