# HyperStickler

Commit & PR formalities checker based on the OpenWrt [submission guidelines](
  https://openwrt.org/submitting-patches#submission_guidelines).

## Inputs

All inputs are optional.

### `exclude_dependabot`

- Exclude commits authored by dependabot from some checks.
- Defaults to `true`

### `exclude_weblate`

- Exclude commits authored by Weblate from some checks.
- Defaults to `false`

### `post_comment`

- Post summaries to the pull request.
- Defaults to `false`

### `warn_on_no_modify`

- Warn when PR edits by maintainers are not allowed. Requires `post_comment` to
  be `true`.
- Defaults to `false`

## Permissions

Posting comments requires `pull-requests: write`.

## Example usage

```yaml
name: Formalities
on:
  pull_request_target:

permissions:
  pull-requests: write

jobs:
  formal:
    runs-on: ubuntu-slim
    name: Formalities
    steps:
      - name: Check formalities
        uses: georgesapkin/stickler@main
        with:
          exclude_weblate: true
          post_comment: true
```

## License

GNU General Public License v2.0 only
