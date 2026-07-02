# Commit Message Convention

## Purpose
Define a consistent commit message format for EduCore to improve traceability, readability, and release management.

## Format
```
<type>(<scope>): <short summary>
```

## Common Types
- feat
- fix
- docs
- refactor
- test
- chore
- ci
- perf
- build

## Guidelines
- Use the imperative mood.
- Keep the summary concise.
- Reference issues when applicable.
- Describe breaking changes in the commit body when necessary.

## Examples
- feat(auth): add password reset flow
- fix(api): handle expired access tokens
- docs(readme): update setup instructions

## Success Criteria
- All commits follow the agreed convention.
- Commit history remains clear and searchable.