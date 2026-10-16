# Notes

## Plan
Added a `PUT /users/:id` endpoint to the Express app so callers can replace a user's name and email (both fields required — full replace, not a partial update).

## Model choice
Used Claude Sonnet for implementation — good balance of speed and accuracy for straightforward CRUD work.

## Commit split
- One commit for the route implementation
- One commit for the corresponding test coverage

## What the review caught
Checked for missing input validation (no body provided), verified the 404 path when the user ID doesn't exist, and confirmed the response shape matches the existing GET endpoint.

## Post-review fixes
A code review pass surfaced five issues that were fixed in a follow-up commit:
- **500 on missing Content-Type**: `req.body` is `undefined` when no JSON header is sent — fixed by destructuring from `req.body || {}`.
- **Whitespace-only strings passed validation**: `!'   '` is falsy-false — fixed by checking `.trim()` before the guard and storing trimmed values.
- **Non-numeric :id returned 404 instead of 400**: `Number('abc')` is `NaN`, which always misses the lookup — fixed with an explicit `isNaN(id)` check returning 400.
- **Store had no defense against undefined fields**: `updateUser` would silently set fields to `undefined` if called without both values — fixed by adding a guard at the top of the function.
- **NOTES.md said PATCH instead of PUT**: the description and implementation were misaligned — corrected to PUT (full replace, both fields required).
