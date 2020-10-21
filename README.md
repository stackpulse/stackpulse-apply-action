# StackPulse Apply Playbook

![Release][badge_release]
[![GitHub marketplace][badge_marketplace]][link_marketplace]
[![Build][badge_ci]][link_actions]
[![License][badge_license]][link_license]

Github Action for applying automatic Incident Response playbooks and triggers with StackPulse.

This action allows you to apply the GitOps paradigm to managing your StackPulse Incident Response Playbooks (and triggers), implementing the continuous integration and delivery to your _operations-as-code_ processes.

## Configuration

In order to use this action you will need to have a [StackPulse](https://stackpulse.com) account and to create StackPulse API keys. For those who are already subscribed to [StackPulse](https://stackpulse.com), the process is explained in detail in the [documentation](https://docs.stackpulse.io/cli/#generating-api-key-and-secret-for-usage-with-stackpulse-cli).

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
      - uses: stackpulse/stackpulse-apply-playbook@v0.2
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
      - uses: stackpulse/stackpulse-apply-playbook@v0.2
        name: Apply trigger
        with:
          clientId: ${{ secrets.SP_CLIENT_ID }}
          clientSecret: ${{ secrets.SP_CLIENT_SECRET }}
          yamlFile: path/to/your/trigger.yaml
          yamlType: trigger
```

### Apply Multiple Playbooks or Triggers Using a Matrix

```yaml
jobs:
  apply-playbook:
    name: An example apply multiple playbooks job
    strategy:
      matrix:
        playbooks: [playbook1.yaml, playbook2.yaml]
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: stackpulse/stackpulse-apply-playbook@v0.2
        name: Apply Playbooks
        with:
          clientId: ${{ secrets.SP_CLIENT_ID }}
          clientSecret: ${{ secrets.SP_CLIENT_SECRET }}
          yamlFile: path/to/your/${{ matrix.playbooks }}
```

## Troubleshooting

Please feel free to open an issue for any problem you may encounter or improvement conceived while using this action.

We will update this sections with common issues or FAQs periodically.

[badge_release]:https://img.shields.io/github/v/release/stackpulse/stackpulse-apply-playbook?include_prereleases&style=flat-square&maxAge=10
[badge_marketplace]:https://img.shields.io/badge/marketplace-stackpulse--apply--playbook-green?logo=github&style=flat-square
[badge_ci]:https://img.shields.io/github/workflow/status/stackpulse/stackpulse-apply-playbook/ci?style=flat-square&maxAge=10
[badge_license]:https://img.shields.io/github/license/stackpulse/stackpulse-apply-playbook.svg?style=flat-square&maxAge=30
[link_actions]:https://github.com/stackpulse/stackpulse-apply-playbook/actions
[link_hub]:https://hub.docker.com/r/avtodev/markdown-lint/
[link_license]:https://github.com/stackpulse/stackpulse-apply-playbook/blob/master/LICENSE
[link_marketplace]:https://github.com/marketplace/actions/stackpulse-apply-playbook
