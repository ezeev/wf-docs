---
title: Release Notes 5.0
keywords:
tags: [release_notes]
sidebar: doc_sidebar
permalink: 50_release_notes.html
summary: These are the release notes for Wavefront 5.0.
---

Wavefront 5.0 introduces many new capabilities focused on improving the usability of the UI, new alert and event behaviors, enhanced integration with logs, a new installer with an improved agent as the default, new integrations, and an updated API:

## New User Interface Design

This release introduces a new user interface design as well as many new capabilities for organizing and managing your Wavefront content.

In addition to a new design, the UI adds important and useful information up front in many list views. List views have also been designed to be much clearer to read and enable faster scanning for information you are most interested in.

## Organizing, Searching, and Performing Actions

Increasingly, Wavefront customers have added more and more content such as dashboards and alerts to their systems. To make it easier for you to manage this content, this release provides many new mechanisms for organizing, searching, and performing actions on Wavefront entities.

### Tags and Tag Paths

Tags allow you to flexibly manage and organize your Wavefront content. With this release, tag paths allow you to organize your content in hierarchies that best suit your particular use of Wavefront. If desired, content can be included in multiple hierarchies to suit the needs of particular sub-groups of users. <span style="font-size: 12pt;">Tags and tag path support has been extended beyond the UI into many areas and can be leveraged in searching/filters, alerts, maintenance windows, and events. </span>

-   Tag paths organize tags by separating tag components with periods ".". For example, **Eastern.DBs.MySQL**.
-   To improve readability, tags retain case for display but are treated case-insensitive for searching, sorting etc.
-   Tags now support search and autocomplete.
-   All tags are now shared. Private tags are deprecated and are no longer supported in the Wavefront UI.

### Search

-   Faceted searching - The Dashboards, Alerts, Events, Maintenance Windows, Agents, Cloud Integrations, Web Hooks, and External Links pages now include a faceted filter bar on the left. You can search by selecting facets and typing in Search fields. In addition to the Search field at the top of each page, many facets have their own Search fields to limit the displayed facets. <span style="font-size: 12pt; font-family: arial, helvetica, sans-serif;">Most pages support the standard facets Saved Searches, Tag Paths, Tags, Last Updated By. In addition there are type-specific facets. For example, Events and Maintenance Windows have the State facet.</span>
-   Saved searches - The faceted filter bar includes a set of commonly used saved searches. In addition, you can also save your own searches. Once you start searching, the following icons [<img src="images/searchicons.png" alt="searchicons.png" class="image-20 jive-image" width="117" height="27" />](images/searchicons.png) display at the top right, allowing you to share a link to, save, and clear the search. Your saved searches appear below the commonly used searches, and have a drop-down menu for renaming, duplicating, and deleting the search.

The following Alert Browser filter demonstrates filtering alerts by the tag path **Microservice.App4**. This filters the view to show all alerts with the tag path **MicroService.App4** and all its children (for example, **MicroService.App4.Auth**). Of the matching alerts, 1 is firing.

[<img src="images/MicroService.App4-Firing.png" alt="MicroService.App4-Firing.png" class="image-15 jive-image" width="119" height="549" />](images/MicroService.App4-Firing.png)

### Metrics

Search fields now supports multi-word searches. For example, if you type **cpu usage** in the Query Builder or Metrics Browser, the drop-down list of matching metrics includes all metrics containing one or more instances of both words in any order.

### UI Patterns

This release introduces several new patterns for performing actions on Wavefront entities:

-   Tagging - After selecting entities, click the tag buttons [<img src="images/tag_toggle.png" alt="tag_toggle.png" class="image-10 jive-image" width="118" height="30" />](images/tag_toggle.png) to create, add, and remove tags.
-   Actions - Perform actions (clone, delete, edit, rename, etc.) on individual entities by clicking the menu icon:  [<img src="images/action_menu.png" alt="action_menu.png" class="image-7 jive-image" width="33" height="24" />](images/action_menu.png)  and selecting an action.
-   Trash - View deleted entities by clicking the trash toggle: Off - [<img src="images/trash_off.png" alt="trash_off.png" class="image-8 jive-image" width="76" height="30" />](images/trash_off.png)  <span style="font-size: 12pt;">On - [<img src="images/trash_on.png" alt="trash_on.png" class="image-9 jive-image" width="76" height="30" />](images/trash_on.png)</span>

## Dashboards

-   Supports sorting along many axes including number of charts and favorites, last updated, updated by, and views:

[<img src="images/dbfilter.png" alt="dbfilter.png" class="image-19 jive-image" width="139" height="152" />](images/dbfilter.png)

-   Supports defining a global event() expression in dashboard preferences and corresponding display options:

[<img src="images/dbevents.png" alt="dbevents.png" class="image-18 jive-image" width="198" height="138" />](images/dbevents.png)

-   The Landing page has been removed. The default landing page is now the **Intro: Home** dashboard. If the Default Dashboard property in user or customer preferences is empty, the landing page is **All Dashboards**.

## Alerts

Alerts have been enhanced in several aspects. Newly surfaced alert properties and filtering based on those properties streamline browsing existing alerts.  New alert behaviors reduce the cost of checking alerts and allow resending alert notifications.

-   Adds filtering by status, severity, and last updated by.
-   Shows points scanned last time alert was run, which helps with understanding and optimizing alert performance.
-   Supports setting how often an alert condition is checked. The minimum and default is 1 minute.
-   Adds the ability to resend an alert notification and set the number of minutes between notifications. The default is to not resend.

-   Maintenance windows support alert tag paths including trailing wildcards ("\*"). For example, to put all alerts in the alert hierarchy with parent alert **MicroService.App1** into maintenance, specify **MicroService.App1.\*** in the window's Alert Tags field.

## Events

-   Adds filtering by severity and source.
-   Events now support tags and tag paths. These can be used when filtering events in the UI and with the event() language.
-   User events can now be edited.
-   event() supports filtering events by alert tag paths including trailing wildcards ("\*"). For example, to view all events associated with alerts tagged with **MicroService.App1**, specify **alertTag=MicroService.App1.\***.
-   Adding a user event to a chart automatically adds the event() expression to the chart.
-   Improved documentation of the event() language, including information on previously undocumented features. See <a href="https://community.wavefront.com/docs/DOC-1159" class="jive-link-wiki-small">Advanced event() Expressions</a>.

## Sending Metrics from Logs

Metric information is frequently contained within logs. Previously, third-party solutions would be used to extract this information from logs and send it to Wavefront.  In addition to third-party solutions, the Wavefront Proxy 4.1 now makes this much easier by providing built-in capabilities to parse logs and extract metric information. Various approaches are supported, including using Filebeat to monitor log files and transmit log data to the Proxy for parsing. Splunk's Universal Forwarder is also supported.

See <a href="http://www.wavefront.com/monitoring-metamorphosis-create-metrics-log-data-wavefront/" class="jive-link-external-small">Monitoring Metamorphosis: How To Create Metrics from Log Data in Wavefront</a> and <a href="https://community.wavefront.com/docs/DOC-1217" class="jive-link-wiki-small">Sending Log Data Metrics To Wavefront</a>.

<span id="external"></span>

## External Links

When viewing metric information in a chart, anomalies or other interesting information is often noticed that requires further investigation. When this investigation requires moving to another system or tool, this release makes the process easier by providing links between Wavefront and external systems using the new external links feature.

For example, if you use logging systems such as ELK and Splunk, you can easily construct a meaningful URL to navigate from a Wavefront chart  to a log entry in one of these systems. While this example focuses on a log scenario, the feature is general <span style="font-size: 12pt;">purpose: you can link through to any type of system.</span>

External links employ a template language that allows you to pass information about metric names, source names, point tag values, and time window of the originating series to the target URL and support filtering based on metric, source, and point tag value regular expressions.

Once configured, to navigate to external link, right-click a time series and select **External Links &gt; &lt;linkName&gt;**. For example, to navigate to an ELK instance you would select

[<img src="images/elk_external_link.png" alt="elk_external_link.png" class="image-17 jive-image" width="386" height="106" />](images/elk_external_link.png)

For more information, see <a href="https://community.wavefront.com/docs/DOC-1242" class="jive-link-wiki-small">External Links</a>.

## Wavefront Installer

This release introduces a new Wavefront Proxy and agent installer named Wavefront CLI. Wavefront CLI is implemented in Python and supports Python 2.6+. In addition to installing and configuring the Wavefront Proxy and collector agent, the installer now supports integrations. For detailed information on how to install and run Wavefront CLI, see <a href="https://community.wavefront.com/docs/DOC-1246" class="jive-link-wiki-small">Wavefront CLI</a>.

### Telegraf Agent

Wavefront CLI installs <a href="http://docs.influxdata.com/telegraf/v1.1/" class="jive-link-external-small">Telegraf</a> as the collector agent instead of <span style="color: #333333;"><a href="http://collectd.org/documentation.shtml" class="jive-link-external-small">collectd</a></span>. Telegraf has a number of advantages including:

-   More complete and easier to use support for tags
-   Inclusion of plugins in the Telegraf binary
-   Simplified plugin development

Wavefront continues to support installing the collectd collector agent using the old Wavefront installer.

When you install Telegraf on an EC2 instance, the Wavefront Proxy supports tagging metrics with EC2 tags, AWS region, the VPC ID, and Image ID of the instance.

For more information on Telegraf, see <a href="http://www.wavefront.com/collectd-vs-telegraf-comparing-metric-collection-agents/" class="jive-link-external-small">Collectd vs. Telegraf: Comparing Metric Collection Agents</a>.

## New Integrations

Wavefront has added many new integrations and example dashboards. For information on each integration, see the related documentation:

-   Docker - Supports Docker containers, Amazon ECS, and Kubernetes. See <a href="https://community.wavefront.com/docs/DOC-1186" class="jive-link-wiki-small">Monitoring Docker with Wavefront</a>.
-   AWS - <a href="https://community.wavefront.com/docs/DOC-1032" class="jive-link-wiki-small">AWS Metrics Integration</a>
-   Cassandra - <a href="https://community.wavefront.com/docs/DOC-1210" class="jive-link-wiki-small">Apache Cassandra 3 Integration</a>
-   Java metrics - <a href="https://community.wavefront.com/docs/DOC-1187" class="jive-link-wiki-small">DropWizard Metrics Integration</a>
-   Puppet - <a href="https://community.wavefront.com/docs/DOC-1231" class="jive-link-wiki-small">Puppet Server Integration</a>
-   StatsD - <a href="https://community.wavefront.com/docs/DOC-1036" class="jive-link-wiki-small">Using StatsD with Wavefront</a>
-   VictorOps - <a href="https://community.wavefront.com/docs/DOC-1251" class="jive-link-wiki-small">Integrating Wavefront Alerts with VictorOps</a>

## Wavefront API

The API has been updated to support new UI features and make the method signatures consistent across all API categories. Consequently the version has been bumped up to v2. In addition, the X-AUTH-TOKEN HTTP header for authentication is deprecated. Instead, use the Authorization:Bearer HTTP header.

For example, to return all alerts using the v2 API, invoke

curl '[https://](http://)<span>&lt;Wavefront\_instance\_&gt;/api/**v2**/alert' header 'Authorization:Bearer &lt;API\_token&gt;'

While Wavefront recommends that you move to the v2 API, the original API (`<Wavefront_instance>/api/`), though deprecated, is still supported. As before, the UI leverages only the public API.

The API is now fully documented. When you open the <a href="https://community.wavefront.com/docs/DOC-1095" class="jive-link-wiki-small">API documentation</a>, the Swagger specified API appears as:

[<img src="images/Wavefront+API+v2.png" alt="Wavefront+API+v2.png" class="image-16 jive-image" width="1305" height="900" />](images/Wavefront+API+Bv2.png)

### API Categories

Wavefront has added **eight** new categories of APIs and renamed the Management category to Source. The full list of categories is:

-   **Agent** - Retrieve information about Wavefront Proxies. Users with Agent Management permission can add and remove Wavefront Proxies.
-   **Alert** - Retrieve all active, snoozed, in-maintenance, and invalid alerts. Users with Alert Management permission can create and update alerts.
-   **Cloud Integration** - Retrieve integrations. Users with Agent Management permission can add and remove integrations with cloud services.
-   **Dashboard** - Retrieve data about dashboards, list dashboards, and return version history. Users with Dashboard Management permission can save, create, delete, clone, undelete dashboards.
-   **Event** - Retrieve events and tags associated with a specific event. Users with Event Management permission can create, update, and delete events. Deleting events is limited to non-system events. System events include events based on alert firings, error events, and maintenance windows.
-   **External Link** - Navigate external links. Users with External Link Management permission can create, update, and delete external links.
-   **Maintenance Window** - Retrieve a complete or filtered list of existing maintenance windows. Users with Alert Management permission can create, close, update, and delete maintenance windows.
-   **Message** - Retrieve messages and mark messages read.
-   **Metric** - Retrieve details on a metric. Users with Metric Management permission can hide and unhide metrics.
-   **Query** - Perform queries.
-   **Saved Search** - Retrieve, add, and remove saved searches.
-   **Search** - Search agents, alerts, cloud integrations, dashboards, external links, maintenance windows, sources, and web hooks.
-   **Source** - Retrieve sources and tags associated with a source. Users with Source Tag Management permission can add and remove source tags and set descriptions.
-   **User** - Users with User Management permission can retrieve a list of all users, create, update, and delete users, and manage permissions.
-   **Webhook** - Retrieve webhooks. Users with Alert Management permission can create, update, and delete webhooks.

{% include links.html %}
