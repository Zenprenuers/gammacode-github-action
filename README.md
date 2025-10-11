# GammaCode GitHub Action

Integrate GammaCode AI assistant into your GitHub workflows for automated issue resolution and code improvements.

## ⚡ Quick Setup

### Prerequisites

- **Pro Subscription**: API key authentication requires a GammaCode Pro subscription
- **API Key**: Generate your API key from [GammaCode Settings](https://app.gammacode.dev/settings)

### 1. Add API Key to Repository Secrets

1. Go to your repository Settings → Secrets and variables → Actions
2. Click "New repository secret"
3. Name: `GAMMACODE_API_KEY`
4. Value: Your GammaCode API key (starts with `zak_`)

### 2. Create Workflow File

Create `.github/workflows/gammacode.yml`:

```yaml
name: GammaCode AI Assistant

on:
  issue_comment:
    types: [created]

jobs:
  gammacode:
    if: contains(github.event.comment.body, '/gammacode') || contains(github.event.comment.body, '/gc')
    runs-on: ubuntu-latest

    permissions:
      contents: write
      issues: write
      pull-requests: write

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Run GammaCode
        uses: Zenprenuers/gammacode-github-action@main
        with:
          api-key: ${{ secrets.GAMMACODE_API_KEY }}
          share: true # Optional: share session for debugging
```

### 3. Usage

Comment on any issue or pull request with:

- `/gammacode` - General AI assistance
- `/gc` - Short alias
- `/gammacode fix the bug in user authentication` - Specific request

## 🔧 Configuration

### Inputs

| Input     | Description                                   | Required | Default        |
| --------- | --------------------------------------------- | -------- | -------------- |
| `api-key` | GammaCode API key (Pro subscription required) | ✅       | -              |
| `share`   | Share the GammaCode session publicly          | ❌       | `true`         |
| `token`   | Custom GitHub token (optional)                | ❌       | Auto-generated |

### Example with Custom Configuration

```yaml
- name: Run GammaCode
  uses: Zenprenuers/gammacode-github-action@main
  with:
    api-key: ${{ secrets.GAMMACODE_API_KEY }}
    share: false # Keep sessions private
    token: ${{ secrets.MY_GITHUB_TOKEN }} # Use custom token
```

## 🚀 Features

- **Smart Issue Resolution**: Automatically analyze and fix issues
- **Pull Request Reviews**: Provide intelligent code review suggestions
- **File Attachments**: Support for images and file uploads in comments
- **Branch Management**: Automatically create branches and PRs for fixes
- **Secure Authentication**: API key-based authentication with proper validation

## 🛡 Security

- API keys are securely validated before execution
- Only Pro subscribers can use headless mode
- Proper permission checks for repository access
- Temporary files are cleaned up after processing

## 📋 Requirements

- GammaCode Pro subscription
- Valid API key with `cli:auth` permission
- Repository write permissions for the GitHub App
- Ubuntu runner (recommended)

## 🔍 Troubleshooting

### Common Errors

**"Invalid or expired GammaCode API key"**

- Verify your API key is correct in repository secrets
- Check that your API key hasn't expired
- Ensure the key starts with `zak_`

**"Pro subscription required"**

- Upgrade to GammaCode Pro at [app.gammacode.dev](https://app.gammacode.dev)
- API key authentication is only available for Pro users

**"API key lacks required permissions"**

- Regenerate your API key with `cli:auth` permission
- Ensure the key was created with the correct permissions

### Getting Help

- [GammaCode Documentation](https://docs.gammacode.dev)
- [Support](https://gammacode.dev/support)
- [GitHub Issues](https://github.com/Zenprenuers/gammacode-github-action/issues)

## 📝 License

This action is part of the GammaCode project. See [LICENSE](LICENSE) for details.
