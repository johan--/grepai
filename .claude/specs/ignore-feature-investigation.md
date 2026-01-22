# Ignore Feature Investigation

## Status: In Progress

## Completed
- [x] Does `grepai init` overwrite user config? **No** - exits early if config exists
- [x] Expand default ignore list with framework-specific patterns (Angular, Rails, Elixir/Phoenix)

## Next Steps

### 1. Investigate .gitignore Handling
- Read `indexer/gitignore.go` - check if .gitignore is already respected
- Read `indexer/scanner.go` - understand how ignore list is applied
- Determine: Does grepai currently respect `.gitignore`?

### 2. Understand Ignore Precedence
- What's the order: gitignore first, then config.yaml additions?
- Are they merged or does one override the other?
- Document the behavior

### 3. Test the Behavior
- Test in `/home/johan/projects/hipconsult/infranav-v2`
- Verify custom ignores from config.yaml are respected
- Verify .gitignore patterns are respected

## Key Files
- `config/config.go` - Config struct and defaults (updated)
- `indexer/gitignore.go` - Gitignore parsing
- `indexer/scanner.go` - File scanning with ignore logic
- `cli/init.go` - Init command (verified)

## Context
User's test project: `/home/johan/projects/hipconsult/infranav-v2` (Angular)
