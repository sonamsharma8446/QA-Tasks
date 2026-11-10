
# GitHub Repository Monitoring Workflow

## 1. Project Overview

This project is an automated GitHub repository monitoring workflow built using n8n.

It fetches repository information from the GitHub API, processes the data, selects the top 5 repositories, andchecks their star count. Based on the star count, it sends notifications to a Discord channel.

## 2. Tools and APIs Used

- **n8n:** To create and execute the automation workflow.
- **GitHub REST API:** To fetch repository information.
- **JavaScript:** To process and filter repository data.
- **Discord Webhook:** To send notifications.

## 3. Workflow Steps

1. **Schedule Trigger:** Starts the workflow automatically at the configured interval.
2. **HTTP Request:** Fetches repository information from the GitHub API.
3. **Code in JavaScript:** Processes the response and selects the top 5 repositories.
4. **Second HTTP Request:** Fetches additional information about the selected repositories.
5. **If Node:** Checks whether the repository has more than 1000 stars.
6. **Discord Notification:** Sends a high-priority notification for repositories with more than 1000 stars and a normal notification for the remaining repositories.

## 4. Notification Logic

The workflow uses the following condition:

`stargazers_count > 1000`

- **True:** Sends a high-priority GitHub alert to Discord.
- **False:** Sends a regular GitHub update to Discord.

Notifications include repository information such as its name, star count, fork count, and GitHub URL.

## 5. Error Handling

Error handling is configured for HTTP Request nodes to make the workflow more reliable.

- Retry on Fail is enabled.
- Maximum retry attempts: 3.
- Wait between retries: 1000 milliseconds.
- The On Error setting is configured to continue using the error output, where supported.

This helps handle temporary API failures without silently stopping the workflow.

## 6. Testing

The workflow was executed manually in n8n to verify the connected nodes and their outputs.

The GitHub API response, JavaScript processing, conditional branches, and Discord notification requests were checked during execution.

## 7. Conclusion

This workflow automates GitHub repository monitoring and sends useful updates to Discord based on repository popularity. It reduces the need to manually check repository information.