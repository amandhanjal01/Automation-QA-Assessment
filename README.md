# GitHub Morning Brief Automation

## Project Overview

This project is an automated GitHub repository monitoring workflow built
using **n8n Cloud**. It retrieves popular repositories from GitHub,
sorts and selects the top five, fetches additional repository details,
applies a star-count condition, and stores qualifying results in Google
Sheets.

## Tools and Technologies

-   **n8n Cloud** -- workflow automation platform
-   **GitHub REST API** -- retrieves repository and repository-detail
    data
-   **JavaScript** -- transforms, sorts, and filters repository data
-   **Google Sheets** -- stores the results and error logs

## Workflow Process

1.  **Schedule Trigger:** Starts the workflow on an hourly schedule.
2.  **HTTP Request 1 -- GitHub Search API:** Calls
    `https://api.github.com/search/repositories` with the search query
    `stars:>1000`, sorted by stars in descending order, requesting five
    results.
3.  **Code Node -- Data Transformation:** Sorts the returned
    repositories by star count and selects the top five. It extracts
    each repository's full name, star count, description, URL, and
    programming language.
4.  **HTTP Request 2 -- Repository Details:** Calls
    `https://api.github.com/repos/{owner}/{repo}` for each selected
    repository to retrieve additional details.
5.  **IF Condition:** Checks whether `stargazers_count` is greater than
    1,000.
6.  **Google Sheets:** Appends qualifying repository details to the
    `GitHub Morning Brief Report` spreadsheet.

## Google Sheets Output

The main worksheet stores:

-   Repository Name
-   Stars
-   Description
-   Repository URL
-   Language
-   Forks
-   Open Issues
-   Last Updated

## Error Handling

A separate workflow named `GitHub Automation Error Handler` is
configured with an **Error Trigger**. The main workflow is configured to
use this error workflow.

When an eligible execution failure occurs, the error handler is designed
to append the following details to the `Error_Log` worksheet:

-   Timestamp
-   Workflow Name
-   Error Message

## How to Run

1.  Sign in to the n8n Cloud workspace.
2.  Open `GitHub Morning Brief Automation`.
3.  Execute the workflow manually for testing, or enable its scheduled
    execution.
4.  Open the `GitHub Morning Brief Report` Google spreadsheet to review
    the results.

## Testing Result

The main workflow was executed successfully. All workflow nodes
completed successfully, and five repository records were verified in
Google Sheets.

## Project Files

-   `Task2_Workflow_AmanDhanjal.json` -- exported main workflow
-   `Task2_Error_Handler_AmanDhanjal.json` -- exported error-handler
    workflow
-   `Task2_Screenshots/` -- screenshots of the workflow, successful
    execution, and Google Sheets output

**Project:** GitHub Morning Brief Automation\
**Platform:** n8n Cloud\
**Output:** Google Sheets
