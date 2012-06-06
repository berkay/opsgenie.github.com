---
layout: blogentry
title: Lamp command line utility released!
---

<p>&nbsp;</p>
<p>Lamp is a command line utility to interact with OpsGenie service. It provides capabilities to create and close alerts, attach files, etc.&nbsp;</p>
<p>Lamp is used to integrate any management tool that can execute a shell script with OpsGenie. Lamp interacts with the OpsGenie service through the RESTful Web API. Lamp has a built in contextual help system for obtaining information on available commands, and available options for their use.&nbsp;If you invoke lamp with the --help option, you will see the available list of commands. If you invoke lamp with the --help option with a specific command, you will see the options for that command.</p>
<p>The default values for the parameters can be specified in the lamp.conf file.</p>
<h3>Create Alert Request</h3>
<p>Lamp createAlert command is used to create alerts in OpsGenie. createAlert command takes the following parameters:</p>
<h4>Mandatory Parameters</h4>
<table>
<tbody>
<tr>
<th>Parameter</th>
<th>&nbsp;</th></tr>
<tr>
<td colspan="1">--customerKey</td>
<td colspan="1">
<p>Customer key used for authenticating API requests</p></td></tr>
<tr>
<td colspan="1">--message</td>
<td colspan="1"><span>Alert text limited to 130 characters</span></td></tr>
<tr>
<td colspan="1">
<p>--recipients</p></td>
<td colspan="1"><span>The user names of individual users or names of groups</span></td></tr></tbody></table>
<h4>Optional Parameters</h4>
<table>
<tbody>
<tr>
<th>Parameter</th>
<th>&nbsp;</th></tr>
<tr>
<td colspan="1">--alias</td>
<td colspan="1">
<p>A user defined identifier for the alert and there can be only one alert with open status with the same alias. Provides ability to assign a known id and later use this id to perform additional actions such as log, close, attach for the same alert.</p></td></tr>
<tr>
<td colspan="1"><span>--</span>actions</td>
<td colspan="1"><span>A comma separated list of actions that can be executed. Custom actions can be defined to enable users to execute actions for each alert. If action callback URL is specified on Settings page of customer, that callback URL will be called when action is executed.</span></td></tr>
<tr>
<td colspan="1">
<p><span>--</span>source</p></td>
<td colspan="1">Field to specify source of alert. By default, it will be assigned to IP address of incoming request</td></tr>
<tr>
<td colspan="1"><span>--</span>tags</td>
<td colspan="1"><span>A comma separated list of labels attached to the alert.</span></td></tr>
<tr>
<td colspan="1">--<span>description</span></td>
<td colspan="1">Alert text in long form. Unlike the message field, not limited to 130 characters.</td></tr>
<tr>
<td colspan="1"><span>--</span>extraprops</td>
<td colspan="1">
<p>Additional alert properties. The syntax is -D&lt;property name&gt;=&lt;property value&gt;</p></td></tr>
<tr>
<td colspan="1"><span>--</span>entity</td>
<td colspan="1">The entity the alert is related to.</td></tr></tbody></table>
<h4>Sample Usage:</h4>
<p><strong>With mandatory parameters:</strong></p>
<p>&nbsp; &nbsp; lamp createAlert --customerKey ab5454992-fabb2-4ba2-ad44f-1af65ds8b5c079 --message &quot;appserver1 down&quot; &nbsp;--recipients&nbsp;john.smith@acme.com</p>
<p><strong>With optional parameters:</strong></p>
<p>&nbsp; &nbsp; lamp createAlert --customerKey ab5454992-fabb2-4ba2-ad44f-1af65ds8b5c079 --message &quot;appserver1 down&quot;&nbsp;&nbsp;--recipients&nbsp;john.smith@acme.com&nbsp;&nbsp;--description &quot;appserver1 is not responding to requests and reported as down by the monitoring tools&quot;&nbsp;&nbsp;--tags operations, servers&nbsp;--actions acknowledge, restart&nbsp;-Dseverity=critical&nbsp;</p>
<p>&nbsp;</p>
<h3>Get Alert Request</h3>
<p>Lamp getAlert&nbsp;command is used to get alerts details from OpsGenie. getAlert command takes the following parameters:</p>
<h4>Mandatory Parameters</h4>
<table>
<tbody>
<tr>
<th>Parameter</th>
<th>&nbsp;</th></tr>
<tr>
<td colspan="1">--customerKey</td>
<td colspan="1">
<p>Customer key used for authenticating API requests</p></td></tr>
<tr>
<td colspan="1">--alertId</td>
<td colspan="1">
<p>Id of the alert that will be retrieved. Either alertId or alias must be provided</p></td></tr>
<tr>
<td colspan="1">
<p>--alias</p></td>
<td colspan="1">Alias of the alert that will be retrieved. <span> Either</span><span> alertId or alias must be provided. Alias option can only be used open alerts</span></td></tr></tbody></table>
<h4><br />Sample Usage:</h4>
<p>&nbsp; &nbsp; lamp getAlert --customerKey ab5454992-fabb2-4ba2-ad44f-1af65ds8b5c079 --alertId&nbsp;44d2e383-df30-49e1-820e-65e8e6e6387f</p>
<p>&nbsp; &nbsp; lamp getAlert --customerKey ab5454992-fabb2-4ba2-ad44f-1af65ds8b5c079 --alias appserver3Down</p>
<p>&nbsp;</p>
<h3>Attach File Request</h3>
<p>Lamp attachFile command is used to attach file to alerts in OpsGenie. attachFile command takes the following parameters:</p>
<h4>Mandatory Parameters</h4>
<table>
<tbody>
<tr>
<th>Parameter</th>
<th>&nbsp;</th></tr>
<tr>
<td colspan="1">--customerKey</td>
<td colspan="1">
<p>Customer key used for authenticating API requests</p></td></tr>
<tr>
<td colspan="1">--alertId</td>
<td colspan="1">
<p>Id of the alert that will be retrieved. Either alertId or alias must be provided</p></td></tr>
<tr>
<td colspan="1">
<p>--alias</p></td>
<td colspan="1">Alias of the alert that will be retrieved. Either alertId or alias must be provided. Alias option can only be used open alerts</td></tr>
<tr>
<td colspan="1">--file</td>
<td colspan="1">Absolute or relative path to the file</td></tr></tbody></table>
<h4><br />Sample Usage:</h4>
<p>&nbsp; &nbsp; lamp attachFile --customerKey ab5454992-fabb2-4ba2-ad44f-1af65ds8b5c079 --alertId&nbsp;44d2e383-df30-49e1-820e-65e8e6e6387f --file /tmp/lastHourCPUChart.png</p>
<p>&nbsp; &nbsp; lamp attachFile --customerKey ab5454992-fabb2-4ba2-ad44f-1af65ds8b5c079 --alias appserver3Down --file /tmp/lastHourCPUChart.png</p>
<p><strong><br /></strong></p>
<h3>Add Note Request</h3>
<p>Lamp addNote command is used to add notes to alerts in OpsGenie. addNote command takes the following parameters:</p>
<h4>Mandatory Parameters</h4>
<table>
<tbody>
<tr>
<th>Parameter</th>
<th>&nbsp;</th></tr>
<tr>
<td colspan="1">--customerKey</td>
<td colspan="1">
<p>Customer key used for authenticating API requests</p></td></tr>
<tr>
<td colspan="1">--alertId</td>
<td colspan="1">
<p>Id of the alert that will be retrieved. Either alertId or alias must be provided</p></td></tr>
<tr>
<td colspan="1">
<p>--alias</p></td>
<td colspan="1">Alias of the alert that will be retrieved. Either alertId or alias must be provided. Alias option can only be used open alerts</td></tr>
<tr>
<td colspan="1">--note</td>
<td colspan="1">Note text</td></tr></tbody></table>
<h4><br />Sample Usage:</h4>
<p>&nbsp; &nbsp; lamp addNote --customerKey ab5454992-fabb2-4ba2-ad44f-1af65ds8b5c079 --alertId&nbsp;44d2e383-df30-49e1-820e-65e8e6e6387f --note I'll work on this</p>
<p>&nbsp; &nbsp; lamp addNote --customerKey ab5454992-fabb2-4ba2-ad44f-1af65ds8b5c079 --alias appserver3Down</p>
<p>&nbsp;</p>
<h3>Close Alert Request</h3>
<p>Lamp closeAlert command is close open alerts in OpsGenie. closeAlert command takes the following parameters:</p>
<h4>Mandatory Parameters</h4>
<table>
<tbody>
<tr>
<th>Parameter</th>
<th>&nbsp;</th></tr>
<tr>
<td colspan="1">--customerKey</td>
<td colspan="1">
<p>Customer key used for authenticating API requests</p></td></tr>
<tr>
<td colspan="1">--alertId</td>
<td colspan="1">
<p>Id of the alert that will be retrieved. Either alertId or alias must be provided</p></td></tr>
<tr>
<td colspan="1">
<p>--alias</p></td>
<td colspan="1">Alias of the alert that will be retrieved. Either alertId or alias must be provided. Alias option can only be used open alerts</td></tr></tbody></table>
<h4><br />Sample Usage:</h4>
<p>&nbsp; &nbsp; lamp closeAlert --customerKey ab5454992-fabb2-4ba2-ad44f-1af65ds8b5c079 --alertId&nbsp;44d2e383-df30-49e1-820e-65e8e6e6387f&nbsp;</p>
<p>&nbsp; &nbsp; lamp closeAlert --customerKey ab5454992-fabb2-4ba2-ad44f-1af65ds8b5c079 --alias appserver3Down</p>
<p>&nbsp;</p>
<h3>Heartbeat Request</h3>
<p>Lamp heartbeat command is send periodic heartbeat messages to OpsGenie. If heartbeat monitoring is enabled and OpsGenie does not get a heartbeat message within 10 minutes, OpsGenie creates an alert to notify the specified people. heartbeat command takes the following parameters.</p>
<h4>Mandatory Parameters</h4>
<table>
<tbody>
<tr>
<th>Parameter</th>
<th>&nbsp;</th></tr>
<tr>
<td colspan="1">--customerKey</td>
<td colspan="1">
<p>Customer key used for authenticating API requests</p></td></tr></tbody></table>
<h4><br />Sample Usage:</h4>
<p>&nbsp; &nbsp; lamp heartbeat --customerKey ab5454992-fabb2-4ba2-ad44f-1af65ds8b5c079</p>
<p>&nbsp;</p>
<p>&nbsp;</p>