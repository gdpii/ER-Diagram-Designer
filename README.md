# ER Diagram Designer

A lightweight browser-based tool for generating a physical ER diagram from Excel-based schema definitions. It reads table metadata from worksheets, infers likely primary and foreign key relationships, and renders a visual diagram you can drag, zoom, and export.

## What it does

- Upload an Excel workbook (`.xlsx` or `.xls`)
- Treat each worksheet as a database table
- Detect likely PK/FK relationships using name and field matching
- Render the schema as an SVG diagram with draggable table nodes
- Export the diagram as an SVG file
- Include a built-in demo schema to preview the tool instantly

## Features

- Format-agnostic field matching
  - Handles names like `CustomerID`, `customer_id`, `customerid`, or `CustomerID`
  - Normalizes common naming variations to infer relationships
- Automatic relationship detection
  - Matches primary keys to foreign keys by field name and table/entity patterns
  - Supports patterns such as `customer_id` -> `Customers.CustomerID`
- Visual diagramming
  - Canvas-style SVG rendering
  - Pan and zoom controls
  - Drag table cards to reorganize the layout
- Export support
  - Save the current diagram to `physical_er_diagram.svg`

## Project structure

- `ER Diagram Designer.html` — complete single-file web application
- `Source Code v0.1` — an additional source snapshot or earlier version of the project

## How to use

### Option 1: Open directly in a browser

1. Open `ER Diagram Designer.html` in a browser.
2. Click `Upload Excel Schema (.xlsx)`.
3. Select a workbook containing one table per sheet.
4. The app will detect relationships and display the ER diagram.

### Option 2: Run with a local web server

If your browser blocks local file behavior, serve the project folder locally:

```bash
python -m http.server 8000
```

Then open:

```text
http://localhost:8000/ER%20Diagram%20Designer.html
```

## Expected Excel format

Each worksheet should represent a table. A worksheet can include columns like:

- `Field` / `field_name` / `Column`
- `DataType` / `type` / `Type`
- `KeyType` / `key` / `Key`

Example schema:

| Table | Field | DataType | KeyType |
| --- | --- | --- | --- |
| Customers | CustomerID | INT | PK |
| Customers | FullName | VARCHAR(100) |  |
| Orders | order_id | INT | PK |
| Orders | customer_id | INT |  |
| OrderItems | item_id | INT | PK |
| OrderItems | order_id | INT |  |

The app will try to infer relationships such as:

- `Customers.CustomerID` -> `Orders.customer_id`
- `Orders.order_id` -> `OrderItems.order_id`

## Demo

The app includes a built-in example schema. Click `Load Example Schema` to generate a sample ER diagram without uploading any files.

## Notes

- This project is a front-end HTML application; no build step or package installation is required.
- It uses the SheetJS library loaded from a CDN for Excel parsing.
- The diagram export is SVG-based and can be used in documentation or presentations.

## License

This project does not include an explicit license file in the repository snapshot provided here. If you plan to publish or reuse the project publicly, consider adding a license that matches your intended distribution terms.
