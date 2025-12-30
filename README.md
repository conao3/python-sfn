# sfn

A command-line tool for working with AWS Step Functions. Provides streamlined commands for listing, describing, and visualizing state machines and their executions.

## Features

- **List state machines** - Quickly enumerate all state machines in your AWS account
- **List executions** - View execution history with status, timing, and duration in CSV format
- **Describe state machines** - Get detailed JSON output of state machine configurations
- **Generate graphs** - Create Graphviz DOT diagrams from state machine definitions for visualization

## Requirements

- Python 3.11 or higher
- AWS credentials configured (via environment variables, AWS CLI, or IAM role)

## Installation

```bash
pip install sfn
```

Or install from source using Poetry:

```bash
git clone https://github.com/conao3/python-sfn.git
cd python-sfn
poetry install
```

## Usage

### List State Machines

```bash
sfn list-state-machines
sfn list-state-machines --max-items 50
```

### List Executions

```bash
sfn list-executions --state-machine-arn arn:aws:states:us-east-1:123456789012:stateMachine:MyStateMachine
```

Outputs CSV with columns: name, status, start_date, stop_date, duration.

### Describe State Machine

```bash
sfn describe-state-machine --state-machine-arn arn:aws:states:us-east-1:123456789012:stateMachine:MyStateMachine
```

### Generate State Machine Graph

Pipe a state machine definition (JSON) to generate a Graphviz DOT diagram:

```bash
sfn describe-state-machine --state-machine-arn <arn> | jq '.definition | fromjson' | sfn state-machine-graph > graph.dot
dot -Tpng graph.dot -o graph.png
```

The generated graph includes AWS service icons and visualizes state transitions, choice branches, and error handling paths.

## License

Apache-2.0
