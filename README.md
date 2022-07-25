# PagerDuty + Airflow Integration Benefits

* ***Notify on-call responders based on conditions set in your DAG.***
* ***Manage the PagerDuty Events API directly for customized responses to failures and outages.***
* ***Take specific actions based on the result of Task output.***
* ***Send alerts when Sensors report late data.***
* ***Allow on-call team members to respond to Alerts within a DAG’s SLA.***

# How it Works

* ***PagerDuty API or Events API calls are created and sent in a DAG as a response to conditions set by the DAG author.***

# Requirements
***If there are requirements that user will need prior to completing the integration, list them here.
Use the current Datadog guide as an example:***
* ***The PagerDuty integration requires an [API token](https://support.pagerduty.com/docs/generating-api-keys#generating-a-general-access-rest-api-key), and if using the Events API, the routing or Integration key is also required.***

# Support

If you need help with this integration, please contact ***support@astronomer.io***

# Integration Walkthrough
## In PagerDuty
1. Generate an **API token** by following [this guide](https://support.pagerduty.com/docs/api-access-keys#generating-a-general-access-rest-api-key).
For Event API calls:
2. Navigate to the **Automation** dropdown menu and select​​ **Event Rules**. Select the appropriate **Event** and copy the **Integration Key**.
<img width="1730" alt="Screen Shot 2022-07-25 at 10 21 23 AM" src="https://user-images.githubusercontent.com/2653551/180800118-0190c09d-54db-49f2-81d9-1904befdb3f6.png">

## Installing the PagerDuty Airflow Provider

To use PagerDuty with Airflow, install the PagerDuty Provider. This can be done in one of two ways:
1. Run the command `pip install apache-airflow-providers-pagerduty` on the machine running the Airflow Scheduler.
2. Add `apache-airflow-providers-pagerduty` to the `requirements.txt` file.

## Creating a PagerDuty Connection in Airflow

1. Open the Connections tab in the Airflow UI by hovering over the `Admin` tab and selecting `Connections`.
<img width="198" alt="Screen Shot 2022-07-25 at 12 04 11 PM" src="https://user-images.githubusercontent.com/2653551/180824324-f54b7034-1aad-401e-b628-4ab4de677da0.png">
2. Press the blue plus icon to create a new connection.
<img width="591" alt="Screen Shot 2022-07-25 at 12 06 03 PM" src="https://user-images.githubusercontent.com/2653551/180824397-adcff94a-0c46-4ad9-b180-2404c5dba5e1.png">
3. In the Edit Connection window, provide a Connection ID, select `Pagerduty` as the Connection Type, and paste the previously created API token into the Pagerduty API token field. Press save.
<img width="1737" alt="Screen Shot 2022-07-25 at 12 08 10 PM" src="https://user-images.githubusercontent.com/2653551/180824732-fbf6da35-1849-4fb8-9732-7d40f0a14790.png">

## Using the PagerDuty Hook in a DAG

To use the `PagerDutyHook` in an Airflow DAG, perform the following steps in a DAG file in the `dags` folder of your Airflow project:
1. Import the appropriate hook(s) by adding the line(s):
  ```
  from airflow.providers.pagerduty.hooks.pagerduty_events import PagerdutyEventsHook
  from airflow.providers.pagerduty.hooks.pagerduty import PagerdutyHook
  ```
2. Create a PagerDuty hook instance in a `PythonOperator` using `PagerdutyHook()` and passing in a `pagerduty_conn_id` (the connection ID from the connection made in the previous step). The `token` parameter may be passed to overwrite the connection's token.
3. Call the `get_session()` and `create_event()` methods, respectively, on the hook with the appropriate parameters.
![Screen Shot 2022-07-25 at 10 41 41 AM](https://user-images.githubusercontent.com/2653551/180804315-8787fb02-b841-466c-b0e1-48a4a49ba7dd.png)

The PagerDuty event will show up in the Incidents tab on the PagerDuty website when the DAG is run.
