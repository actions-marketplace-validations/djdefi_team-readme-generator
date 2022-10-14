# team-readme-generator

Action to automatically keep a table of team members up to date in a repository README.

## Example:

### The Team:

<!--auto-team-table-->
| 👤 | Username | Location | Bio |
| --- | --- | --- | --- |
| <img src="https://avatars.githubusercontent.com/u/3662109?v=4" width="30" /> | @djdefi | California | Staff Support Engineer @github  |
| <img src="https://avatars.githubusercontent.com/u/17680929?v=4" width="30" /> | @bevns | California | Software Engineer |
<!--/auto-team-table-->

### About us

We are small but mighty!

## Usage:

1. Configure a workflow such as the example

    ```yaml
    name: "Team README table generator"

    on:

      # Allows you to run this workflow manually from the Actions tab
      workflow_dispatch:
        inputs:
          org:
            description: 'The organization to run the workflow against'
            required: true
            default: 'my-org'
          team:
            description: 'The team to run the workflow against'
            required: true
            default: 'my-team'

    jobs:
      run_team_readme_job:
        runs-on: ubuntu-latest
        name: Run team readme generator
        steps:
          - uses: actions/checkout@v3
          - id: Generate
            uses: djdefi/team-readme-generator@main
            with:
              org: ${{ github.event.inputs.org }}
              team: ${{ github.event.inputs.team }}
              my-pat: ${{ secrets.MY_PAT }}

    ```
1. Setup the README.md by adding the following two tags wherever you want the table to appear:

    ```markdown
    <!--auto-team-table-->
    <!--/auto-team-table-->
    ```
1. Configure `MY_PAT` as an Actions secret. The token needs to have `org:read` and `repo:write` scopes to get team info and create pull requests.
1. Run the the Action workflow with the desired team name.
1. Review and merge the resulting pull requests.
