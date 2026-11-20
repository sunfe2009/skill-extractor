# Skill Extractor

A local tool that watches your git history and turns repeated manual Python fixes into reusable, verified skills.

## Problem
You keep making the same class of fix across projects (type errors, migration patterns, small refactors). Each time you rewrite it by hand.

## Solution
A local daemon that:
- Watches recent commits
- Detects repeated Python diff patterns
- Extracts a candidate skill
- Verifies it on held-out diffs before saving
- Only outputs a skill file you can review

## How it works

1. **Trigger**  
   Post-commit hook + local file watcher. Runs fully local.

2. **Pattern detection**  
   Scans recent Python file diffs for repeated edits.

3. **Skill extraction**  
   Turns the repeated change into a small, reusable transformation.

4. **Verification (strict)**  
   - Splits past diffs into extraction set and hold-out set  
   - Applies the skill to the hold-out set  
   - Only accepts the skill if it produces an exact match on every hold-out case  
   - Otherwise discards or tightens the pattern and retries

5. **Output**  
   Writes a single skill file to `.skills/` containing:
   - The pattern
   - The transformation
   - The hold-out cases it passed  

   Nothing is auto-applied. You review the file like normal code.

## Scope (v1)
- Python only
- Git local history only
- Strict identity match on hold-out
- Human in the loop for every skill

## Non-goals
- No cloud
- No auto-apply
- No multi-language support yet