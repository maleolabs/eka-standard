# Exchange conformance corpus

Normative examples for the package format described in
`specification/exchange.md`. Each case is a repository fixture plus an entry in
`cases.json`; together they state what an implementation must produce when it
exports a repository to a package, imports that package into a fresh
repository, and exports again.

The corpus is examples, not an additional rule: it asserts only what the
specification already requires — the round trip is byte-identical, declared
envelope fields survive, and an artifact that declared nothing gains nothing.

## Running a case

Against one fixture directory:

1. export it to a package;
2. assert every path listed under `unit` appears in the exported `unit.json`;
3. import the package into an empty repository;
4. assert every path under `artifact` is present, and every path under `absent`
   is absent, in the written artifact;
5. export the imported repository and require the bytes to equal the first
   package.

`roundtrip` is the only outcome supported today, and its value is
`identical`. A case that asserts nothing is a defect: every entry states at
least one expectation.

## Why the expectations are split

`unit` and `artifact` are separate lists because the two documents spell a
declared zero confidence differently, and a single list would either assert
something false or hide a loss:

- the package unit omits a zero value, so a declared `0` is carried by
  `hasConfidence: true`;
- the repository artifact carries `confidence: 0` and never carries
  `hasConfidence`, which is a package-transport flag.

## Cases

| Case | Fixture | Declares |
| --- | --- | --- |
| `envelope-full` | `envelope-full/` | provenance, prompt hash, a declared zero confidence, commit sha, full capture metadata, validity horizon |
| `envelope-absent` | `envelope-absent/` | nothing; the cycle must not invent a declaration |
| `note` | `note/` | a comment unit and its `note-state` domain |

## Adding a case

Add a fixture directory and one manifest entry. No code changes in the
implementation either: a corpus that needs new logic to accommodate a case is
a corpus that stopped describing the format.

Fixtures carry no absolute paths and no host state, so the directory can be
copied into an implementation's own test data verbatim. `SHA256SUMS` records
the bytes of every file here; an implementation that ships its own copy
verifies it against that file, which is how a corpus that quietly diverged
from the published one becomes visible.