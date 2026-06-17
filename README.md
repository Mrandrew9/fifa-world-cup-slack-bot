# FIFA World Cup 2026 Slack Schedule Bot

Google Apps Script automation that reads FIFA World Cup 2026 match schedule data from Google Sheets and posts a formatted daily schedule to a Slack channel.

This project was built for UAT/testing and can be adapted for production use.

## Features

* Reads match schedule data from Google Sheets
* Posts daily match schedule to Slack
* Displays team flags, kickoff time, stadium, city, stage, and group
* Converts ET kickoff time to PT
* Supports a test date for validating future match days
* Includes debug and health-check functions
* Uses Slack Block Kit formatting

## Slack Output Example

```text
⚽ Today's World Cup Schedule
Tuesday, June 16, 2026

1. 🇫🇷 France vs 🇸🇳 Senegal
🕒 3:00 PM ET / 12:00 PM PT
🏟️ MetLife Stadium
📍 East Rutherford
🏷️ Group Stage — Group A
```

## Required Slack Bot Scopes

The Slack app bot needs the following OAuth scopes:

```yaml
chat:write
channels:read
groups:read
```

After adding or changing scopes, reinstall the Slack app to the workspace.

## Required Google Sheet Columns

The script expects the following column layout:

| Column | Index | Purpose         |
| ------ | ----: | --------------- |
| C      |     2 | Stage           |
| D      |     3 | Group           |
| E      |     4 | Team 1          |
| F      |     5 | Team 2          |
| H      |     7 | Kickoff Date ET |
| I      |     8 | Kickoff Time ET |
| N      |    13 | Stadium         |
| O      |    14 | City            |

The date in Column H should be formatted like:

```text
2026-06-16
```

## Configuration

Do not hard-code the Slack bot token in GitHub.

Use Apps Script Script Properties instead.

Go to:

```text
Apps Script → Project Settings → Script Properties
```

Add:

```text
SLACK_BOT_TOKEN = xoxb-your-token-here
SLACK_CHANNEL_ID = your-channel-id
SPREADSHEET_ID = your-google-sheet-id
```

## Testing

Run these functions manually from Apps Script:

```text
testSlackPost
debugSheetData
postDailyWorldCupSchedule
healthCheck
```

For testing a future match date, update this line in `Code.gs`:

```javascript
const TEST_DATE_ET = "2026-06-16";
```

For normal daily use, keep it blank:

```javascript
const TEST_DATE_ET = "";
```

## Trigger Setup

To automate the daily post:

1. Open Apps Script
2. Go to Triggers
3. Click Add Trigger
4. Select function: `postDailyWorldCupSchedule`
5. Event source: Time-driven
6. Type: Day timer
7. Pick a morning time window

## Important Security Note

Never commit a real Slack bot token to GitHub.

If a token was committed or shared publicly, rotate it immediately in Slack.
