# app-test-cases

Test cases that the Breeze apps (`breeze-android` and `breeze-ios`) share, so that rules both apps
work out separately give the same result. The apps use this repo as a git submodule.

| Folder | What | Spec |
|---|---|---|
| `time-rules/` | Badge, opening-hours rows and exceptions at a fixed clock and time zone | `facilities-in-bff`, "Time rules in both apps" (R10, R17) |

## Rules

- A case holds the input and the expected result only. Expected results have no words, so each app
  can keep its own strings.
- Expected results come from the spec, not from what an app returns. A change to a case is a
  change to a rule: make it together with the spec, and move both apps to the new commit.
- Each folder has a README with the format of its cases.
- Cases must not contain secrets, tokens or personal data.
