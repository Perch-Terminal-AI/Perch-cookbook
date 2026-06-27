# Verify citations in a draft

**Surface:** Web / Desktop

Generation tools are good at writing a brief. They are not good at confirming that every case they cited exists, says what it is cited for, and is still good law. That is a separate job, and it is the one that keeps a filing out of trouble. Perch treats citation verification as a check, not as part of the draft.

> This recipe runs on the web app and the desktop app. The citation checker relies on document indexing that lives outside the terminal-safe CLI bridge, so it is not a `perch run` command today.

## On the web

1. Go to [chat.perchai.app](https://chat.perchai.app) and sign in.
2. Upload or paste the draft you want to check.
3. Ask Quill to verify the citations.

```
Verify every citation in this draft. For each one, tell me whether the
authority exists, whether it supports the proposition it is cited for,
and whether it is still good law. Mark anything you cannot confirm.
```

## What you get back

Citation states are intentionally plain:

- **Verified.** The authority exists and supports the claim.
- **Unsupported.** The authority exists but does not say what it is cited for.
- **Missing.** The source could not be found, which is the signature of a fabricated citation.

Unsupported and missing claims are flagged rather than quietly smoothed over, so you know exactly what the draft can defend before it goes anywhere.

## Drafting with Quill from the start

You can also write with verification built in. Ask Quill to draft from a source set, and it reads the sources before it writes, marking any claim it cannot support as `[UNSOURCED]` instead of letting it pass as fact.

## Why this is the point

A fabricated citation looks exactly like a real one on the page. Its correctness is invisible until someone checks. Perch makes the check the default, with the evidence shown, so trust is something you can confirm rather than something you extend.
