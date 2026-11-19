# Time rules: shared test vectors

`cases.json` holds cases for the rules that both apps work out themselves from the facilities
response and the clock (spec `facilities-in-bff`, "Time rules in both apps", R10 and R17). The
expected results have no words on purpose, so each app can keep its own strings.

Both the Android and the iOS app run this file against their own implementation, so a rule can
not change in one app only. Change the file only together with the spec
(`app-squad-product`, `spec/facilities-in-bff`). Each app reads it through this repo as a git
submodule, so a change here reaches an app when the app moves its submodule to the new commit.

## A case

| Field | Meaning |
|---|---|
| `id`, `rule` | A short name, and the spec rule the case checks. |
| `timeZone` | The hotel's IANA time zone. |
| `nowUtc` | The fixed clock, in UTC. The hotel's time is this instant in `timeZone`. |
| `schedules` | The facility category's schedules, as in the API contract (`type`, `validFrom`, `validTo`, `rows` of `days` and `periods`). A `closing` of `null` means closes late. |
| `expected` | Any of the parts below. A part that is missing is not checked. |

## Expected

- `hotelNow`: the hotel's local date and time.
- `status`: the badge. `kind` is `closesAt` (with `time`), `opensAt` (with `from`),
  `openAllDay`, `closingLate` or `none`.
- `rows`: the regular hours rows, in order. `runs` are the days in a row, Monday first (one day
  is a run with the same first and last day), `star` is the `*` mark, `periods` are the periods
  and `today` marks today's row. No rows means the hours are hidden.
- `exceptionRows`: the upcoming exceptions, one line for each period that has not ended. A
  `period` of `null` means closed.

The dates are in November 2026: 2026-11-18 is a Wednesday, and Oslo is UTC+1.
