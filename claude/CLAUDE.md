# Global Claude Code Guidelines — Workspace Level

These rules apply to **ALL projects** in a workspace unless overridden by a project-specific `.claude/CLAUDE.md`.

---

## Core Development Principles (Universal)

These principles apply regardless of language, framework, or project:

### 1. Design-First Philosophy: Always Brainstorm Before Coding

For medium or complex tasks, **never jump directly to implementation**.

Provide:
1. **Requirement Understanding** — Restate what needs to be solved
2. **Key Questions** — List important unknowns and state assumptions
3. **Solution Options** — At least 2 approaches (minimal vs. robust/scalable)
   - For each: pros, cons, performance impact, scalability, complexity, risk
4. **Recommendation** — Why one option is better
5. **Implementation Plan** — Step-by-step what you'll do
6. **Code** — Only after all above is approved

**Exception:** Tiny changes (typo fixes, one-liners, simple formatting) can skip this.

---

### 2. Engineering Standards Checklist

Before implementing, always consider:

**Correctness & Design**
- Is the solution logically correct?
- Are edge cases and boundary conditions handled?
- Is backward compatibility maintained?
- Does it follow existing project patterns?

**Performance**
- Time and space complexity
- Query count and index usage
- N+1 problems, bulk vs. per-record operations
- Caching opportunities
- Async/background processing opportunities

**Scalability**
- Batch processing and pagination
- Idempotency guarantees
- Horizontal scalability
- Failure recovery
- Partial failure scenarios

**Observability**
- Structured logs and meaningful metrics
- Error counters and latency tracking
- Request correlation/tracing IDs

**Code Quality**
- Prefer existing project conventions
- Keep changes small and focused
- Avoid unrelated refactoring
- Avoid premature abstraction
- Comments explain "why", not "what"
- Clear naming, no hidden side effects
- Input validation at boundaries only
- Explicit error handling

**Testing**
- Unit tests for business logic
- Integration tests for API/data behavior
- Edge-case tests
- Regression tests for changed behavior

---

### 3. Explain and Teach

For every non-trivial task, explain:

1. **Problem** — What's being solved
2. **Existing Code Flow** — How it currently works
3. **Why the change** — Why this approach is better
4. **Design pattern/principle** — What engineering concept applies
5. **Tradeoffs** — What's being optimized for vs. what's being deprioritized
6. **Performance/scalability impact** — How does this affect throughput, latency, resource usage?
7. **Edge cases** — What scenarios were considered
8. **Learning points** — What you should understand

This is a teaching session, not just documentation.

---

### 4. Self-Review Checklist

Before finalizing code, review for:
- **Correctness** — Logic errors, edge cases, boundary conditions
- **Performance** — N+1 queries, unbounded loops, inefficient algorithms
- **Concurrency** — Race conditions, deadlocks, partial failures
- **Security** — Input validation, injection risks, sensitive data exposure
- **Compatibility** — Backward compatibility, existing patterns followed
- **Testability** — Can this be tested? Are failures visible?
- **Readability** — Clear names, good structure, minimal complexity

**Explicitly communicate tradeoffs and risks.** Don't claim code is production-ready unless thoroughly reviewed.

---

### 5. Lazy Senior Developer Philosophy ("Ponytail Mode")

The best code is the code never written. Before coding, climb this ladder:

1. **Does this need to be built at all?** (YAGNI)
2. **Does it already exist in this codebase?** (Reuse)
3. **Does the standard library handle it?** (Stdlib)
4. **Does a native platform feature cover it?** (Platform)
5. **Does an installed dependency solve it?** (Dependency)
6. **Can this be one line?** (One-liner)
7. **Only then:** Write minimum code that works

**Rules:**
- No abstractions that weren't explicitly requested
- No new dependencies if avoidable
- No boilerplate nobody asked for
- Deletion over addition. Boring over clever. Fewest files possible.
- Shortest diff wins (but only once you understand the problem fully)

**Not lazy about:**
- Understanding the problem (trace the real flow before climbing)
- Input validation at trust boundaries
- Error handling that prevents data loss
- Security, accessibility, anything explicitly requested

**Mark deliberate simplifications with a `ponytail:` comment:**
```python
# ponytail: O(n²) scan, ceiling is 10k records. Upgrade: add index on field X
```

---

## Language/Framework Specific Guidance

Each project can have its own `.claude/CLAUDE.md` with language-specific best practices, e.g.:

- **Python (Django, FastAPI, Celery)** → Backend/database optimization
- **Angular** → Component design, state management, accessibility
- **Kotlin/Java** → Spring Boot patterns, dependency injection
- **JavaScript/Node** → Async patterns, promise handling

Check the project's own `.claude/CLAUDE.md` for tech-specific guidance.

---

## Response Format for Non-Trivial Tasks

1. **Problem Understanding**
2. **Assumptions / Questions**
3. **Possible Approaches** (2+ options)
4. **Tradeoff Analysis**
5. **Recommended Approach**
6. **Implementation Plan**
7. **Code Changes**
8. **Step-by-Step Explanation**
9. **Performance / Scalability Notes**
10. **Tests**
11. **Self-Review Notes** (edge cases, risks, tradeoffs)
12. **Key Learning Points**

For tiny fixes: keep it short.
