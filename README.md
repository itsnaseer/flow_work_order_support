# Work Order Support Flow

A Salesforce-native solution designed to streamline technical, translation, and hazard support for field technicians. This project automates the creation of dedicated **Slack Support Channels** directly from a **Work Order** record to bridge the gap between the field and the back office.

📺 [https://salesforce.enterprise.slack.com/files/U029AQTEC0M/F0AEYM4L2R0/screenshare_-_2026-02-13_2_52_29_pm.mp4]|(Demo Recording) (Salesforce-internal)

## 🚀 Features

- **Contextual Support:** Automatically captures the `recordId` from Work Orders to link support requests to the correct asset.
- **Slack Automation:** Uses the "Salesforce for Slack" invocable actions to generate unique collaboration channels on the fly.
- **Dynamic Routing:** A branching Screen Flow logic that handles Technical Support, Translation requests, and Hazard reporting with specific data collection for each.
- **API v66.0 Ready:** Optimized for the latest Salesforce Spring '26 features, including modern Slack integrations.

## 🛠 Prerequisites

Before deploying, ensure the following are configured in your target org:

1. **Enable Work Orders:** Go to **Setup > Work Order Settings** and ensure Work Orders are active.
2. **Install Salesforce for Slack:** The official Slack app must be installed in your Salesforce Org and authorized to a Slack Workspace.
3. **API Version:** This project requires **API Version 66.0** or higher.

## 📦 Installation & Deployment

### 1. Clone the repository
```bash
git clone [https://github.com/itsnaseer/flow_work_order_support.git](https://github.com/itsnaseer/flow_work_order_support.git)
cd flow_work_order_support
```

### 2. Authenticate to your org
```bash
sf org login web --alias my-org
```

### 3. Deploy Metadata
```bash
sf project deploy start --manifest manifest/package.xml --target-org my-org
```

## Project Structure
* `force-app/main/default/flows/`: Source XML for the Screen Flow and Slack Subflow.
* `manifest/package.xml`: Deployment manifest listing all metadata components.
* `sfdx-project.json`: Project configuration and API versioning.

## Post-Deployment Setup
1. Activate the Flows
* Go to **Setup > Flows**
* Activate `Create_Support_Channel` (Subflow).
* Activate `WorkOrder_Support_Request` (Screen Flow).

2. Add to Record Page:
* Open any **Work Order** record.
* Click the **Gear Icon > Edit Page**.
* Drag the **Flow Component** onto the layout.
* Select `WorkOrder_Support_Request`.
* **Important**: Check the box **"Pass all field values from the record into this flow variable"** for the `recordId` variable to ensure the flow knows which Work Order it is running on.

## 📝 Troubleshooting
* **Action Not Found**: If you encounter errors regarding "Go to Record" actions, ensure you have the required navigation components installed or use the simplified version provided in the latest commit.
* **Slack Permissions**: If the Slack channel isn't creating, verify that the user running the flow has the "Salesforce for Slack" permission set assigned.