---
summary: "Checklist for AI-assisted code review covering correctness, style, testing, and cross-package impact"
---

# Skill: Code review

Guidelines for AI-assisted code review in Toby's packages.

## Checklist

When reviewing code, check the following:

### Correctness
- [ ] Does the code do what it claims to do?
- [ ] Are edge cases handled?
- [ ] Are there off-by-one errors, null/None handling issues, or type mismatches?

### Style and conventions
- [ ] Follows the project's existing naming conventions
- [ ] Consistent with the style guide in `guidelines/` (if available)
- [ ] No unnecessary complexity or over-engineering

### Testing
- [ ] Are there tests for new functionality?
- [ ] Do existing tests still pass?
- [ ] Are edge cases tested?

### Documentation
- [ ] Public API changes are documented
- [ ] Complex logic has explanatory comments
- [ ] CHANGELOG or NEWS updated if applicable

### Bioinformatics-specific
- [ ] Numerical results are reproducible (seeds set where applicable)
- [ ] Memory usage is reasonable for typical input sizes
- [ ] Input validation covers common bioinformatics data formats
