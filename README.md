# Gitea Delete artifacts

Based on [https://github.com/GeekyEggo/delete](https://github.com/GeekyEggo/delete).

A GitHub Action for deleting artifacts within the workflow run. This can be useful when artifacts are shared across jobs, but are no longer needed when the workflow is complete.

## ✅ Compatibility

| `actions/upload-artifact` | `geekyeggo/delete-artifact` |
| ------------------------- | --------------------------- |
| `@v4`                     | `@v5`                       |

<!-- prettier-ignore -->
> [!TIP]
> You can reference the immutable commit SHA, instead of a version, for example.
> ```yml
> - uses: geekyeggo/delete-artifact@f275313e70c08f6120db482d7a6b98377786765b # v5.1.0
> ```
<!-- prettier-ignore-end -->

## ⚡ Usage

See [action.yml](action.yml)

### Delete an individual artifact

```yml
steps:
    - name: Checkout
      uses: actions/checkout@v4

    - name: Create test file
      run: echo hello > test.txt

    - uses: actions/upload-artifact@v4
      with:
          name: my-artifact
          path: test.txt

    - uses: geekyeggo/delete-artifact@v5
      with:
          name: my-artifact
```

### Specify multiple names

```yml
steps:
    - uses: geekyeggo/delete-artifact@v5
      with:
          name: |
              artifact-*
              binary-file
              output
```

## 🚨 Error vs Fail

By default, the action will fail when it was not possible to delete an artifact (with the exception of name mismatches). When the deletion of an artifact is not integral to the success of a workflow, it is possible to error without failure. All errors are logged.

```yml
steps:
    - uses: geekyeggo/delete-artifact@v5
      with:
          name: okay-to-keep
          failOnError: false
```
