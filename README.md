# Swim Calendar

Automated swim team schedule data repository. This repository stores varsity swim practice and event data that is automatically synced from the team schedule via an n8n workflow.

## Overview

The `swim-calendar-data.json` file contains structured event data for upcoming swim practices and meets, including:

- Practice times and locations
- GPS coordinates for each venue
- Event descriptions and original schedule text
- Unique identifiers for calendar integration

## Data Source

Data is automatically extracted and updated by the **Varsity Swim Schedule (Fixed Python v2)** n8n workflow, which:
- Parses the team's swim schedule
- Converts times to UTC format
- Geocodes practice locations
- Generates unique event IDs
- Updates this repository with the latest schedule

## Data Structure

```json
{
  "workflow": {
    "id": "workflow-id",
    "name": "Varsity Swim Schedule (Fixed Python v2)",
    "status": "active",
    "lastExecution": "ISO-8601-timestamp",
    "totalEvents": 12
  },
  "events": [
    {
      "summary": "Varsity Swim Practice",
      "location": "Location Name (lat,lng)",
      "locationName": "Friendly Location Name",
      "description": "Full event details",
      "startDateTime": "UTC ISO-8601",
      "endDateTime": "UTC ISO-8601",
      "date": "YYYY-MM-DD",
      "dayName": "Day abbreviation",
      "originalText": "Raw schedule text",
      "uniqueId": "varsity-swim-YYYY-MM-DD-HHMM"
    }
  ],
  "metadata": {
    "dataSource": "n8n Workflow name",
    "extractedAt": "ISO-8601-timestamp",
    "totalEvents": 12,
    "dateRange": {
      "start": "YYYY-MM-DD",
      "end": "YYYY-MM-DD"
    },
    "locations": [
      {
        "name": "Location Name",
        "code": "Location Code",
        "coordinates": "lat,lng"
      }
    ]
  }
}
```

## Known Locations

| Location Code | Name | Coordinates |
|--------------|------|-------------|
| NRCA | North Raleigh Christian Academy | 35.879750,-78.541972 |
| OPT | Optimist Aquatic Center | 35.862278,-78.643806 |
| Springdale | Springdale | 35.896361,-78.723583 |

## Time Zone

All event times are stored in UTC format. The workflow converts from Eastern Time (ET) to UTC, accounting for Daylight Saving Time transitions.

## Usage

This data can be consumed by:
- Calendar applications (Google Calendar, Apple Calendar, etc.)
- Mobile apps for team members
- Notification systems
- Location/navigation services
- Team management platforms

## Updates

The schedule is automatically updated by the n8n workflow. Check the `metadata.extractedAt` field for the last update timestamp.
