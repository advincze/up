---
title: Commands
---


Up provides the `up` command-line program. To view details for a command at any time use `up help` or `up help <command>`.

```
Usage:

  up [<flags>] <command> [<args> ...]

Flags:

  -h, --help           Output usage information.
  -r, --region=REGION  Override the region.
  -C, --chdir="."      Change working directory.
  -v, --verbose        Enable verbose log output.
      --version        Show application version.

Commands:

  help            Show help.
  config          Show configuration after defaults and validation.
  deploy          Deploy the project.
  logs            Show log output.
  run             Run a hook.
  stack update    Create or update configured resources.
  stack delete    Delete configured resources.
  stack show      Show the status of the stack.
  start           Start development server.
  url             Show, open, or copy a stage endpoint.

Examples:

  Deploy the project to the development stage.
  $ up

  Deploy the project to the prod stage.
  $ up deploy prod

  Tail project logs.
  $ up logs -f

  Show error or fatal level logs.
  $ up logs 'error or fatal'

  Show help and examples for a sub-command.
  $ up help logs

  Run build command manually.
  $ up run build

```

## config

Validate and output configuration with defaults applied.

```
$ up config
```

```json
{
  "name": "app",
  "description": "",
  "type": "server",
  "headers": null,
  "redirects": null,
  "hooks": {
    "build": "GOOS=linux GOARCH=amd64 go build -o server *.go",
    "clean": "rm server"
  },
  "environment": null,
  "regions": [
    "us-west-2"
  ],
  "inject": null,
  "lambda": {
    "role": "arn:aws:iam::ACCOUNT:role/lambda_function",
    "memory": 128,
    "timeout": 5
  },
  "cors": null,
  "error_pages": {
    "dir": ".",
    "variables": null
  },
  "proxy": {
    "command": "./server",
    "backoff": {
      "min": 100,
      "max": 500,
      "factor": 2,
      "attempts": 3,
      "jitter": false
    }
  },
  "static": {
    "dir": "."
  },
  "logs": {
    "disable": false
  },
  "certs": null,
  "dns": {
    "zones": null
  }
}
...
```

## logs

Show or tail log output with optional query for filtering. 

```
 Usage:

   up logs [<flags>] [<query>]

 Flags:

   -h, --help           Output usage information.
   -r, --region=REGION  Override the region.
   -C, --chdir="."      Change working directory.
   -v, --verbose        Enable verbose log output.
       --version        Show application version.
   -f, --follow         Follow or tail the live logs.

 Args:

   [<query>]  Query pattern for filtering logs.

 Examples:

   Show logs from the past 5 minutes.
   $ up logs

   Show live log output.
   $ up logs -f

   Show error logs.
   $ up logs error

   Show error and fatal logs.
   $ up logs 'error or fatal'

   Show non-info logs.
   $ up logs 'not info'

   Show logs with a specific message.
   $ up logs 'message = "user login"'

   Show 200 responses with latency above 150ms.
   $ up logs 'status = 200 duration > 150'

   Show 4xx and 5xx responses.
   $ up logs 'status >= 400'

   Show emails containing @apex.sh.
   $ up logs 'user.email contains "@apex.sh"'

   Show emails ending with @apex.sh.
   $ up logs 'user.email = "*@apex.sh"'

   Show emails starting with tj@.
   $ up logs 'user.email = "tj@*"'

   Show logs with a more complex query.
   $ up logs 'method in ("POST", "PUT") ip = "207.*" status = 200 duration >= 50'
```

## url

Show, open, or copy a stage endpoint.

```

Usage:

  up url [<flags>] [<stage>]

Flags:

  -h, --help           Output usage information.
  -r, --region=REGION  Override the region.
  -C, --chdir="."      Change working directory.
  -v, --verbose        Enable verbose log output.
      --version        Show application version.
  -o, --open           Open endpoint in the browser.
  -c, --copy           Copy endpoint to the clipboard.

Args:

  [<stage>]  Name of the stage.

Examples:

  Show the development endpoint.
  $ up url

  Open the development endpoint in the browser.
  $ up url --open

  Copy the development endpoint to the clipboard.
  $ up url --copy

  Show the production endpoint.
  $ up url production

  Open the production endpoint in the browser.
  $ up url -o production

  Copy the production endpoint to the clipboard.
  $ up url -c production

```

## start

Start development server.

```
Usage:

  up start [<flags>]

Flags:

  -h, --help             Output usage information.
  -r, --region=REGION    Override the region.
  -C, --chdir="."        Change working directory.
  -v, --verbose          Enable verbose log output.
      --version          Show application version.
      --address=":3000"  Address for server.

Examples:

  Start development server on port 3000.
  $ up start

  Start development server on port 5000.
  $ up start --address :5000

```
