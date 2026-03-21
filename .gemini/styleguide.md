# UCP Schema (ucp-schema) Style Guide

<!--*
freshness: { owner: 'chadliu' reviewed: '2026-03-21' }
*-->

This guide defines the standards for the `ucp-schema` repository, which focuses on high-performance Rust tools for UCP schema resolution and validation.

## Core Principles

### 1. Brand Neutrality
*   **DO NOT** use brand names (e.g., Target, Shopify) in code or tests.
*   **DO** use role-based terms: `Merchant`, `Provider`, `Agent`.

### 2. Rust Performance and Safety
*   **Memory Safety:** Avoid `unsafe` blocks unless absolutely necessary for performance-critical FFI or low-level optimizations. Any `unsafe` block must include a `// SAFETY:` comment.
*   **Error Handling:** Use `thiserror` for library-level errors and `anyhow` for CLI-level application logic. Prefer `Result` over `unwrap()` or `expect()`.
*   **Serde:** Leverage `serde` for efficient JSON serialization/deserialization. Use `#[serde(rename_all = "snake_case")]` to ensure compatibility with UCP field naming standards.

### 3. JSON Schema Integrity
*   **Validation:** Ensure all schema validation logic is strictly compliant with the JSON Schema Draft 2020-12 or higher.
*   **Tests:** Every new feature must include integration tests using `assert_cmd` or `mockito` for mocking remote schema lookups.

## Technical Standards

### Rust Code Style
*   **Format:** Follow standard `rustfmt` rules (enforced via pre-commit).
*   **Doc Comments:** Use `///` for documentation on public items (structs, enums, functions). Include a `# Examples` section for public API functions.
*   **Naming:** `snake_case` for variables/functions, `PascalCase` for types/traits.

### Repository Specifics
*   **Fixtures:** When adding new test fixtures in `fixtures/`, ensure they are brand-neutral and include a comment explaining the scenario they cover.
*   **CLI UX:** Ensure CLI output is clear, informative, and follows standard POSIX exit code conventions.

## Semantic Review Focus
Gemini should prioritize:
1.  **Rust Idioms:** Is the code idiomatic (e.g., using `map`, `and_then`, `match`)?
2.  **Schema Compliance:** Does the resolver handle `$ref` and `$id` correctly according to UCP standards?
3.  **No Brand Leaks:** Check for any brand names in new test fixtures or error messages.
