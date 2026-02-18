# Appendix\_B\_MCP\_Configuration

**MCP** = Model Context Protocol. It lets Cursor connect to external tools and services for enhanced development capabilities.

**When to use**: When you need Cursor to interact with external systems (databases, APIs, Docker, GitHub) or need enhanced reasoning capabilities.

***

## Why MCPs Matter

**Without MCPs**: Cursor only sees your local files. To check database state, Docker containers, or GitHub issues, you copy-paste manually.

**With MCPs**: Cursor can query databases, inspect Docker containers, read GitHub issues, and access external tools directly.

**Result**: Faster debugging, better context, less context switching.

***

## Essential MCPs for Product Development

### Docker MCP (for local development)

**Use when**: Running services in Docker containers (databases, Redis, message queues)

**What it provides**:

* Inspect running containers
* Check logs
* Verify environment variables
* Debug networking issues

**Configuration**:

```jsonc
{
  "mcpServers": {
    "docker": {
      "command": "/usr/local/bin/docker",
      "args": ["mcp", "gateway", "run"]
    }
  }
}
```

**Prerequisites**:

```bash
# macOS
brew install docker

# Verify installation
docker --version
```

**Example usage with Cursor**:

```
You: "Check if postgres container is running and show me its logs"
Cursor: [uses Docker MCP]
Cursor: "Container postgres_db is running. Recent logs show..."
```

**Common scenarios**:

* "Why isn't my API connecting to the database?" → Cursor checks container status
* "What environment variables are set in the Redis container?" → Cursor inspects config
* "Show me the last 50 lines of API logs" → Cursor fetches from Docker

***

### GitHub MCP (for issue tracking and PRs)

**Use when**: Project uses GitHub for issues, PRs, project management

**What it provides**:

* Read issues and PRs
* Check project status
* Reference discussion context
* Track feature progress

**Configuration**:

```jsonc
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "ghp_your_token_here"
      }
    }
  }
}
```

**Setup**

{% stepper %}
{% step %}
### Create a GitHub Personal Access Token

* Go to GitHub → Settings → Developer Settings → Personal Access Tokens → Tokens (classic)
* Generate new token
* Select scopes: `repo`, `read:org`, `read:project`
* Copy token
{% endstep %}

{% step %}
### Add token to MCP config

Add the token to the `env` section of the `github` MCP configuration (example above).
{% endstep %}

{% step %}
### Security note

Don't commit config with token. Use environment variable:

```jsonc
"env": {
  "GITHUB_PERSONAL_ACCESS_TOKEN": "${GITHUB_TOKEN}"
}
```

Then set `GITHUB_TOKEN` in your shell environment.
{% endstep %}
{% endstepper %}

**Example usage**:

```
You: "What are the open issues for the chat feature?"
Cursor: [uses GitHub MCP]
Cursor: "There are 3 open issues:
1. #42: Streaming disconnects on slow connections
2. #45: Message history not loading for new users  
3. #47: Chat composer doesn't handle line breaks"

You: "Show me the context from issue #42"
Cursor: [reads issue]
Cursor: "Issue #42 describes users experiencing disconnects when on mobile networks. Suggested fix involves adding exponential backoff..."
```

**Common scenarios**:

* "What's the status of the authentication refactor?" → Cursor checks PR and related issues
* "Are there any open bugs related to memory system?" → Cursor searches issues
* "What did we decide about the database schema?" → Cursor references PR discussion

***

### Sequential-Thinking MCP (for complex reasoning)

**Use when**: Cursor needs to work through complex logic, multi-step reasoning, or architectural decisions

**What it provides**:

* Step-by-step reasoning display
* Better handling of complex problems
* Visible thought process (helps you catch errors)

**Configuration**:

```jsonc
{
  "mcpServers": {
    "sequential-thinking": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-sequential-thinking"]
    }
  }
}
```

**No setup required** - works out of the box.

**Example usage**:

```
You: "How should I refactor the goal system to support recurring goals?"
Cursor: [uses sequential-thinking MCP]
Cursor: "Let me think through this step by step:

1. Current system stores goals as single entities with start/end dates
2. Recurring goals need pattern (daily, weekly, monthly)
3. Each instance needs its own completion state
4. Need to handle goal template vs goal instance
5. Completion history must link to specific instances

Based on this reasoning, I recommend..."
```

**Common scenarios**:

* Complex architectural decisions
* Debugging tricky bugs with multiple causes
* Planning database migrations with dependencies
* Designing API contracts between services

***

### PostgreSQL MCP (for database inspection)

**Use when**: You use PostgreSQL and frequently need to check schema, query data, or debug database issues

**What it provides**:

* Query database directly
* Inspect schema
* Check indexes and performance
* Verify migrations

**Configuration**:

```jsonc
{
  "mcpServers": {
    "postgres": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-postgres"],
      "env": {
        "DATABASE_URL": "postgresql://user:password@localhost:5432/dbname"
      }
    }
  }
}
```

**Security note**: Use local database only. Don't point to production.

**Example usage**:

```
You: "Show me the schema for the users table"
Cursor: [uses PostgreSQL MCP]
Cursor: "Users table has:
- id (uuid, primary key)
- email (text, unique)
- created_at (timestamp)
- profile_data (jsonb)
..."

You: "How many users have goals created in the last week?"
Cursor: [queries database]
Cursor: "347 users have created goals in the last 7 days"
```

**Common scenarios**:

* "What indexes exist on the goals table?" → Cursor checks schema
* "Show me a sample goal record" → Cursor queries data
* "Did the migration add the new column?" → Cursor inspects schema
* "Why is this query slow?" → Cursor analyzes indexes

***

### Filesystem MCP (for external codebases)

**Use when**: You need to reference external codebases, libraries, or documentation not in your current project

**What it provides**:

* Read files outside project root
* Reference other repositories
* Check library source code

**Configuration**:

```jsonc
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem"],
      "env": {
        "ALLOWED_PATHS": "/Users/you/projects:/Users/you/reference-code"
      }
    }
  }
}
```

**Security note**: Limit `ALLOWED_PATHS` to only what you need. Don't give access to entire system.

**Example usage**:

```
You: "Check how the authentication library handles token refresh"
Cursor: [reads external library code via filesystem MCP]
Cursor: "The auth library implements token refresh in src/auth.ts:

[shows relevant code from external repo]

You could adapt this pattern for your use case..."
```

**Common scenarios**:

* "How does library X implement feature Y?" → Cursor reads source
* "Show me an example from reference-project" → Cursor fetches file
* "What's the API contract for this external service?" → Cursor reads OpenAPI spec

***

## Practical MCP Setup Workflow

### Minimal Setup (Start Here)

For most projects, start with 2 MCPs:

```jsonc
{
  "mcpServers": {
    "docker": {
      "command": "/usr/local/bin/docker",
      "args": ["mcp", "gateway", "run"]
    },
    "sequential-thinking": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-sequential-thinking"]
    }
  }
}
```

**Why these two**:

* Docker: Essential for local development debugging
* Sequential-thinking: Improves Cursor's reasoning on complex problems

**Time to setup**: 5 minutes

### Add GitHub if Using GitHub Projects

```jsonc
{
  "mcpServers": {
    "docker": {
      "command": "/usr/local/bin/docker",
      "args": ["mcp", "gateway", "run"]
    },
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "${GITHUB_TOKEN}"
      }
    },
    "sequential-thinking": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-sequential-thinking"]
    }
  }
}
```

**Additional time**: 10 minutes (includes GitHub token creation)

### Add Database MCP if Frequent Schema Work

```jsonc
{
  "mcpServers": {
    "docker": {
      "command": "/usr/local/bin/docker",
      "args": ["mcp", "gateway", "run"]
    },
    "postgres": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-postgres"],
      "env": {
        "DATABASE_URL": "postgresql://localhost:5432/myapp_dev"
      }
    },
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "${GITHUB_TOKEN}"
      }
    },
    "sequential-thinking": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-sequential-thinking"]
    }
  }
}
```

**Additional time**: 5 minutes

***

## Configuration Location

### macOS/Linux

```
~/.cursor/mcp.json
```

### Windows

```
%APPDATA%\Cursor\mcp.json
```

### Project-Specific Config

You can also create `.cursor/mcp.json` in project root for project-specific MCPs.

***

## When MCPs Are Worth It

### High ROI scenarios:

**Microservices architecture**: Docker MCP essential for debugging service interactions

**Active GitHub workflows**: GitHub MCP saves constant tab switching to check issues/PRs

**Database-heavy work**: PostgreSQL MCP faster than switching to database GUI

**Complex refactoring**: Sequential-thinking MCP helps Cursor work through multi-step changes

**Reference implementations**: Filesystem MCP useful when adapting patterns from other codebases

### Low ROI scenarios:

**Simple projects**: One service, no Docker → Docker MCP unnecessary

**Solo developer, no issues tracking**: GitHub MCP won't add much value

**Static schema**: If database rarely changes, PostgreSQL MCP is overkill

**Straightforward logic**: Sequential-thinking MCP doesn't help with simple CRUD

***

## Troubleshooting MCPs

### MCP not loading

**Symptom**: Cursor doesn't show MCP capabilities

**Check**

{% stepper %}
{% step %}
### Is MCP config file in correct location?

Check `~/.cursor/mcp.json` or `.cursor/mcp.json` in project root.
{% endstep %}

{% step %}
### Is JSON valid?

Use a JSON validator to confirm there are no syntax errors.
{% endstep %}

{% step %}
### Are paths correct?

Verify binaries/paths (for example, `/usr/local/bin/docker`) exist.
{% endstep %}

{% step %}
### Restart Cursor after config changes

Make sure to restart the Cursor app/process to pick up new config.
{% endstep %}
{% endstepper %}

**Debug**

```bash
# macOS: Verify Docker path
which docker

# Verify npx available
which npx
```

### Docker MCP fails

**Symptom**: "Cannot connect to Docker daemon"

**Solutions**:

* Start Docker Desktop
* Verify Docker is in PATH: `docker ps` should work in terminal
* Check Docker MCP config uses correct path: `/usr/local/bin/docker` (macOS) or `docker` (if in PATH)

### GitHub MCP authentication fails

**Symptom**: "Invalid token" or "Unauthorized"

**Solutions**:

* Verify token has correct scopes (`repo`, `read:org`)
* Check token hasn't expired
* Ensure environment variable is set: `echo $GITHUB_TOKEN`
* Try using token directly in config (temporarily) to isolate issue

### PostgreSQL MCP connection fails

**Symptom**: "Could not connect to database"

**Solutions**:

* Verify database is running: `psql -U user -d dbname`
* Check `DATABASE_URL` format: `postgresql://user:password@host:port/dbname`
* Use `localhost` not `127.0.0.1` if connecting via Unix socket
* Verify user has permissions to read schema

***

## Security Best Practices

### DO:

* Use environment variables for tokens and credentials
* Limit filesystem MCP to specific directories (`ALLOWED_PATHS`)
* Use local/dev databases only (never production)
* Rotate GitHub tokens periodically
* Use read-only database users when possible

### DON'T:

* Commit MCP config with tokens/passwords
* Give filesystem MCP access to home directory or system paths
* Point PostgreSQL MCP to production database
* Use admin/root database credentials
* Share MCP config files publicly

***

## Other Useful MCPs

Beyond the essentials, these MCPs can be useful for specific scenarios:

* **Slack MCP**: Read Slack messages, search channels (useful for understanding team context)
* **Google Drive MCP**: Access docs, sheets (useful if product specs live in Drive)
* **Stripe MCP**: Query customer data, subscriptions (useful for billing work)
* **Memory MCP**: Long-term conversation memory across sessions (experimental)
* **Brave Search MCP**: Web search for current information (alternative to built-in search)

See full list at: [Model Context Protocol Registry](https://github.com/modelcontextprotocol/servers)

***

## When to Skip MCPs

**Don't use MCPs if**:

* Security concerns: Handling sensitive data, can't expose to Cursor
* Simple project: Small MVP, straightforward logic, one developer
* Learning curve: Team unfamiliar with Cursor, adding MCPs creates confusion
* Maintenance burden: MCPs require keeping config updated, tokens rotated
* Alternative tools sufficient: Sometimes copying from database GUI is faster than MCP setup

***

## Summary

**Start with**:

* Docker MCP (if using containers)
* Sequential-thinking MCP (always useful)

**Add if relevant**:

* GitHub MCP (if heavy GitHub usage)
* PostgreSQL MCP (if frequent schema work)
* Filesystem MCP (if referencing external code)

**Setup time**: 15-30 minutes for basic config

**ROI**: Starts paying off immediately for debugging, compounds over time

**Security**: Use environment variables, read-only access, local/dev databases only

**When to skip**: Simple projects, security concerns, team unfamiliarity with Cursor

***

## Example: Full Development Config

```jsonc
{
  "mcpServers": {
    "docker": {
      "command": "/usr/local/bin/docker",
      "args": ["mcp", "gateway", "run"]
    },
    "postgres": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-postgres"],
      "env": {
        "DATABASE_URL": "${DATABASE_URL}"
      }
    },
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "${GITHUB_TOKEN}"
      }
    },
    "sequential-thinking": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-sequential-thinking"]
    }
  }
}
```

Then in my shell config (`.zshrc` or `.bashrc`):

```bash
export DATABASE_URL="postgresql://localhost:5432/myapp_dev"
export GITHUB_TOKEN="ghp_your_token_here"
```

This gives me:

* Docker debugging for local services
* Database inspection for schema work
* GitHub context for issues and PRs
* Enhanced reasoning for complex problems

**Time saved per day**: 30-60 minutes (less context switching, faster debugging)
