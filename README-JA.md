# GitHub MCP サーバー

GitHub MCP サーバーは [Model Context Protocol (MCP)](https://modelcontextprotocol.io/introduction) サーバーであり、GitHub API とのシームレスな統合を提供し、開発者やツール向けに高度な自動化およびインタラクション機能を可能にします。

[![VS Code で Docker を使用してインストール](https://img.shields.io/badge/VS_Code-Install_Server-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect/mcp/install?name=github&inputs=%5B%7B%22id%22%3A%22github_token%22%2C%22type%22%3A%22promptString%22%2C%22description%22%3A%22GitHub%20Personal%20Access%20Token%22%2C%22password%22%3Atrue%7D%5D&config=%7B%22command%22%3A%22docker%22%2C%22args%22%3A%5B%22run%22%2C%22-i%22%2C%22--rm%22%2C%22-e%22%2C%22GITHUB_PERSONAL_ACCESS_TOKEN%22%2C%22ghcr.io%2Fgithub%2Fgithub-mcp-server%22%5D%2C%22env%22%3A%7B%22GITHUB_PERSONAL_ACCESS_TOKEN%22%3A%22%24%7Binput%3Agithub_token%7D%22%7D%7D) [![VS Code Insiders で Docker を使用してインストール](https://img.shields.io/badge/VS_Code_Insiders-Install_Server-24bfa5?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect/mcp/install?name=github&inputs=%5B%7B%22id%22%3A%22github_token%22%2C%22type%22%3A%22promptString%22%2C%22description%22%3A%22GitHub%20Personal%20Access%20Token%22%2C%22password%22%3Atrue%7D%5D&config=%7B%22command%22%3A%22docker%22%2C%22args%22%3A%5B%22run%22%2C%22-i%22%2C%22--rm%22%2C%22-e%22%2C%22GITHUB_PERSONAL_ACCESS_TOKEN%22%2C%22ghcr.io%2Fgithub%2Fgithub-mcp-server%22%5D%2C%22env%22%3A%7B%22GITHUB_PERSONAL_ACCESS_TOKEN%22%3A%22%24%7Binput%3Agithub_token%7D%22%7D%7D&quality=insiders)

## 使用例

- GitHub ワークフローやプロセスの自動化。
- GitHub リポジトリからのデータ抽出と分析。
- GitHub エコシステムと連携する AI ツールやアプリケーションの構築。

## 前提条件

1. サーバーをコンテナで実行するには、[Docker](https://www.docker.com/) をインストールする必要があります。
2. [GitHub Personal Access Token を作成](https://github.com/settings/personal-access-tokens/new)してください。
   MCP サーバーは多くの GitHub API を使用できるため、AI ツールに許可したい権限を有効にしてください（アクセストークンの詳細については、[ドキュメント](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens) を参照してください）。

## インストール

### VS Code を使用する場合

クイックインストールには、この README の上部にあるワンクリックインストールボタンを使用してください。

手動インストールの場合、以下の JSON ブロックを VS Code のユーザー設定 (JSON) ファイルに追加します。`Ctrl + Shift + P` を押して `Preferences: Open User Settings (JSON)` と入力することで設定を開くことができます。

オプションとして、ワークスペース内の `.vscode/mcp.json` ファイルに追加することもできます。これにより、設定を他の人と共有できます。

> `.vscode/mcp.json` ファイルでは `mcp` キーは不要です。

```json
{
  "mcp": {
    "inputs": [
      {
        "type": "promptString",
        "id": "github_token",
        "description": "GitHub Personal Access Token",
        "password": true
      }
    ],
    "servers": {
      "github": {
        "command": "docker",
        "args": [
          "run",
          "-i",
          "--rm",
          "-e",
          "GITHUB_PERSONAL_ACCESS_TOKEN",
          "ghcr.io/github/github-mcp-server"
        ],
        "env": {
          "GITHUB_PERSONAL_ACCESS_TOKEN": "${input:github_token}"
        }
      }
    }
  }
}