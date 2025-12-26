* 書籍: MCP入門 生成AIアプリ本格開発
    - [https://gihyo.jp/book/2025/978-4-297-15295-6]

* 付録
   - [https://nova-join-5c4.notion.site/_-1-_Cursor-MCP-272b1102fb33807aab47f754eb815a6a]

* オリジナル
    - [https://github.com/gamasenninn/MCP_Learning/tree/main]

* このリポジトリではオリジナルと異なり chapter09 で使用する基盤モデルを Amazon Bedrock の Anthropic Claude にしている。
    - オリジナルは OpenAI の GPT を使用

* uv のバージョンアップ
  - ```
    uv self update
    ```
* uv 初期化
  ```
  - uv init
  ```

* uv でパッケージを追加
    ```
  - uv add fastmcp
    ```

* uv で Python 実行
  ```
  - uv run python .\calculator_server.py
  ```

* Inspector を MCP サーバーと同時に起動
  - ```
    npx @modelcontextprotocol/inspector uv run python calculator_server.py
    ```

----------------

ファイル名の前に .\ をつけるとエラーになる
npx @modelcontextprotocol/inspector uv run python .\calculator_server.py

C:\Users\tnobe\AppData\Roaming\uv\python\cpython-3.10.17-windows-x86_64-none\python.exe: can't open file 'C:\\Users\\tnobe\\Desktop\\MCP_Learning\\.calculator_server.py': [Errno 2] No such file or directory

------------------

ファイル - 設定 - 開発者 - 設定を編集

C:\Users\tnobe\AppData\Roaming\Claude\claude_desktop_config.json

PowerShell での環境変数の設定は下記のようにする

$env:MCP_TRANSPORT = "http"

パスに全角を含むとパスが認識できずエラーになる

HTTPの場合、Claude Desktop からは直接使えない

下記を実行することで、mcp-proxy経由で使用できる

uv  tool install mcp-proxy 


* Claude Desktop の MCP 構成ファイル
    - C:\Users\tetsu\AppData\Roaming\Claude\claude_desktop_config.json
    - 変更した後は、Claude Desktop を再起動する
        - Windows の場合、Task Manager でゾンビプロセスも必ず終了させてから起動する
```
{
  "mcpServers": {
    "filesystem": {
      "command": "C:\\Program Files\\nodejs\\npx.cmd",
      "args": [
        "-y",
        "@modelcontextprotocol/server-filesystem",
        "C:\\Users\\tetsu\\Desktop",
        "C:\\Users\\tetsu\\Downloads"
      ]
    },
    "universal-tools": {
      "command": "uv",
      "args": [
        "--directory",
        "C:\\Users\\tetsu\\Desktop\\MCPLearning\\chapter08",
        "run",
        "universal_tools_server_exe_3.py"
      ]
    },
    "external_api": {
      "command": "uv",
      "args": [
        "--directory",
        "C:\\Users\\tetsu\\Desktop\\MCPLearning\\chapter07",
        "run",
        "external_api_server.py"
      ]
    },
    "database": {
      "command": "uv",
      "args": [
        "--directory",
        "C:\\Users\\tetsu\\Desktop\\MCPLearning\\chapter06",
        "run",
        "database_server.py"
      ]
    },
    "calculator": {
      "command": "uv",
      "args": [
        "--directory",
        "C:\\Users\\tetsu\\Desktop\\MCPLearning\\chapter03",
        "run",
        "calculator_server.py"
      ]
    }
  },
  "preferences": {
    "menuBarEnabled": true
  }
}
```
