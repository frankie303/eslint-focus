# eslint-focus

Allows running ESLint on a directory with a single rule or set of rules matching a pattern.
The matched rules MUST be enabled in your ESLint config for the files you want it to run on (e.g. enable it in your root `.eslintrc.js`).

## Usage

```bash
npx eslint-focus <ruleOrRulePattern> <relativeOrAbsolutePath>

Run ESLint with a single rule or rules matching a pattern on a given directory.

Positionals:
  ruleOrRulePattern       A single rule or pattern                                                              [string]
  relativeOrAbsolutePath  An absolute path or a path relative to the current working directory.                 [string]

Options:
  --version            Show version number                                                                     [boolean]
  --help               Show help                                                                               [boolean]
  --allowInlineConfig  Respects eslint-disable directives.                                    [boolean] [default: false]
  --fix                Same as `eslint --fix`: https://eslint.org/docs/latest/use/command-line-interface#--fix
                                                                                              [boolean] [default: false]
  --fix-type           Same as `eslint --fix-type`: https://eslint.org/docs/latest/use/command-line-interface#--fix-type
                                                                                                                 [array]

Examples:
  npx eslint-focus react-hooks/rules-of-hooks .                 Run `react-hooks/rules-of-hooks` on every file inside
                                                                the current directory.
  npx $1 /jest\// .                                             Run all Jest rules on every file inside the current
                                                                directory.
  npx eslint-focus react-hooks/exhaustive-deps . --fix          Fixes all `react-hooks/exhaustive-deps` issues inside
  --fix-type suggestion                                         the current directory.
```

```bash
$ npx eslint-focus react/no-unstable-nested-components .
/Users/sebastian.silbermann/repo/BottomSheet.native.tsx:106:29
/Users/sebastian.silbermann/repo/BottomSheet.native.tsx:145:15
/Users/sebastian.silbermann/repo/CardExpirationWarning.tsx:51:23
┌──────────────────────┬────────┐
│       (index)        │ Values │
├──────────────────────┼────────┤
│   Considered files   │ 71671  │
│    Skipped files     │  181   │
│ Files failed to lint │   1    │
│  Files with issues   │  216   │
│        Issues        │  308   │
└──────────────────────┴────────┘
Done in 386.08s.
```

## Missing

Configure extensions. By default it runs on everything that's TypeScript or JavaScript i.e. `/\.(cjs|cts|js|jsx|mjs|mts|ts|tsx)$/`.

## Why?

- eslint-nibbler is slow
- ESLint formatters still executes every rule
- ESLint `--no-eslintrc` means I have to know the parser options up front
- ESLint has no built-in support to stream results
