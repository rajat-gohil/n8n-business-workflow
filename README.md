# n8n Customer Support Ticket Automation

An automated customer support notification workflow built using n8n, Google Sheets, and Gmail. The workflow detects newly added support tickets, evaluates their priority, and sends email notifications for high-priority and urgent issues.

## Project Overview

Customer support teams need to identify important tickets quickly without manually checking every new entry in a spreadsheet.

This project automates that process by connecting Google Sheets to n8n and Gmail. It demonstrates how workflow automation can reduce repetitive monitoring and help teams respond to important issues.

## Business Problem

Manually monitoring a support spreadsheet can delay responses to urgent customer issues.

This workflow automatically evaluates each new ticket and sends an email alert when its priority requires attention.

## Features

- Detects newly added rows in Google Sheets.
- Evaluates ticket priority using conditional logic.
- Sends Gmail notifications for High- and Urgent-priority tickets.
- Skips notifications for lower-priority tickets.
- Supports visual workflow monitoring and execution history.
- Includes an exportable n8n workflow JSON file.

## Technology Stack

- **n8n:** Workflow automation and conditional logic.
- **Google Sheets:** Support ticket data source.
- **Gmail:** Email notification delivery.
- **JSON:** Workflow export and configuration.

## Workflow Architecture

```text
Google Sheets
     |
     v
Detect New Ticket
     |
     v
IF: Priority = High OR Urgent
     |
     +------ True ------> Gmail: Send Notification
     |
     +------ False -----> No Action
```

## Ticket Data Structure

The Google Sheets worksheet uses the following columns:

| Column | Description |
|---|---|
| Ticket ID | Unique ticket identifier |
| Customer | Customer name |
| Email | Customer email address |
| Issue | Description of the support issue |
| Priority | High, Urgent, Medium, or Low |
| Status | Current ticket status |

The workflow evaluates the Priority field when a new row is detected.

## How It Works

1. A new support ticket is added to the Google Sheets worksheet.
2. The Google Sheets trigger detects the new row.
3. The IF node checks whether the priority is High or Urgent.
4. If the condition is true, Gmail sends a notification containing the ticket details.
5. If the condition is false, the workflow ends without sending an email.

The trigger uses polling, so notifications may not be instantaneous.

## Setup Instructions

### Prerequisites

- An n8n instance.
- A Google account with access to Google Sheets.
- A Gmail account authorized for sending notifications.

### 1. Prepare the spreadsheet

Create a Google spreadsheet named `Customer Ticket Tracker` and a worksheet named `Tickets`.

Add the following headers:

`Ticket ID`, `Customer`, `Email`, `Issue`, `Priority`, `Status`

### 2. Import the workflow

1. Open your n8n instance.
2. Create a new workflow or open the workflow editor.
3. Use the workflow menu to import `workflow.json`.
4. Configure the Google Sheets and Gmail credentials in your own n8n instance.
5. Select your spreadsheet and worksheet.
6. Verify that the IF node evaluates the correct Priority field.

### 3. Configure and test

Add a new ticket with High priority and verify that an email notification is sent.

Add another ticket with Low priority and verify that no email is sent.

### 4. Activate the workflow

After successful testing, save and activate the workflow. Ensure that the n8n instance remains available for automatic execution.

## Testing

| Test Case | Expected Result |
|---|---|
| New High-priority ticket | Email notification sent |
| New Urgent-priority ticket | Email notification sent |
| New Medium-priority ticket | No email notification |
| New Low-priority ticket | No email notification |

Actual results should be confirmed in the n8n execution history and the recipient's inbox.

## Screenshots

### Workflow Overview

![Workflow overview](screenshots/workflow-overview.png)

### Successful Execution

![Successful execution](screenshots/successful-execution.png)

## Limitations

- Trigger execution depends on the configured polling interval.
- The n8n instance must remain available for the workflow to run.
- Google and Gmail credentials must be configured separately when importing the workflow.
- The current implementation does not include retries, duplicate-ticket detection, or automatic ticket status updates.
- The workflow is a demonstration project and is not a complete production support system.

## Future Improvements

- Add a notification status column to Google Sheets.
- Prevent duplicate notifications for the same ticket.
- Add error handling and retry logic.
- Record email delivery outcomes.
- Create daily summaries of support tickets.
- Integrate additional communication channels.

## Learning Outcomes

This project demonstrates practical experience with:

- No-code and low-code workflow automation.
- Google Sheets integration.
- Conditional logic and branching.
- Gmail integration.
- Event-driven business processes.
- Workflow testing, exporting, and documentation.
