# GPT-Chat インタラクションスクリプト

このリポジトリには、OpenAIのGPTベースのモデルと対話するためのPythonスクリプトが含まれています。このスクリプトを使用すると、テキストファイルから入力を読み込み、AIモデルにクエリを送信し、その応答を出力ファイルに保存できます。また、対話履歴を保存することで、セッションを継続することができます。

## 特徴

- OpenAI APIキーを環境変数から取得し、安全にAPIにアクセス
- 指定されたファイルからユーザー入力を読み込み、GPTモデルに送信
- 会話履歴の読み込みと保存が可能で、セッションの継続をサポート
- 応答内容を出力ファイルに保存して簡単にアクセス可能

## 必要条件

- Python 3.x
- [OpenAI Pythonライブラリ](https://beta.openai.com/docs/libraries)
- 環境変数 `OPENAI_API_KEY` に設定されたOpenAI APIキー

## セットアップ

1. **このリポジトリをクローンします:**
   ```bash
   git clone https://github.com/your_username/your_repo_name.git
   cd your_repo_name
   ```

2. **必要なパッケージをインストールします:**
   ```bash
   pip install openai
   ```

3. **OpenAI APIキーを設定します:**
   環境変数としてOpenAI APIキーを設定します。
   ```bash
   export OPENAI_API_KEY="your_openai_api_key"
   ```

## 使い方

### コマンドラインからの実行

スクリプトを以下の形式で実行します。

#### 初期実行：

```bash
python openai-api.py <入力ファイル>
```
- `<入力ファイル>`: ユーザーの入力が記載されたテキストファイルのパス
- 実行すると、「プロジェクト名を入力してください:」と表示されるので、プロジェクト名を入力してください。実行完了後に、指定したプロジェクト名に基づいた「<プロジェクト名>.pickle」という履歴ファイルが作成されます。

#### 2回目以降：

```bash
python openai-api.py <入力ファイル> [履歴ファイル]
```

- `<入力ファイル>`: ユーザーの入力が記載されたテキストファイルのパス
- [履歴ファイル]: 既存のプロジェクトの履歴が記録された pickle ファイルのパス

### 実行例

1. **入力ファイルを準備**します（例: `input.txt`）にユーザーのクエリやプロンプトを記入します。
2. スクリプトを実行します:
   ```bash
   python openai-api.py input.txt chat_history.pickle
   ```
   このコマンドは `input.txt` の内容をGPTモデルに送信し、AIの応答を `output-[project name].txt` に保存します。`chat_history.pickle` が存在する場合は、以前の状態から対話を継続し、存在しない場合は新規に `.pickle` ファイルが作成されます。

### 出力

GPTモデルからの応答は `output-[project name].txt` にセパレーター付きで追記されます。会話履歴は指定された `.pickle` ファイルにシリアライズされ、継続した対話が可能です。

## エラーハンドリング

API呼び出し中にエラーが発生した場合、エラーメッセージがコンソールに表示されるとともに、`output-[project name].txt` にも保存されます。
