# Microsoft Fabric Items Retrieval and Management System
[![Visual Studio Code](https://custom-icon-badges.demolab.com/badge/Visual%20Studio%20Code-0078d7.svg?logo=vsc&logoColor=white)](#)
[![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=fff)](#)
[![Markdown](https://img.shields.io/badge/Markdown-%23000000.svg?logo=markdown&logoColor=white)](#)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)


This project provides two Python notebooks for retrieving and managing Microsoft Fabric items efficiently, with minimal Capacity Unit usage. The notebooks are:
1. retrieval.ipynb: A comprehensive system for retrieving Fabric items, tracking changes, validating data quality, enabling incremental refreshes, and setting up alerts.
2. simple-retrieval.ipynb: A simplified version focused on basic retrieval and storage of Fabric items in Delta format.
Both notebooks are designed to optimize resource usage compared to Spark notebooks and store data in Delta format for efficient analysis.

### Common Notes
- Dataflow Gen2 Exclusion: As of March 2025, Dataflow Gen2 is not included in the Fabric items retrieved by either notebook.
- Scope Limitation: These notebooks only retrieve Fabric Items, not Power BI Items.
- Efficiency: Using Python notebooks consumes significantly fewer Capacity Units than Spark notebooks.

## Notebooks
1. retrieval.ipynb - Comprehensive Retrieval and Management
This notebook provides a full-featured system for managing Microsoft Fabric items.

### Features
- Efficient Retrieval: Retrieves Fabric items with minimal Capacity Unit usage.
- Change Tracking: Monitors and records changes in Fabric item inventory over time.
- Data Quality Validation: Ensures data integrity through validation checks.
- Incremental Refreshes: Supports incremental updates to reduce processing overhead.
- Alerting System: Notifies users of significant changes in the Fabric item inventory.

### Usage
- Prerequisites: Install Python, Jupyter Notebook, and required libraries (e.g., requests, pandas, delta).
- Clone the Repository: Use git clone to download the project files.
- Configure the System: Adjust settings in the config dictionary within the notebook (see Configuration).
- Run the Notebook: Execute the notebook to start the retrieval and management process.

2. simple-retrieval.ipynb - **Simplified Retrieval**
- This notebook offers a streamlined approach for retrieving Fabric items, ideal for basic use cases.

### Features
- Efficient Retrieval: Retrieves all Fabric items with minimal Capacity Unit usage via the REST API.
- Data Storage: Stores results in Delta format for analysis and tracking.
- Lightweight Design: Focuses on core retrieval functionality without additional management features.

### Usage
- Prerequisites: Install Python, Jupyter Notebook, and required libraries (e.g., requests, pandas, deltalake).
- Clone the Repository: Use git clone to download the project files.
- Authenticate: Ensure Azure Key Vault secrets are accessible for authentication.
- Run the Notebook: Execute the notebook to retrieve and store Fabric items.

### Configuration
#### For retrieval.ipynb
The system is configured via a config dictionary in the notebook. Key settings include:

- API and Authentication Settings:
- key_vault_url: Azure Key Vault URL.
- tenant_id_secret_name, client_id_secret_name, client_secret_name: Secret names in Key Vault.
- fabric_api_base_url: Fabric API base URL.
- api_scope: API authentication scope.
- Storage Paths: Paths for raw JSON, staging, production, changes, history, and quality issues Delta tables.
- Runtime Configurations: Incremental refresh toggle, history retention days, request delay, batch size.
- Alert Settings: Enable alerts, email recipients, SMTP server details, change threshold.
- Data Quality Thresholds: Minimum items, required fields, valid item types.

#### For simple-retrieval.ipynb
Configuration is simpler and embedded in the code:

- Authentication: Uses Azure Key Vault for tenantid, powerbi-applicationid, and powerbi-clientsecret.
- Storage: Saves raw JSON to Files/Fabric_Items/ and Delta tables to /lakehouse/default/Tables/.

### Logging
- retrieval.ipynb: Logs execution details and errors to Files/Logs/fabric_items_<timestamp>.log.
- simple-retrieval.ipynb: Does not include dedicated logging; outputs are printed to the notebook.

### Alerting
- retrieval.ipynb: Sends email alerts for significant inventory changes (configurable via enable_alerts).
- simple-retrieval.ipynb: No alerting system included.

### Data Storage
Both notebooks store data in Delta format:

- retrieval.ipynb: Uses multiple tables (staging, production, changes, history, quality issues).
- simple-retrieval.ipynb: Stores data in staging (staging_all_fabric_items) and production (all_fabric_items) tables.

### Change Tracking
- retrieval.ipynb: Tracks changes (new, updated, deleted items) in a dedicated fabric_items_changes table.
- simple-retrieval.ipynb: Performs basic upsert operations to update the production table.

### Analysis Views
- retrieval.ipynb: Creates SQL views (e.g., usage trends, recent modifications, workspace growth).
- simple-retrieval.ipynb: No analysis views provided.

### Unit Tests
- retrieval.ipynb: Includes unit tests for critical functions like data quality checks.
- simple-retrieval.ipynb: No unit tests included.

### Contributing
Contributions are welcome! Submit pull requests or issues via GitHub.

### License
This project is licensed under the MIT License. See the LICENSE file for details.
