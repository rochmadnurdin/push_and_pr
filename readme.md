# Push and PR to Other Repo

sample github action workflow file. Put `push_and_pr.yml` in `.github/workflow` with this code:

```yml
# This CI should run after mergin from Pull Request (after editing)

name: Push to Other Repo and Make a PR

on:
 pull_request:
  types: [closed]
  
jobs:
  build:
    if: github.event.pull_request.merged == true
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Push to other repository
        uses: tegarimansyah/push_and_pr@master
        env:
            API_TOKEN_GITHUB: ${{ secrets.API_TOKEN_GITHUB }}

            DEST_GITHUB_USERNAME: 'tegarimansyah'
            DEST_REPO_NAME: 'destination_repo'
            USER_EMAIL: 'test@example.com'
            PUSH_TO_BRANCH: 'from_jupyter'
            PR_TO_BRANCH: 'dev'
            SRC_DIR: 'docs'
            DEST_DIR: 'jupyter'
            PREFIX_DEST_FOLDER: 'planet/'
```