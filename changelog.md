## [v0.22.0](https://github.com/boywithkeyboard/updater/releases/tag/v0.22.0)

- **Support for deno.re.** updater can now update `https://deno.re/...` imports.

## [v0.21.1](https://github.com/boywithkeyboard/updater/releases/tag/v0.21.1)

- The error log for type checking is now logged directly on the console. This fixes the problem of exceeding the maximum character length of a pull request description.

## [v0.21.0](https://github.com/boywithkeyboard/updater/releases/tag/v0.21.0)

- The pull request now contains the error log in the event that the type check has failed.

## [v0.20.0](https://github.com/boywithkeyboard/updater/releases/tag/v0.20.0)

- **den.ooo is no longer supported.**

- **`include` and `exclude` specific files and directories.** You can specify files, directories and glob patterns to include or exclude.

- **updater accidentally created a schema.json file.** This bug has now been fixed.

## [v0.19.0](https://github.com/boywithkeyboard/updater/releases/tag/v0.19.0)

- **`updater.json` config file.** You can now configure updater with this configuration file.

  ```json
  {
    "$schema": "https://updater.mod.land/schema.json",
    "allowBreaking": true
  }
  ```

  The file must be in the root directory of your project or in the `.github` directory.

- **Short footnote in pull request**, with the used version of updater and the number of updated imports.

## [v0.18.3](https://github.com/boywithkeyboard/updater/releases/tag/v0.18.3)

- **denopkg.com imports are now updated correctly.** v0.18.0 introduced support for denopkg.com imports, but updates for such imports previously failed.

## [v0.18.2](https://github.com/boywithkeyboard/updater/releases/tag/v0.18.2)

- **updater's GitHub action now uses deno.land/x.** This is due to the upcoming major update of den.ooo, which could cause an interruption.

## [v0.18.1](https://github.com/boywithkeyboard/updater/releases/tag/v0.18.1)

- **Correct updating of side effect imports.** v0.18.0 introduced an issue which basically replaced side effect imports with the URL without preserving the import statement.

  ```ts
  // before
  import 'https://esm.sh/slash@5.0.0'
  // after
  https://esm.sh/slash@5.1.0
  ```

  v0.18.1 now fixes this behavior and preserves the import statement.

  ```ts
  // before
  import 'https://esm.sh/slash@5.0.0'
  // after
  import 'https://esm.sh/slash@5.1.0'
  ```

## [v0.18.0](https://github.com/boywithkeyboard/updater/releases/tag/v0.18.0)

- **Regenerate `deno.lock`.** If your project has a `deno.lock` file, updater will now regenerate this file as well.

- **Update side effect imports.** updater used to ignore such imports in the past due to a minor bug that occurred during the parsing of the regex matches. This issue has now been resolved.
  
  [mdn reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#import_a_module_for_its_side_effects_only)

- **Support for denopkg.com.** updater can now update `https://denopkg.com/...` imports.

## [v0.17.0](https://github.com/boywithkeyboard/updater/releases/tag/v0.17.0)

- **Compatibility Checking**

  updater now performs a basic compatibility check (with `deno check`) and adds a warning to the changelog if there are any issues.

## [v0.16.0](https://github.com/boywithkeyboard/updater/releases/tag/v0.16.0)

- **Support for JSR**

  updater can now handle `jsr:` imports. Please read [the documentation](https://github.com/boywithkeyboard/updater#supported-registries) to learn more.

- **Bug Fixes**

  - Scoped NPM modules should now be updated correctly.
  - In the event of an error, response body streams are now properly aborted.

## [v0.15.0](https://github.com/boywithkeyboard/updater/releases/tag/v0.15.0)

- **GitHub Action**

  It's now easier than ever to integrate **boywithkeyboard's updater** into your workflow.

  ```yml
  name: update

  on:
    schedule:
      - cron: '0 0 * * *'
    workflow_dispatch:

  permissions:
    contents: write
    pull-requests: write

  jobs:
    update:
      runs-on: ubuntu-latest

      steps:
        - uses: actions/checkout@v4

        - name: Run updater
          uses: boywithkeyboard/updater@v0
  ```

  [Read more](https://github.com/boywithkeyboard/updater?tab=readme-ov-file#boywithkeyboards-updater)
