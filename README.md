# Microsoft Fabric Items Retrieval and Management System
- This project provides a system for efficiently retrieving Microsoft Fabric items, tracking changes over time, validating data quality, enabling incremental refreshes, and setting up alerts for significant changes. 
- The system is designed to minimize Capacity Unit usage and is implemented as a Python notebook.


- Dataflow Gen2 Exclusion: As of March 2025, Dataflow Gen2 is not included in the Fabric items retrieved by this system.
- Scope Limitation: This system only retrieves Fabric Items, not Power BI Items.
- Efficiency: Using this Python notebook consumes significantly fewer Capacity Units compared to a Spark notebook.

## Features
- Efficient Retrieval: Retrieves Microsoft Fabric items with minimal Capacity Unit usage.
- Change Tracking: Monitors and records changes in Fabric item inventory over time.
- Data Quality Validation: Ensures the integrity of retrieved items through validation checks.
- Incremental Refreshes: Supports incremental data updates to reduce processing overhead.
- Alerting System: Notifies users of significant changes in the Fabric item inventory.

## Usage

- Prerequisites: Ensure you have Python, Jupyter Notebook, and required libraries (e.g., requests, pandas, delta) installed.
- Clone the Repository: Download the project files to your local machine using git clone.
- Configure the System: Open the Jupyter notebook and adjust settings in the config dictionary (see Configuration).
- Run the Notebook: Execute the notebook to initiate the retrieval and management process.

## Configuration
The system is configured via a config dictionary in the notebook. 

Key settings include:

- API and Authentication Settings:
- key_vault_url: URL of the Azure Key Vault.
- tenant_id_secret_name: Name of the tenant ID secret in Key Vault.
- client_id_secret_name: Name of the client ID secret in Key Vault.
- client_secret_name: Name of the client secret in Key Vault.
- fabric_api_base_url: Base URL for the Fabric API.
- api_scope: Scope for API authentication.

## Storage Paths:
- raw_json_dir: Directory for storing raw JSON data.
- staging_table_path: Path for the staging Delta table.
- production_table_path: Path for the production Delta table.
- changes_table_path: Path for the changes tracking Delta table.
- history_table_path: Path for the history Delta table.
- quality_issues_path: Path for the quality issues Delta table.

## Runtime Configurations:
- incremental_refresh: Boolean to enable/disable incremental refresh (e.g., True).
- days_to_keep_history: Number of days to retain historical data (e.g., 30).
- request_delay: Delay between API requests in seconds (e.g., 0.5).
- batch_size: Number of items to process in memory at once (e.g., 1000).

## Alert Settings:
- enable_alerts: Boolean to enable/disable alerts (e.g., True).
- alert_email_recipients: List of email addresses for alerts (e.g., ["user@example.com"]).
- alert_smtp_server: SMTP server for sending alerts (e.g., smtp.example.com).
- alert_smtp_port: Port for the SMTP server (e.g., 587).
- alert_sender_email: Sender email for alerts (e.g., alerts@example.com).
- alert_threshold_item_count_change_pct: Percentage change threshold for alerts (e.g., 10).

## Data Quality Thresholds:
- min_expected_items: Minimum expected number of items (e.g., 50).
- required_fields: List of required fields (e.g., ["id", "name"]).
- valid_item_types: List of valid item types (e.g., ["table", "report"]).

## Logging
- The system logs execution details and errors to files in the Files/Logs/ directory. 
- Each run generates a log file named fabric_items_<timestamp>.log (e.g., fabric_items_20250315_123456.log).

## Alerting
-  The alerting system notifies users of significant changes in the Fabric item inventory (e.g., item count changes exceeding the threshold). Configure alerts using the enable_alerts setting and related parameters.
-  When enabled, alerts are sent via email through the specified SMTP server.

## Data Storage
- Retrieved data is stored in Delta format at the configured storage paths. Delta Lake is used for efficient storage, versioning, and history management.

##Change Tracking
- Changes in the Fabric item inventory (e.g., new, updated, or deleted items) are tracked in the fabric_items_changes table. This table provides a historical record for auditing and analysis.

## Analysis Views
- The system creates SQL views for common analysis patterns, stored as Delta tables.

Examples include:
- Usage Trends by Item Type: Tracks item type distribution over time.
- Recently Modified Items: Lists items modified recently.
- Workspace Growth: Monitors workspace size changes.
- Most Active Users: Identifies users with the most activity.
- Item Change Frequency: Analyzes how often items change.

## Unit Tests
- Unit tests are included to validate critical functions, such as data quality checks. Run these tests to ensure system reliability before deployment.

## Contributing
Contributions are welcome!

## License
This project is licensed under the MIT License. See the LICENSE file for details.
