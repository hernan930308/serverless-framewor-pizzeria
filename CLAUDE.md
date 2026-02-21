# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Serverless Framework project for deploying AWS Lambda functions. The service is configured to use AWS Lambda with Node.js 20.x runtime.

## Architecture

- **Handler Functions**: Lambda function handlers are defined in `handlers.js` (note: `serverless.yml` references `handler.hello` but the actual file is `handlers.js`)
- **Configuration**: `serverless.yml` defines the service configuration, provider settings, and function definitions
- **Deployment Artifacts**: The `.serverless/` directory contains CloudFormation templates and deployment artifacts (generated after deployment)

### Configuration Mismatch

There's a discrepancy between `serverless.yml` and the actual project structure:
- `serverless.yml:9` references `handler.hello` as the handler
- The actual handler file is `handlers.js` with `exports.hello`
- When modifying or adding functions, ensure the handler path in `serverless.yml` matches the actual file name

## Common Commands

### Deployment
```bash
serverless deploy
# or
sls deploy
```

### Local Invocation
```bash
serverless invoke local -f hello
# or
sls invoke local -f hello
```

### Remote Invocation (after deployment)
```bash
serverless invoke -f hello
# or
sls invoke -f hello
```

### View Logs
```bash
serverless logs -f hello
# or
sls logs -f hello --tail
```

### Remove Deployed Stack
```bash
serverless remove
# or
sls remove
```

### Package (without deploying)
```bash
serverless package
```

## Development Workflow

1. Modify function handlers in `handlers.js`
2. Update `serverless.yml` if adding new functions or changing configurations
3. Test locally using `serverless invoke local -f <function-name>`
4. Deploy to AWS using `serverless deploy`
5. Check deployment artifacts in `.serverless/` directory

## Function Handler Pattern

Lambda handlers should follow this structure:
```javascript
exports.functionName = async (event) => {
  return {
    statusCode: 200,
    body: JSON.stringify({ message: "response" })
  };
};
```

The event object contains HTTP request data when triggered via HTTP API Gateway events.
