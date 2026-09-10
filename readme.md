**Table of contents**

- [Link to ticket system adder](#link-to-ticket-system-adder)
- [Forge Deployer](#forge-deployer)

## 'Link to ticket system' adder
When a Pull Request gets created it will add a small footer to the description with a link to the ticket. This is based on the branch of the feature.

### Prerequisites / install
_️👉 Apart from creating this file, no further action is required to make this work._ 

```yaml
# .github/workflows/auto-commenter.yml
name: Add relevant data to description

on:
  pull_request:
    types: [opened]

permissions:
  pull-requests: write

jobs:
  comment:
    runs-on: ubuntu-latest

    steps:
      - uses: DeboNL/github-actions/add-ticket-link-to-description@v1
        with:
          ticketBaseUrl: https://example.atlassian.net/browse/ # required
          issuePattern: '([a-z]{2}\-\d+)' # Optional, default is '([a-zA-Z]{1,5}-\d{1,9})', 'EXAM-12345', 'ABC-112233', 'xyz-9876'
```

---

## Forge Deployer
Adds Tag Based releasing to Forge. Create a Release in Github and use the tag to sync Forge.  
Create a release and control with its label where you deploy to:
- Label '_pre-release_' will use the `staging` parameters
- Labels '_latest_' or '_none_' will use `production` parameters.
- When you change a 'pre-release' to '_none_'/'_latest_' it will push to production

### Recommended workflow:
- Have one default branch, e.g. 'main' or 'master'.
- Merge one or more Pull Requests
- Create a release in Github, set a tag and label it with '_pre-release_'
- Verify everything is working as expected, then edit the release to '_latest_' or '_none_'.

### Prerequisites / install
_👉 Add the following file._
_👉 This assumes that you have the Forge deploy already working._
```yaml
# .github/workflows/forge-deployer.yml
name: Deploy webhook

on:
  release:
    types: [published, released]

jobs:
  comment:
    runs-on: ubuntu-latest

    steps:
      - uses: DeboNL/github-actions/forge-deployer@v1
        with:
          organization: example-company # you can find this in the url: https://forge.laravel.com/example-company
          apiToken: ${{ secrets.FORGE_API_TOKEN }} # https://forge.laravel.com/profile/api -> create token > 'site:create' + 'site:manage-deploys'
          # Both staging and production are optional. You can have one or both (or none)
          stagingServerId: 112233 
          stagingSiteId: 112233
          productionServerId: 112233
          productionSiteId: 112233
```
