# Django Action

A GitHub action for drawing a Django data model automatically.

## Usage

### Parameters

| Parameter      | Required |       Default       | Description                                                        |
| -------------- | :------: | :-----------------: | ------------------------------------------------------------------ |
| commit_message |   :x:    | Updated data schema | Custom git commit message                                          |
| output_path    |   :x:    |          .          | Output path for generated files (see 'Example Config' for example) |
| pip_path       |   :x:    |  requirements.txt   | Requirements path for the Django project                           |
| project_path   |   :x:    |         ./          | The path to manage.py (see 'Example Config' for example)           |

> Note: The output_path has to exist already.

### Example Config

```yaml
name: Continuous Integration

# This action works with pull requests and pushes
on:
  pull_request:
  push:
    branches:
      - master

jobs:
  graph-models:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v2
        with:
          # Make sure the actual branch is checked out when running on pull requests
          ref: ${{ github.head_ref }}

      - name: Generate Data Schema
        uses: noah-software/django_action@v1.1
        with:
          # This part is also where you can pass other options, for example:
          pip_path: testfolder/app/requirements.txt
          project_path: app/
          output_path: docs/model.png
```

More documentation for writing a workflow can be found [here](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions).

## Issues

Please report all bugs and feature request using the [GitHub issues function](https://github.com/noah-software/django_action/issues/new). Thanks!
