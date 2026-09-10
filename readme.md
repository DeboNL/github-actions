## Link to ticket system adder
This adds a link to the ticket of which the PR originates, so that users can easily view the ticket for context.
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

## Forge Deployer
Adds Tag Based releasing to Forge. Create a Release in Github and use the tag to sync Forge.  
Create a release with label 'pre-release' to push to staging, 'latest' or 'none' for production. You can change a 'pre-release' to either to ALSO push to production

_**Note:** This assumes that you have the Forge deploy already working._
```yaml
name: Deploy webhook

on:
  release:
    types: [published, released]

jobs:
  deploy:
    uses: DeboNL/github-actions/.github/workflows/deploy-forge@v1
    secrets:
      organization: example-company # you can find this in the url: https://forge.laravel.com/example-company
      apiToken: ${{ secrets.FORGE_API_TOKEN }} # https://forge.laravel.com/profile/api -> create token > 'site:create' + 'site:manage-deploys'
      # Both staging and production are optional. You can have one or both (or none)
      stagingServerId: 112233 
      stagingSiteId: 112233
      productionServerId: 112233
      productionSiteId: 112233
```