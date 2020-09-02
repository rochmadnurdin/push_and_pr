# Push and PR to Other Repo

Sample github action workflow file. 

## Implement

* Generate new [token](https://github.com/settings/tokens/new). Select `repo` scope.
* In your_source_repo/settings/secret , add `API_TOKEN_GITHUB` with your generated token.
* In source repo, put `push_and_pr.yml` in `.github/workflow` with this code:

```yaml
# This CI should run after publish a new release

name: Push to Other Repo and Make a PR

on:
  release:
    types: [published]
  
jobs:
  build:
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
            PR_TO_BRANCH: 'master'
            # You can add multiple source file or folder separate by space
            SRC_DIR: 'docs readme.adoc' 
            DEST_DIR: 'jupyter'
            PREFIX_DEST_FOLDER: 'planet/'
            # You can rename with format source(comma)target
            RENAME: >-
                    jupyter.adoc,readme.adoc
                    jupyter,docs
```

* Create a release and see your action!

## Example

* Source repo: https://github.com/tegarimansyah/Jupyter
* Destination repo: https://github.com/tegarimansyah/destination_repo

## To Do

* More flexible copy command 
* Enable other script to run before push and PR