# GitHub MCP Server - Java Implementation

A Java implementation of the GitHub MCP (Model Context Protocol) Server using Spring AI. This server provides MCP-compatible tools for interacting with the GitHub API.

## Features

This Java implementation provides the following GitHub MCP tools:

### Repository Operations
- `create_repository` - Create a new repository
- `fork_repository` - Fork a repository
- `get_repository` - Get repository details
- `list_commits` - List commits
- `get_commit` - Get commit details
- `get_file_contents` - Get file contents
- `create_or_update_file` - Create or update a file
- `delete_file` - Delete a file
- `create_branch` - Create a branch
- `list_branches` - List branches
- `merge_branch` - Merge branches

### Issue Operations
- `create_issue` - Create an issue
- `update_issue` - Update an issue
- `add_issue_comment` - Add comment to issue
- `list_issues` - List issues
- `get_issue` - Get issue details
- `close_issue` - Close an issue
- `reopen_issue` - Reopen an issue
- `assign_issue` - Assign issue to users
- `unassign_issue` - Unassign issue
- `add_issue_labels` - Add labels to issue
- `remove_issue_label` - Remove label from issue

### Pull Request Operations
- `create_pull_request` - Create a PR
- `update_pull_request` - Update a PR
- `list_pull_requests` - List PRs
- `get_pull_request` - Get PR details
- `merge_pull_request` - Merge a PR
- `close_pull_request` - Close a PR
- `reopen_pull_request` - Reopen a PR
- `add_pull_request_comment` - Add PR comment
- `create_pull_request_review` - Create PR review
- `submit_pull_request_review` - Submit PR review

### Search Operations
- `search_code` - Search code
- `search_issues` - Search issues
- `search_repositories` - Search repositories
- `search_users` - Search users

### User Operations
- `get_authenticated_user` - Get authenticated user info
- `get_user` - Get user info
- `list_user_repositories` - List user repositories

## Prerequisites

- Java 17 or higher
- Maven 3.8+
- GitHub Personal Access Token

## Configuration

### Environment Variables

| Variable | Description | Required |
|----------|-------------|----------|
| `GITHUB_PERSONAL_ACCESS_TOKEN` | GitHub Personal Access Token | Yes |
| `GITHUB_HOST` | GitHub hostname (for GitHub Enterprise) | No |
| `GITHUB_READ_ONLY` | Enable read-only mode | No |
| `GITHUB_TOOLSETS` | Comma-separated list of toolsets to enable | No |
| `GITHUB_TOOLS` | Comma-separated list of specific tools to enable | No |
| `GITHUB_EXCLUDE_TOOLS` | Comma-separated list of tools to exclude | No |

### Creating a GitHub Personal Access Token

1. Go to GitHub Settings → Developer settings → Personal access tokens
2. Click "Generate new token (classic)"
3. Select the following scopes:
   - `repo` - Full control of private repositories
   - `workflow` - Update GitHub Action workflows
   - `read:org` - Read org and team membership
   - `gist` - Create gists
   - `notifications` - Access notifications
   - `read:user` - Read user profile data
4. Generate and copy the token

## Building

```bash
mvn clean package
```

## Running

### Using Maven

```bash
export GITHUB_PERSONAL_ACCESS_TOKEN=your_token_here
mvn spring-boot:run
```

### Using JAR

```bash
export GITHUB_PERSONAL_ACCESS_TOKEN=your_token_here
java -jar target/github-mcp-server-1.0.0.jar
```

## Docker

### Build Docker Image

```bash
docker build -t github-mcp-server .
```

### Run Docker Container

```bash
docker run -p 8080:8080 -e GITHUB_PERSONAL_ACCESS_TOKEN=your_token_here github-mcp-server
```

## MCP Client Configuration

### Claude Desktop

Add to your `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "github": {
      "command": "java",
      "args": [
        "-jar",
        "/path/to/github-mcp-server-1.0.0.jar"
      ],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "your_token_here"
      }
    }
  }
}
```

### HTTP Transport

The server also supports HTTP transport on port 8080:

```json
{
  "mcpServers": {
    "github": {
      "url": "http://localhost:8080/mcp"
    }
  }
}
```

## API Endpoints

- `GET /health` - Health check endpoint
- `POST /mcp` - MCP protocol endpoint

## Project Structure

```
com.github.mcp/
├── GithubMcpApplication.java          # Main Spring Boot application
├── client/
│   ├── GitHubRestClient.java          # REST API client
│   └── GitHubGraphqlClient.java       # GraphQL client
├── config/
│   ├── GitHubProperties.java          # Configuration properties
│   └── WebConfig.java                 # Web configuration
├── controller/
│   └── HealthController.java          # Health check endpoint
├── dto/
│   ├── common/
│   │   ├── ApiResponse.java           # Generic API response wrapper
│   │   └── PagedResponse.java         # Paginated response wrapper
│   ├── request/                       # Request DTOs
│   └── response/                      # Response DTOs
├── exception/
│   ├── GitHubMcpException.java        # Base exception
│   └── GlobalExceptionHandler.java    # Global error handler
├── service/
│   ├── interfaces/                    # Service interfaces
│   └── impl/                          # Service implementations
└── tools/
    ├── RepositoryTools.java           # Repository operations
    ├── IssueTools.java                # Issue operations
    ├── PullRequestTools.java          # PR operations
    ├── SearchTools.java               # Search operations
    └── UserTools.java                 # User operations
```

## Technology Stack

- Java 21
- Spring Boot 3.4.3
- Spring AI 1.0.0-M6 (MCP Server)
- Maven
- Lombok
- Jackson

## License

MIT License - See LICENSE file for details

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Acknowledgments

This project is a Java port of the official [GitHub MCP Server](https://github.com/github/github-mcp-server) written in Go.
