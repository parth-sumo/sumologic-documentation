---
id: onelogin
title: OneLogin
sidebar_label: OneLogin
description: The Sumo Logic app for OneLogin provides real-time visibility and analysis of OneLogin user activity through event data, such as user logins, administrative operations, and provisioning.
---

import useBaseUrl from '@docusaurus/useBaseUrl';

<img src={useBaseUrl('img/integrations/saml/onelogin.png')} alt="Thumbnail icon" width="50"/>

OneLogin is an Identity Management provider that supplies a comprehensive set of enterprise-grade identity and access management solutions, including single sign-on (SSO), user provisioning, and multi-factor authentication (MFA). The Sumo Logic app for OneLogin provides real-time visibility and analysis of OneLogin user activity through event data, such as user logins, administrative operations, and provisioning.

## Prerequisites

:::note
To use this feature, you'll need to enable access to your OneLogin logs and ingest them into Sumo Logic.
:::

Once you begin uploading data, your daily data usage will increase. It's a good idea to check the **Account** page in Sumo Logic to make sure that you have enough quota to accommodate additional data in your account. If you need additional quota you can [upgrade your account](/docs/manage/manage-subscription/upgrade-account/upgrade-cloud-flex-legacy-account) at any time.

* **OneLogin Enterprise** or **Unlimited** plan subscription.
* **Configure an Event Broadcaster**
   * Add a Sumo Logic [Hosted Collector](/docs/send-data/hosted-collectors/configure-hosted-collector) to your Sumo Logic Org.
   * Configure an [HTTP Source](/docs/send-data/hosted-collectors/http-source/logs-metrics) for your OneLogin data. Make sure to set the **Source Category** when configuring the OneLogin source. For example, onelogin.
   * From OneLogin, configure a broadcaster that points to this endpoint using the instructions in the [OneLogin documentation](https://onelogin.service-now.com/support?id=kb_article&sys_id=43f95543db109700d5505eea4b961959). You must use SIEM (NDJSON) format. Use the Sumo Logic HTTP Source URL as the Listener URL, and custom header is not needed.

## Log types

The Sumo Logic app for OneLogin uses event logs in NDJSON format.

## Sample log messages

Each event is a single-line JSON, containing information such as:

```json
{
	"event":{
		"create":{
			"_id":"443ce874-7704-54d2-b12f-b6e4a72ec6ef"
		},
		"entity":null,
		"role_id":null,
		"client_id":null,
		"trusted_idp_name":null,
		"notes":null,
		"app_name":null,
		"service_directory_id":null,
		"actor_system":"",
		"login_name":null,
		"assuming_acting_user_id":null,
		"mapping_name":null,
		"directory_sync_run_id":null,
		"api_credential_name":null,
		"directory_id":null,
		"certificate_id":null,
		"group_id":null,
		"role_name":null,
		"imported_user_name":null,
		"resolved_at":null,
		"mapping_id":null,
		"authentication_factor_type":null,
		"user_field_name":null,
		"proxy_ip":null,
		"certificate_name":null,
		"task_name":null,
		"adc_id":null,
		"uuid":"443ce874-7704-54d2-b12f-b6e4a72ec6ef",
		"note_title":null,
		"event_timestamp":"2017-03-21 00:09:27+0000",
		"actor_user_name":"Peyton Newton",
		"proxy_agent_id":null,
		"otp_device_name":null,
		"actor_user_id":11826257,
		"trusted_idp_id":null,
		"imported_user_id":null,
		"policy_type":null,
		"user_id":11826257,
		"resource_type_id":null,
		"login_id":null,
		"solved":null,
		"policy_id":null,
		"policy_name":null,
		"otp_device_id":null,
		"radius_config_name":null,
		"app_id":null,
		"user_name":"Peyton Newton",
		"account_id":22348,
		"resolved_by_user_id":null,
		"radius_config_id":null,
		"error_description":null,
		"note_id":null,
		"param":null,
		"event_type_id":11,
		"proxy_agent_name":null,
		"privilege_id":null,
		"user_field_id":null,
		"authentication_factor_description":null,
		"ipaddr":"137.219.197.240",
		"custom_message":null,
		"directory_name":null,
		"object_id":null,
		"group_name":null,
		"resolution":null,
		"privilege_name":null,
		"authentication_factor_id":null,
		"adc_name":null
	}
}
```

## Sample queries

```sql title="Name - Events by User"
_sourceCategory=onelogin
| json "event.event_type_id", "event.app_name","event.ipaddr", "event.user_name", "event.actor_user_name" as event_id, app_name, src_ip, user_name, actor_user_name  
| where event_id in ("10","11")
| count by user_name
| sort by _count
```

## Installing the OneLogin app

import AppInstall from '../../reuse/apps/app-install-v2.md';

<AppInstall/>

## Viewing OneLogin dashboards

import FilterDashboards from '../../reuse/filter-dashboards.md';

<FilterDashboards/>

### Overview

**Visitor Locations.** See the count and location of visitor IP addresses over the last 24 hours on the world map.

**Events by App.** See events from the last 24 hours by application name in a pie chart and compare app usage.

**Logins by Country.** See the count of number of logins by country name displayed in a table to get an idea of your visitor traffic by country in the last 24 hours.

**Event Outlier Over Time.** See the events that fall outside the normal range for the last 24 hours.

**Failed Login Outlier.** See any logins over the last 24 hours that fall outside the specified failed login threshold.

**Successful Login Outlier.** See any logins over the last 24 hours that fall outside the specified successful login threshold.

**Top 10 Users by Events.** View the top 10 users by number of events for the last 24 hours to identify heavy activity.

<img src={useBaseUrl('img/integrations/saml/OneLoginOverview.png')} alt="OneLogin" />

### App Monitoring

**Event Distribution by App.** See the percentage of events by application in the last 24 hours as a pie chart to identify the event distribution by apps having the most events recently.

**Event Distribution by Event ID.** See the percentage of each user action by Event ID for the last 24 hours as a pie chart to identify the apps having the most activity recently.

**Logins by App.** See the percentage of logins by application in the last 24 hours as a pie chart to identify the apps having the most events recently.

**Top 10 Provisioning Errors and Warnings.** See the top 10 provisioning error messages and warnings issued by OneLogin by count for the last 24 hours.

**Failed Actions.** See the error descriptions of failed actions and a count of the occurrence for the last 24 hours displayed in a table to identify possible issues.

<img src={useBaseUrl('img/integrations/saml/OneLoginAppMonitoring.png')} alt="OneLogin" />

### Security

**User Activity.** View the count of user activities by username as a bar chart for the last 24 hours as a bar chart to quickly identify unusual user activity.

**Password Changes.** See the count of password changes by username as a bar chart for the last 24 hours to quickly identify any unusually high numbers of password changes by a particular user.

**Logins by Country.** View the count of the logins by country in the last 24 hours to identify any unusual activity by country.

**Users Created in Apps.** See the number of users created in applications in the last 24 hours as a column chart. You can filter by app name to track the count of a particular app.

**Assumed Users.** View the details such as the timestamp, destination user, notes, source user, and count for the event when one user acted as another user in the last 24 hours.

**Failed Logins.** See the number of login failures by username in the last 24 hours on a bar chart to identify any unusual activity. You can filter by username as needed.

**Successful Logins.** See the number of successful logins by username in the last 24 hours to identify any unusual activity. You can filter by username as needed.

**User Modifications.** See user modifications by timestamp, destination user, source user, notes, and error description for the last 24 hours displayed in  table. You can filter by time, user name, source user, or error description as needed to track unusual behavior.

<img src={useBaseUrl('img/integrations/saml/OneLoginSecurity.png')} alt="OneLogin" />

## Upgrade/Downgrade the OneLogin app (Optional)

import AppUpdate from '../../reuse/apps/app-update.md';

<AppUpdate/>

## Uninstalling the OneLogin app (Optional)

import AppUninstall from '../../reuse/apps/app-uninstall.md';

<AppUninstall/>