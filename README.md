# HyperStickler

Commit & PR formalities checker based on the OpenWrt [submission guidelines](
  https://openwrt.org/submitting-patches#submission_guidelines).

## Rules

- Pull request must come from a feature branch
- Pull request must not include merge commits
- Author name must be either a real name 'firstname lastname' or a
  nickname/alias/handle
- Author email must not be a GitHub noreply email
- Commit(ter) name must be either a real name 'firstname lastname' or a
  nickname/alias/handle
- Commit(ter) email must not be a GitHub noreply email
- Commit subject must start with `<package name or prefix>: `
- Commit subject must start with a lower-case word after the prefix
- Commit subject must not end with a period
- Commit subject must be <= `MAX_SUBJECT_LEN_HARD` (and should be <=
  `MAX_SUBJECT_LEN_SOFT`) characters long

  `MAX_SUBJECT_LEN_SOFT` is 50

  `MAX_SUBJECT_LEN_HARD` is 60

- `Signed-off-by` must match author
- `Signed-off-by` must not be a GitHub noreply email
- Commit message must exist
- Commit message lines should be <= `MAX_BODY_LINE_LEN` characters long

  `MAX_BODY_LINE_LEN` is 75

- Commit to stable branch should be marked as cherry-picked

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

## Example output

![Example output](assets/output.png)

## Example status comment

> [!WARNING]
>
> Some formality checks failed.
>
> Consider (re)reading [submissions guidelines](
https://openwrt.org/submitting-patches#submission_guidelines).

<details>
<summary>Failed checks</summary>

Issues marked with an :x: are failing checks.

### Commit efa95656a79cdae0b976c6a5b28de91922a431a6

- :x: Commit message must exist

</details>

  For more details, see the [full job log](https://github.com/GeorgeSapkin/openwrt-packages/actions/runs/20278728720/job/58239257139?pr=1#step:4:1).

Something broken? Consider [providing feedback](
https://github.com/openwrt/actions-shared-workflows/issues).

## Tests

```bash
src/test.sh /tmp/some-tmp-path
```

## License

GNU General Public License v2.0 only
