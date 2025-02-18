---
uid: KI_missing_avg_trending
---

# Missing 1-day average trending records

## Affected versions

- DataMiner Main Release versions from 10.2.0 onwards
- DataMiner Feature Release versions from 10.1.10 onwards

## Cause

Day records for trending are only written into the Cassandra database if there is a TTL specified and there is an entry specifying the window size in *MaintenanceSettings.xml*.

## Fix

No fix is available yet.

## Workaround

Explicitly configure `<TimeSpan1DayRecords window="120" />` in *MaintenanceSettings.xml*. See [Trending.TimeSpan1DayRecords](xref:MaintenanceSettings_xml#trendingtimespan1dayrecords).

This will ensure that records are written into the database. However, note that this will not generate records in the past, so you may continue to see a gap in trend graphs for some time.

## Issue description

If a DMA with Cassandra database had "time to live" settings enabled for day records without using a custom window size for day records, it could occur that trend graphs did not show older data or showed a gap between the 10.2 upgrade and a timestamp equal to the current time minus the TTL for hour records.
