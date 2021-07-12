This repository demonstrates an issue with `analysistest` where `RunWithSuggestedFixes`
passes even if there is no golden file present.

https://github.com/golang/go/issues/47128

## Explanation

The testdata file `no_corresponding_golden_file.go` does not have a corresponding
`.go.golden` file.

It also has no suggested fixes. So `RunWithSuggestedFixes`
seems to skip the file during its checks.

Ideally files that don't have suggested fixes are still compared
against a golden file: some test authors may write tests to ensure
that no fixes are suggested for a given file, and that the file remains
unchanged after applying (the zero) suggested fixes.
