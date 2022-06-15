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
* ***1. Generate an **API token** by following [this guide](https://support.pagerduty.com/docs/api-access-keys#generating-a-general-access-rest-api-key).
For Event API calls:
* ***2. Navigate to the **Automation** dropdown menu and select​​ **Event Rules**. Select the appropriate **Event** and copy the **Integration Key**.

## Installing the PagerDuty Airflow Provider

To use PagerDuty with Airflow, install the PagerDuty Provider. This can be done in one of two ways:
* ***1. Run the command `pip install apache-airflow-providers-pagerduty` on the machine running the Airflow Scheduler.
* ***2. Add `apache-airflow-providers-pagerduty` to the `requirements.txt` file.

