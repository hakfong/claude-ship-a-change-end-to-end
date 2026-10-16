# Notes

## Plan
Added a `PATCH /users/:id` endpoint to the Express app so callers can update a user's name and email independently without replacing the whole record.

## Model choice
Used Claude Sonnet for implementation — good balance of speed and accuracy for straightforward CRUD work.

## Commit split
- One commit for the route implementation
- One commit for the corresponding test coverage

## What the review caught
Checked for missing input validation (no body provided), verified the 404 path when the user ID doesn't exist, and confirmed the response shape matches the existing GET endpoint.
