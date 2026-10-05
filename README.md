# llm-trading-lab-anchors

Public register of SHA256 fingerprints of preregistered research hypotheses.

The research happens in a private repository. Before a hypothesis is tested, its full preregistration is committed there and its SHA256 hash is added here. Anyone who later receives the preregistration can recompute the hash and compare it with the line in this register. A match shows that the document existed in exactly this form when the line was pushed, before the test started.

This repository contains hypothesis IDs, timestamps and hashes only. No strategy details, code or data.

## File format

anchors.csv holds one line per preregistration:

```
hypothesis_id,created_utc,sha256
H001,2026-10-20T09:30:00Z,<64 lowercase hex characters>
```

| Field | Meaning |
|---|---|
| hypothesis_id | ID of the hypothesis in the private research log, for example H001. A changed preregistration gets a new ID. |
| created_utc | When the preregistration was finalized and hashed, ISO 8601 in UTC |
| sha256 | SHA256 hash of the exact bytes of the preregistration file |

## Rules

* Append only. Lines are never edited, reordered or deleted.
* main is protected: GitHub rejects force pushes and deletion of main, so published lines can't be removed by rewriting history.
* Each preregistration contains a random nonce line, so its content can't be found by hashing guessed texts.
* Nothing except the three fields above is stored here.

## Verifying an anchor

1. Get the preregistration file from the author.
2. Compute its hash. Mac or Linux: `shasum -a 256 FILE`. Windows PowerShell: `Get-FileHash FILE -Algorithm SHA256`.
3. Find the hypothesis ID in anchors.csv and compare the hashes.
4. Check when the line arrived on GitHub. The commit date is set by the author's computer and proves nothing on its own. The push time recorded by GitHub is listed in this repository's Activity view: github.com/saschaurban/llm-trading-lab-anchors/activity
