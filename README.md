Fabric – Análisis_Clientes (Dataflow → Warehouse → Semantic Model → Power BI)
Overview

This project demonstrates an end-to-end analytics workflow in Microsoft Fabric: ingesting a CSV, transforming it with Dataflow Gen2 (Power Query), loading a curated table into a Fabric Warehouse, modeling it with a Direct Lake semantic model, and delivering insights through a Power BI report.

Architecture

Source CSV → Dataflow Gen2 (Power Query transformations) → Warehouse table (dbo.Analisis_Datos_Clientes) → Semantic Model (SM_Analisis_Datos_Clientes, Direct Lake on SQL) → Report (RPT_Ordenes_y_Ventas)

Dataset & Model

Core fields

NumPedido (Order ID)

Categoria, Subcategoria (Product grouping)

CantidadProductos (Units)

Precio (Unit price)

PrecioTotal (Line total / revenue per row)

Primary reporting table

WH_Análisis_Clientes.dbo.Analisis_Datos_Clientes

Transformations (Dataflow Gen2)

Transformations are implemented in Power Query (M) and exported to the repo.
Typical steps include:

Promote headers

Set/convert data types (numeric fields)

Remove blank/invalid rows

Remove duplicates

Replace values / standardize categories

Create derived columns (e.g., PrecioTotal if applicable)

KPIs (DAX measures)

The report is driven by these measures:

Revenue = SUM(PrecioTotal)

Orders = DISTINCTCOUNT(NumPedido)

Units = SUM(CantidadProductos)

Avg Order Value = Revenue / Orders

Report – “Reporte de Ordenes y Ventas”

Page 1 (Overview)

KPI cards: Revenue, Orders, Units, Avg Order Value

Revenue by Category (bar chart)

Top Subcategories by Revenue (bar chart)

Detail table for drill-down (orders + line items)

How to Reproduce (High Level)

Run Dataflow Gen2 to ingest and transform the CSV.

Confirm the output table exists in the Warehouse:

dbo.Analisis_Datos_Clientes

Create a Semantic Model:

Storage mode: Direct Lake on SQL

Table included: dbo.Analisis_Datos_Clientes

Build and save the Power BI report:

RPT_Ordenes_y_Ventas

Repository Contents

dataflow/ – Power Query (M) scripts exported from Dataflow Gen2

pipeline/ – Pipeline definition (JSON) and run evidence (if available)

sql/ – Validation queries (schema + quick data quality checks)

powerbi/ – DAX measures and/or PBIX (if export is enabled)

docs/ – Screenshots of the workflow and report

Screenshots (Evidence)

Add your images here (filenames are suggestions):

docs/01_workspace_items.png – workspace items (Dataflow, Pipeline, Warehouse, Semantic model, Report)

docs/02_dataflow_steps.png – Dataflow applied steps

docs/03_pipeline_run_succeeded.png – pipeline run status (Succeeded)

docs/04_warehouse_table.png – warehouse table preview

docs/05_report.png – final report page

Notes

Fabric GitHub integration was not available in this tenant; therefore, this repo contains exported artifacts + documentation rather than a direct workspace-to-Git sync.