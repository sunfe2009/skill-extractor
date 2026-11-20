# Skill Extractor

Local tool that watches git history and turns repeated Python fixes into reusable skills.

- Triggered by post-commit hook
- Extracts repeated diff patterns
- Verifies on held-out diffs (strict match)
- Writes skill file to .skills/ only after verification passes
- Human reviews before use