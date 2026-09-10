## Link to ticket system added
This step adds a link to the ticket system of your choice so that users can easily view the ticketfor context.
```yaml
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
Adds Tag Based releasing to Forge. Create a Release in Github and use the tag to sync Forge

```yaml
name: Deploy webhook

on:
  release:
    types: [published, released]

jobs:
  deploy:
    uses: DeboNL/github-actions/.github/workflows/deploy-forge.yml@v1
    secrets:
      # Both staging and production are optional. You can have one or both (or none)
      stagingServerId: 112233 
      stagingSiteId: 112233
      productionServerId: 112233
      productionSiteId: 112233
      organization: 112233
      apiToken: ${{ secrets.FORGE_API_TOKEN }}
```