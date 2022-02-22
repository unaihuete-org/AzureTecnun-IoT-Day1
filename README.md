## Solution architecture

Below is a diagram of the solution architecture you will build in this lab. Please study this carefully, so you understand the whole of the solution as you are working on the various components.

![Diagram of the preferred solution described in the next paragraph.](./media/preferred-solution-architecture.png 'Preferred high-level architecture')

Smart Meters are installed in buildings. They will register with a Device Provisioning Service using an attestation method through an enrollment group. Once registered and connected, messages are ingested from the Smart Meters via the IoT Hub that the Device Provisioning Service assigned to the device. A Stream Analytics job pulls telemetry messages from IoT Hub and sends the messages to two different destinations. There are two Stream Analytics jobs, one that retrieves all messages and sends them to Blob Storage (the cold path), and another that selects out only the important events needed for reporting in real time (the hot path). Data entering the hot path will be reported on using Power BI visualizations and reports. For the cold path, Azure Databricks can be used to apply the batch computation needed for the reports at scale.