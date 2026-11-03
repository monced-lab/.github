# Testing

How we test, for all monced-lab repos.

## Where tests live

| What | Where |
| --- | --- |
| Automated tests | `tests/` in the repo of the code, run on every PR |
| Manual checks | `docs/manual-tests.md` in that repo, starts with a link to this file |
| What a feature needs tested | the Tests section of its issue |
| How it went | "How it was tested" in the PR |
| Recurring server checks (restore, monthly check, DMARC) | issues and runbook in `server` |

Tests never go in a separate repo, they change in the same PR as the code.

## Rules

- Test the rules hardest: anything that books, mails, deletes or refuses
- A real database (Postgres in Docker), not a fake one
- A fake clock for anything that waits (reminders, expiry), never real waiting
- Every refusal gets a test: wrong signature, old timestamp, invalid link, too many attempts
- Test names say what they check: `test_bad_signature_is_refused`
- Only made-up data, never real names or emails from our inbox
- Failing tests first (`test:` commit), then the code (`feat:`), when it makes sense
- Every mail checked in Mailpit, in NL and EN, before a release

## Manual checks

Each code repo has a `docs/manual-tests.md` like this:

```markdown
# Manual tests

How we test: see [TESTING.md](https://github.com/monced-lab/.github/blob/main/TESTING.md)

## Before every release
- [ ] ...

## Once at setup
- [ ] ...
```

## CI

Once a repo has code, its tests run on every PR with GitHub Actions.
Actions pinned to a commit, `permissions: contents: read`.
