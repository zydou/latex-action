## [v3.2.0](https://github.com/zydou/latex-action/compare/v3.1.2...v3.2.0) (2023-08-29)

### Features

- add `ubuntu` series base image by **@zydou** in [337d8d2](https://github.com/zydou/latex-action/commit/337d8d2b9f84eec14b39cdc95552a4f56d301337)
- always glob root file by **@Cheng XU** in [33306cd](https://github.com/zydou/latex-action/commit/33306cd91227c182f3513add9732a1da310b4604)
- remove obsolete release.yml by **@Cheng XU** in [6fcbaff](https://github.com/zydou/latex-action/commit/6fcbaffa1c796d159423b954bc89f5c47d77d28b)
- show what docker commands are used by **@Cheng XU** in [e4e73e7](https://github.com/zydou/latex-action/commit/e4e73e7d1f6e2ffe0c1a754df885aeab21bbd6af)
- improve action.yaml by **@Cheng XU** in [24ee590](https://github.com/zydou/latex-action/commit/24ee59069341611952269008d5bfc4b85542c6e3)
- add an option to select texlive version directly by **@zydou** in [0f3ba56](https://github.com/zydou/latex-action/commit/0f3ba5642bcfdb25fbc66491f2a909a396cbc40b)

### Bug Fixes

- add default values for boolean option and use `=` to test them ([#131](https://github.com/zydou/latex-action/issues/131)) by **@Zhiyong Dou** in [9ae8710](https://github.com/zydou/latex-action/commit/9ae8710583a967aa7f9773ab07c8695131b732b7)
- fix typo in entrypoint path by **@Cheng XU** in [ace7072](https://github.com/zydou/latex-action/commit/ace7072bc8b91fba8d6608f005af916dac1c2dd4)
- use texlive-full:20220201 for v2-texlive2021 by **@Cheng XU** in [7efc1fe](https://github.com/zydou/latex-action/commit/7efc1fe0dc361fa00688457a1fcff448e2a70343)
- use `Doulos SIL` to test `extra_fonts` function by **@zydou** in [6c9efba](https://github.com/zydou/latex-action/commit/6c9efba311576008de38dd4f451eb152f28d11ae)
- fix indent in `action.yml` by **@zydou** in [a9c06ad](https://github.com/zydou/latex-action/commit/a9c06ad44ee8111b7f4620375aec5cf57f5e5ab1)

### Documentation

- use author name instead of committer name in changelog by **@zydou** in [a81c4e4](https://github.com/zydou/latex-action/commit/a81c4e40c8605b90f22702837155607cf65cc17e)

### Chores

- remove deprecated input extra_packages by **@Cheng XU** in [868bee6](https://github.com/zydou/latex-action/commit/868bee6c01c8634e96caa1c0006d35b119d865e3)

### Full Changelog: [v3.1.2 -> v3.2.0](https://github.com/zydou/latex-action/compare/v3.1.2...v3.2.0)

## [v3.1.2](https://github.com/zydou/latex-action/compare/v3.1.1...v3.1.2) (2023-08-26)

### Bug Fixes

- use equals sign to compare strings by **@zydou** in [aa8bcf7](https://github.com/zydou/latex-action/commit/aa8bcf7ea310b1b53f81a646f8c991390df2fa49)

### Continuous Integration

- **test:** add test directory to ci by **@zydou** in [d281589](https://github.com/zydou/latex-action/commit/d281589f2264c8f60537265cb99ef17e93efed78)

### Styles

- apply formatter `beautifysh` and `shfmt`, fix `shellcheck` warning by **@zydou** in [e5dc5ba](https://github.com/zydou/latex-action/commit/e5dc5ba3c15e2e8b29d448c41db303e5d392613c)

### Documentation

- update usages and add comparisons to the original by **@zydou** in [5ccce87](https://github.com/zydou/latex-action/commit/5ccce876b13095c6e2dd090b4069218a75ee9495)

### Chores

- **bump:** bump patch version from `v3.1.1` to `v3.1.2` by **@zydou** in [9cc13ea](https://github.com/zydou/latex-action/commit/9cc13ea096f28c60ab338b753a2a0f6c9db439e6)

### Full Changelog: [v3.1.1 -> v3.1.2](https://github.com/zydou/latex-action/compare/v3.1.1...v3.1.2)

## [v3.1.1](https://github.com/zydou/latex-action/compare/v3.1.0...v3.1.1) (2023-08-26)

### Continuous Integration

- update release workflow by **@zydou** in [f291f9a](https://github.com/zydou/latex-action/commit/f291f9aa9e288c7c78e81f0e7d85941239356a1d)
- add path filter to test.yml by **@zydou** in [c3113ff](https://github.com/zydou/latex-action/commit/c3113ff840ccb4a206425923712ee83d7ec5c105)

### Chores

- **bump:** bump patch version from `v3.1.0` to `v3.1.1` by **@zydou** in [076dfcc](https://github.com/zydou/latex-action/commit/076dfcc34121bf03a0cdebf00d37bebfb4cc3495)

### Full Changelog: [v3.1.0 -> v3.1.1](https://github.com/zydou/latex-action/compare/v3.1.0...v3.1.1)

## [v3.1.0](https://github.com/zydou/latex-action/compare/v3.0.0...v3.1.0) (2023-08-25)

### Features

- add options to select texlive and debian versions by **@zydou** in [debe130](https://github.com/zydou/latex-action/commit/debe130b66e31ae4fcd46ee5c9d58dde66be00e4)

### Full Changelog: [v3.0.0 -> v3.1.0](https://github.com/zydou/latex-action/compare/v3.0.0...v3.1.0)

## [v3.0.0](https://github.com/zydou/latex-action/commits/v3.0.0) (2023-08-25)

### Bug Fixes

- fix glob expanding by **@Cheng XU** in [8c9adec](https://github.com/zydou/latex-action/commit/8c9adec310ed05afa3650bd2727d1e71ca1dfd0d)
- fix incorrect glob expanding by **@Cheng XU** in [cf136a3](https://github.com/zydou/latex-action/commit/cf136a3e6e442dec959ecfd501eda8511d332687)

### Continuous Integration

- add workflow_dispatch trigger by **@Cheng XU** in [700834e](https://github.com/zydou/latex-action/commit/700834ee23eb4dbd3028a3270ca1e9f46f4f7934)

### Code Refactoring

- use composite action and zydou/texlive as base image by **@zydou** in [0d8ba0d](https://github.com/zydou/latex-action/commit/0d8ba0de7a7e1abbf984942b87354ee2f21f02d9)

### Tests

- remove github default template test by **@Cheng XU** in [5a4e79a](https://github.com/zydou/latex-action/commit/5a4e79a69121c2944c1447dcf3649dc3b35fb25e)

### Chores

- fmt the code by **@Cheng XU** in [3b20ee1](https://github.com/zydou/latex-action/commit/3b20ee12f88004811fa0cc18963925dbc730e045)

### Pull Requests

- Merge pull request [#57](https://github.com/zydou/latex-action/issues/57) from ascopes/patch-1
- Merge pull request [#56](https://github.com/zydou/latex-action/issues/56) from sinchang-bot/patch-1
- Merge pull request [#48](https://github.com/zydou/latex-action/issues/48) from allexks/request/create-working-dir
- Merge pull request [#40](https://github.com/zydou/latex-action/issues/40) from tomjaguarpaw/patch-1

### Full Changelog: [v3.0.0](https://github.com/zydou/latex-action/commits/v3.0.0)
