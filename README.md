# ![alt text](https://avatars3.githubusercontent.com/u/59413032?s=48 "OctoPulse") StackPulse Apply Action

Github Action for applying automatic Incident Response playbooks and triggers with StackPulse.

This action allows you to apply the Gitops paradigm to managing your StackPulse Incident Response Playbooks (and triggers), implementing the continuous integration and delivery to your _operations-as-code_ processes. 

## Configuration

In order to use this action you will need to have a [StackPulse](https://stackpulse.com) account and to create a StackPulse API keys. For those who are already subscribed to [StackPulse](https://stackpulse.com), the process is explained in detail in the [documentation](https://docs.stackpulse.io/cli/#generating-api-key-and-secret-for-usage-with-stackpulse-cli).

After creating the API keys we recommend storing them as [Github Secrets](https://docs.github.com/en/actions/reference/encrypted-secrets) in your organization or repository in order to use this action.

> In the examples below StackPulse API client id and secret are stored as `SP_CLIENT_ID` and `SP_CLIENT_SECRET` accordingly.

## Inputs

The following inputs are briefly explained here are fully declared and documented in the [action.yaml](action.yaml):

* `clientId` [**Required**] - Your StackPulse API Client ID

* `clientSecret` [**Required**] - Your StackPulse API Client Secret

* `yamlFile` [**Required**] - Path to the yaml file of the playbook or trigger to apply, only relative path allowed

* `yamlType` - Type of yaml resource to apply, 'playbook' or 'trigger' (default is 'playbook')

## Examples

### Apply a Playbook

```yaml
jobs:
  apply-playbook:
    name: An example apply playbook job
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: stackpulse/stackpulse-apply-action@v0.1
        name: Apply playbook
        with:
          clientId: ${{ secrets.SP_CLIENT_ID }}
          clientSecret: ${{ secrets.SP_CLIENT_SECRET }}
          yamlFile: path/to/your/playbook.yaml
```

### Apply a Trigger

```yaml
jobs:
  apply-playbook:
    name: An example apply trigger job
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: stackpulse/stackpulse-apply-action@v0.1
        name: Apply trigger
        with:
          clientId: ${{ secrets.SP_CLIENT_ID }}
          clientSecret: ${{ secrets.SP_CLIENT_SECRET }}
          yamlFile: path/to/your/trigger.yaml
          yamlType: trigger
```

## Troubleshooting

Please feel free to open an issue for any problem you may encounter or improvement conceived while using this action.

We will update this sections with common issues or FAQs periodically.
