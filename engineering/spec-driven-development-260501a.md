# Spec-Driven Development

**Date:** 2026-05-01  
**Category:** engineering  
**Tags:** `spec-driven`, `tdd`, `bdd`, `api-first`, `design`, `testing`, `workflow`  
**Related:** [First Principles Thinking in Software Engineering](first-principles-260422a.md)

---

## TL;DR

- **Spec-Driven Development (SDD)** means writing a precise specification *before* any implementation — the spec is the design, not the documentation of it
- The spec can take many forms: an OpenAPI contract, a BDD scenario, a type signature, a property test, or a formal schema
- SDD inverts the typical order: instead of code → docs → tests, you get spec → tests → code
- The primary benefit is that decisions about *what* a system does are made explicitly and up front — before they are locked into implementation details
- The discipline exposes ambiguity early, when it is cheap to resolve, and produces code that is easier to test, review, and replace

---

## What Spec-Driven Development Is

Spec-Driven Development is the practice of writing a **precise, verifiable description of a system's behavior** before writing any implementation code. The specification is not a design document that will eventually be translated into code — it *is* the design. The implementation is the work of satisfying it.

The term is an umbrella. Depending on context and tooling, the spec might be:

| Form | Example |
|---|---|
| API contract | An OpenAPI / Swagger YAML describing every endpoint, request shape, and response code |
| Behavioral scenario | A Gherkin `Given / When / Then` block expressing user-observable behavior |
| Type signature | A function signature with pre- and post-conditions |
| Schema | A JSON Schema or Protobuf definition that every message must conform to |
| Property test | A QuickCheck-style invariant that must hold for all inputs |
| Formal spec | A TLA+ or Alloy model describing state transitions |

What all of these share: they are **machine-checkable**, written by a human before any implementation exists, and they define what "correct" means independently of the code that will be asked to achieve it.

---

## How It Differs From TDD and BDD

SDD is often conflated with Test-Driven Development and Behavior-Driven Development. The relationships are real but distinct.

**TDD** is a micro-cycle discipline: red test → green code → refactor. TDD is about *rhythm* and design feedback at the unit level. It does not prescribe what the units are, what the public API looks like, or how components fit together.

**BDD** is a communication discipline: it uses structured natural language (Gherkin) to align stakeholders on behavior before implementation begins. BDD scenarios can serve as specs, but BDD is primarily about the conversation — making sure everyone agrees on what "done" looks like.

**SDD** is a *design-first* discipline. It is concerned with:

1. Making the external contract explicit before writing a single line of implementation
2. Treating the spec as the artifact that drives everything else — tests, stubs, documentation, and review

A useful way to place them:

```
TDD    → specifies behavior at the unit level, during implementation
BDD    → specifies behavior in human language, to align stakeholders
SDD    → specifies the external contract before design begins, to constrain everything that follows
```

SDD does not replace TDD or BDD. In a mature workflow, BDD scenarios become SDD specs, and those specs drive TDD micro-cycles during implementation.

---

## The Core Workflow

```
1. Write the spec
2. Validate the spec (review, lint, schema-check)
3. Generate stubs or mocks from the spec
4. Write tests against the spec
5. Implement until tests pass
6. Verify the implementation against the spec
```

The distinguishing feature of step 3 is that it makes the spec immediately useful — not eventually useful once someone writes code. API stubs can be deployed on day one. Consumer teams can build against a mock server. Integration tests can be written before the backend exists.

This is what separates SDD from "write a design doc and then implement whatever feels right" — the spec has executable weight from the moment it is written.

---

## API-First as the Most Common SDD Pattern

The most widely practiced form of SDD is **API-First development** — writing an OpenAPI specification before implementing any endpoints.

A concrete flow with OpenAPI:

1. **Author the spec** — define paths, verbs, request bodies, response schemas, and error codes in `openapi.yaml`
2. **Validate** — run `openapi-generator validate` or equivalent; review the spec in a tool like Swagger UI
3. **Generate a server stub** — use the generator to produce controller scaffolding with the correct signatures but empty bodies
4. **Generate a mock server** — tools like Prism can serve the spec as a live mock immediately
5. **Write contract tests** — consumer teams write tests against the mock; producer teams write tests that assert their implementation matches the spec
6. **Implement** — fill in the stub bodies; tests enforce that the responses conform to the contract
7. **Gate the CI pipeline** — fail any build where the running server's responses violate the spec

The spec becomes the **source of truth** for the API surface. Documentation is generated from it. SDK clients are generated from it. Breaking change detection is automated against it.

---

## Behavioral Specifications with Gherkin

When the artifact being specified is user-observable behavior rather than an API contract, BDD-style Gherkin scenarios serve as the spec:

```gherkin
Feature: User authentication

  Scenario: Successful login with valid credentials
    Given a registered user with email "alice@example.com" and password "correct-horse"
    When the user submits the login form
    Then the user is redirected to the dashboard
    And a session token is stored in the response cookie

  Scenario: Failed login with invalid password
    Given a registered user with email "alice@example.com"
    When the user submits the login form with password "wrong"
    Then the response status is 401
    And the body contains the error code "INVALID_CREDENTIALS"
    And no session token is set
```

These scenarios, written before any code, do several things at once:

- They expose ambiguity (what *exactly* is the error message? which cookie? what is the redirect path?)
- They become executable tests via frameworks like Cucumber or SpecFlow
- They serve as acceptance criteria that any implementation must satisfy
- They are readable by non-engineers, enabling earlier review

The discipline is in writing them *first* — before the implementation makes the answers feel obvious.

---

## Property-Based Specifications

For logic-heavy code, specs can be expressed as **invariants that must hold across all inputs** rather than as fixed examples:

```python
# Property: encode and decode are inverses
@given(st.binary())
def test_round_trip(data):
    assert decode(encode(data)) == data

# Property: compression never increases size beyond a known bound
@given(st.binary(min_size=100))
def test_compression_ratio(data):
    assert len(compress(data)) <= len(data) * 1.1
```

Property tests are specifications written in code. They express what *must always be true* rather than what is true for one example. Tools like Hypothesis (Python), QuickCheck (Haskell), and fast-check (JavaScript) generate thousands of random inputs to challenge the invariant — and shrink failing cases to the minimal example that breaks it.

Property-based specifications are especially powerful for:
- Serialization and encoding
- Sorting and ranking algorithms
- State machine transitions
- Security invariants (authorization must never allow X regardless of input shape)

---

## Why Specifications Expose Ambiguity

The single most valuable thing a specification does is **force a decision before implementation begins**.

In most development processes, ambiguity lives in requirements documents, verbal agreements, and assumptions. It becomes visible only when two engineers build components that cannot talk to each other, or when a feature ships and stakeholders realize it does not do what they expected.

Writing a spec externalizes the implicit. When you have to write:

```yaml
responses:
  '422':
    description: Validation error
    content:
      application/json:
        schema:
          $ref: '#/components/schemas/ValidationError'
```

You are forced to decide: what fields does `ValidationError` have? Does it include the field name? The rejected value? A human-readable message? A machine-readable code? All of the above?

These questions have answers. The spec forces you to write them down before the implementation makes the wrong answer feel normal.

---

## When SDD Is Most Valuable

SDD pays the largest dividend when:

- **Multiple teams share a boundary** — a spec lets consumers and producers work in parallel without blocking on each other
- **The contract is long-lived** — APIs used by external clients, public SDKs, or mobile apps where breaking changes are expensive
- **The behavior is complex or safety-critical** — formal or property-based specs catch edge cases that example-based tests miss
- **Regulatory or compliance requirements exist** — a spec is auditable evidence of intended behavior, separate from the implementation

SDD is overkill when:
- The system boundary will not be shared or persisted
- The team is small enough that informal agreement is fast and reliable
- The domain is too exploratory to specify up front (prototypes, spikes)

---

## Common Failure Modes

| Failure | Description |
|---|---|
| **Spec drift** | The implementation diverges from the spec, and no CI gate catches it — the spec becomes a historical artifact rather than a living contract |
| **Spec theater** | A spec is written after the implementation to satisfy a process requirement, losing all the design-time benefit |
| **Over-specification** | Implementation details leak into the spec, making it brittle to refactor — specs should describe *what*, not *how* |
| **Ambiguity laundering** | A spec is written, but the hard questions are deferred with vague language ("suitable error message") — the spec does the work of looking rigorous without resolving the actual ambiguity |
| **Consumer-producer misalignment** | The spec is owned by one team with no mechanism for consumers to propose changes — breaking changes ship without warning |

---

## Keeping the Spec Honest

A spec that is not enforced is documentation. To keep it honest:

1. **Gate CI on spec conformance** — use tools like Dredd, Schemathesis, or Spectral to run your implementation against the spec on every build
2. **Generate, don't maintain** — wherever possible, generate code (types, clients, server stubs) from the spec rather than maintaining both in parallel
3. **Version the spec** — treat the spec as a versioned artifact; breaking changes require a version bump and a migration plan
4. **Contract testing at boundaries** — use Pact or similar consumer-driven contract testing to verify that the spec accurately reflects what consumers actually depend on

---

## A Working Heuristic

Before writing any implementation code at a system boundary, ask:

1. **What does "correct" mean for this component, stated independently of how it will be implemented?**
2. **Can I write that definition down in a form a machine can check?**
3. **If another team were building the implementation and I were building the consumer, would this spec be enough for both of us to work independently?**
4. **What questions does writing this spec force me to answer that I have been deferring?**

If you cannot answer question 1, you are not ready to implement. If you can answer it but not question 2, your spec is still informal — worth writing, but not yet enforcing. Questions 3 and 4 are the discipline: the spec is not done until it is sufficient for parallel work and has no deferred decisions.

---

## Sources

[1] [OpenAPI Specification (3.1)](https://spec.openapis.org/oas/v3.1.0)  
[2] [Gherkin Reference — Cucumber Documentation](https://cucumber.io/docs/gherkin/reference/)  
[3] [Hypothesis: Property-Based Testing for Python](https://hypothesis.readthedocs.io/en/latest/)  
[4] [Dredd — HTTP API Testing Framework](https://dredd.org/en/latest/)  
[5] [Schemathesis — Property-Based API Testing](https://schemathesis.readthedocs.io/en/stable/)  
[6] [Pact — Consumer-Driven Contract Testing](https://docs.pact.io/)  
[7] [Spectral — OpenAPI Linter](https://stoplight.io/open-source/spectral)
