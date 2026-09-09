## Link to ticket system added
This step adds a link to the ticket system of your choice so that users can easily view the ticketfor context.
```yaml
- uses: DeboNL/github-actions/add-ticket-link-to-description@v1
  with:
    ticketBaseUrl: https://example.atlassian.net/browse/ # required
    issuePattern: '([a-z]{2}\-\d+)' # Optional, default is '([a-zA-Z]{1,5}-\d{1,9})', 'EXAM-12345', 'ABC-112233', 'xyz-9876'
```