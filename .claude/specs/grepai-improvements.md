# grepai Improvement Ideas

## Status: Planning

## Priority 1: Call Graph Reliability

The trace feature (callers/callees/graph) returns empty results too often. This could be the killer feature for refactoring workflows.

### Investigation Needed
- [ ] Why does `symbols.gob` not contain expected symbols?
- [ ] Is the symbol extraction language-specific? Which languages are supported?
- [ ] Are method calls vs function calls handled differently?
- [ ] Is there a minimum project size or structure required?

### Potential Fixes
- [ ] Add `grepai trace status` to show indexed symbol count and coverage
- [ ] Improve symbol extraction for common languages (Go, TypeScript, Python)
- [ ] Add warnings when trace returns empty ("No symbols indexed for this project")

## Priority 2: Index Resilience

Transient read errors on GOB files shouldn't surface as "corruption" to users.

### Potential Fixes
- [ ] Add retry logic (2-3 attempts with backoff) for GOB reads
- [ ] File locking to prevent read-during-write races
- [ ] Better error messages: distinguish corruption vs transient vs missing index
- [ ] `grepai index --verify` command to check index health

## Priority 3: Graceful Degradation

When semantic search fails, provide useful fallback behavior.

### Potential Fixes
- [ ] If embedder unavailable, suggest exact-match fallback command
- [ ] If index missing/corrupt, auto-trigger reindex with user confirmation
- [ ] Timeout handling for slow embedder responses (Ollama cold start)

## Priority 4: Search Quality Improvements

### Ideas
- [ ] Show which chunk matched (not just file + line range)
- [ ] Highlight matching concepts in output (like grep highlights matches)
- [ ] `--explain` flag to show why a result matched (embedding similarity breakdown)
- [ ] Filter by file type: `grepai search "auth" --type ts`
- [ ] Negative filtering: `grepai search "auth" --exclude "*test*"`

## Priority 5: Developer Experience

### Ideas
- [ ] `grepai status` - show index stats (files, chunks, symbols, last updated)
- [ ] `grepai index --dry-run` - show what would be indexed
- [ ] Progress indicator during initial indexing (large codebases)
- [ ] `grepai config show` - display effective config with sources

## Key Files
- `store/gob.go` - GOB storage implementation
- `indexer/symbols.go` - Symbol extraction for call graph
- `search/search.go` - Search execution
- `cli/trace.go` - Trace command implementation

## Notes
- Semantic search quality is good (0.7+ scores correlate with relevance)
- Local Ollama embeddings keep it cost-free for heavy use
- `--json --compact` for AI integration is well designed
