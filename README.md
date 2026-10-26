# INET coverage

This repository holds the code coverage reports of the master branch of the
[INET Framework](https://github.com/inet-framework/inet). The workflow
"Test: coverage" (`.github/workflows/coverage-tests.yml` in INET) writes it on
each push to INET master. Do not edit it by hand.

The latest report is at <https://inet-framework.github.io/coverage/>.

## Branches

- **`master`** holds the history:
  - `history.jsonl` has one line for each reported INET commit: the commit,
    its date, the line, function and branch totals, the totals of each area of
    `src/inet/` and of each test suite, and the change against the previous
    line, in percentage points.
  - `latest.json` is the full summary of the latest report, with the values of
    each source file.
- **`gh-pages`** holds the HTML report of the latest INET master commit, made
  by `genhtml`. The workflow replaces this branch with one new commit for each
  report, so the repository does not grow with the HTML.

## What the values mean

The workflow builds OMNeT++ and INET in coverage mode
(`-fprofile-instr-generate -fcoverage-mapping`) and runs these test suites:
the fingerprint tests and the unit, module, packet, queueing and protocol tests.
A line, function or branch counts as covered if at least one of these tests
executes it.

The reports cover `src/inet/`, without the generated message files (`_m.cc`,
`_m.h`) and the third-party code (the lwIP stack and `src/3rdparty`). CI cannot
execute some parts of INET, for example emulation, which needs real network
interfaces, and most of the visualizers, which need Qtenv.

Coverage shows that code ran. It does not show that a test checked the result
of that code.

## Reproduce a report

The commands are in the coverage guide of opp_repl
(`doc/coverage.md` in [omnetpp/opp_repl](https://github.com/omnetpp/opp_repl)):
run the tests with `-m coverage`, export each suite with `opp_export_coverage`,
and merge the exports with `opp_coverage_report`.
