# Example Principal

This is a template principal directory. Copy this directory and rename it to create your own principal.

## Setup

1. Copy this directory: `cp -r claude/principals/example-principal claude/principals/yourname`
2. Update `claude/config/agency.yaml` to map your system username to your principal name:
   ```yaml
   principals:
     your_system_username: yourname
   ```
3. Customize the directories as needed

## Directory Structure

```
yourname/
  artifacts/      # Deliverables produced by agents
  instructions/   # Tasks and direction for agents
  notes/          # Your personal notes
  requests/       # Work requests (REQUEST-xxx files)
  resources/      # Reference materials, configs
  sessions/       # Session logs and context
```

## Usage

- Use `./tools/capture-instruction` to create instructions for agents
- Use `./tools/capture-artifact` when agents produce deliverables
- Store work requests in `requests/` using the REQUEST-xxx pattern
