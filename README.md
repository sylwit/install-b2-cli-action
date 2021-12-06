# install-b2-cli-action

[![test-action](https://github.com/sylwit/install-b2-cli-action/workflows/test-action/badge.svg)](https://github.com/sylwit/install-b2-cli-action/actions?query=workflow%3Atest-action)

Install Backblaze b2 CLI on a GitHub Actions Linux host. This action doesn't rely on docker image so is blazing fast.

After this action, every step is capable of running `b2` CLI.

You can set 2 environment variables (secrets) `B2_APPLICATION_KEY_ID` and `B2_APPLICATION_KEY` to authenticate your cli.

### Usage

Add the following step to a job in your workflow

```yaml
- id: install-b2-cli
  uses: sylwit/install-b2-cli-action@v1.0.0
  with:
    version: v3.0.1     # default to latest
  env:
    B2_APPLICATION_KEY_ID: ${{ secrets.B2_APPLICATION_KEY_ID }}
    B2_APPLICATION_KEY: ${{ secrets.B2_APPLICATION_KEY }}
```

### Full example

```yaml
name: Sync app
on:
  push:

jobs:
  sync:
    runs-on: ubuntu-20.04
    steps:
      - uses: actions/checkout@v2.4.0

      - uses: sylwit/install-b2-cli-action@v1.0.0
        env:
          B2_APPLICATION_KEY_ID: ${{ secrets.B2_APPLICATION_KEY_ID }}
          B2_APPLICATION_KEY: ${{ secrets.B2_APPLICATION_KEY }}
      ...

      - name: Sync
        run: b2 sync ./build b2://my_bucket
```

## Authors

Created and maintained by [Sylvain Witmeyer](https://github.com/sylwit)

## License

This project is licensed under the MIT License - see the [LICENSE](https://github.com/sylwit/install-b2-cli-action/blob/master/LICENSE) file for details