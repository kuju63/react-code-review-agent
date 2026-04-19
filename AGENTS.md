# AGENTS.md

> **同期ファイル**: このファイルはプロジェクトガイドラインの正（source of truth）です。
> Claude Code 用の設定は **CLAUDE.md** に分離されています。
> どちらかを変更した際は、もう一方のファイルも確認・更新してください。

このプロジェクトはモダンなPython環境（pyproject.tomlベース、uv/venv/最新pip推奨）で構築・運用されることを前提としています。

## プロジェクト概要

- プロジェクト名: frontend-review-agent
- エージェント実装には Strands を使用します。
- React のコードレビューエージェントを開発するプロジェクトです。
- ユーザーからレビュー対象のブランチ名または PR 番号を受け取り、それを元に React のベストプラクティスに基づくコードレビューを行います。
- 初期段階のため、ソースコード・テストコードは最小限です。
- src/frontend-review-agent/ ディレクトリ配下に実装ファイルを配置します。
- tests/ ディレクトリ配下にテストファイルを配置します。

## 開発環境

- Python 3.12以上を推奨
- 依存管理: pyproject.toml（uvで管理）
- 仮想環境: venv を利用

### 仮想環境の作成・有効化・無効化

#### Windows

```powershell
python -m venv .venv
.venv\Scripts\activate
# 無効化
deactivate
```

#### Mac/Linux

```sh
python3 -m venv .venv
source .venv/bin/activate
# 無効化
deactivate
```

## ビルド・テスト・実行

- ビルド不要（Pythonスクリプト）
- テスト: pytestを使用（tests/ 配下にテスト追加）
- 依存インストール: uv推奨

### 依存インストール（uv使用）

```sh
uv pip install -r requirements.txt  # requirements.txtが必要な場合
uv pip install -e .                # pyproject.tomlからインストール
```

### テスト実行

```sh
pytest
```

### Coverage取得

```sh
pytest --cov=src --cov-report=term-missing --cov-report=html
```

### フォーマッター実行（black）

```sh
black src/ tests/
```

### Linter実行（ruff）

```sh
ruff src/ tests/
```

### 型チェック（mypy）

```sh
mypy src/
```

### 実行例

```sh
python -m src.frontend-review-agent.main
```

## 開発フロー

- 開発は SDD と TDD を組み合わせて進めます。
- まず仕様を明確化し、期待される振る舞いとレビュー観点を定義してから実装します。
- 仕様を明確化する際は、推測で要件や挙動を補完せず、不明点は必ずユーザーに確認しながら振る舞いを定義します。
- TDD は Red, Green, Refactor のサイクルで進めます。
- Red: 失敗するテストを先に追加し、必ずテストを実行して失敗を確認します。
- Green: テストを通す最小限の実装を追加し、必ずテストを実行して成功を確認します。
- Refactor: 振る舞いを維持したまま設計と実装を改善し、必ずテストを実行して回帰がないことを確認します。
- すべての変更は、各 TDD サイクル内でテスト実行を伴うことを必須とします。
- テストコードは最終的にすべてのラインカバレッジを通過していることを必須とします。

## レビュー運用

- マージは、レビューコメントで LGTM が付いた場合にのみ main ブランチに対して行います。
- LGTM 以外のレビュー指摘については、指摘が誤っている可能性も考慮して妥当性を評価し、必要に応じて修正を行います。
- すべてのレビューコメントには、修正の有無にかかわらず必ず reply を行います。

## Git運用

- 実装作業はすべて worktree 内で行います。
- main へのマージ完了後は、対象 worktree を削除します。
- main へのマージ完了後は、レビュー対象のブランチを削除します。
- main へのマージ完了後は、ローカルの main ブランチを最新状態に更新します。

## コーディング規約・推奨事項

- PEP8/PEP517/PEP518 準拠
- **Type Hint（型ヒント）は必須**（近年のPython開発の標準的な流れに準拠）
- ドキュメンテーションは**Googleスタイルのdocstring**を使用
  - 参考: <https://google.github.io/styleguide/pyguide.html#38-comments-and-docstrings>
- 依存追加時はpyproject.tomlを必ず更新

## 参考

- [pyproject.toml 公式ドキュメント](https://packaging.python.org/en/latest/specifications/pyproject-toml/)
- [PEP8](https://peps.python.org/pep-0008/)
- [Strands Agents Documentation](https://strandsagents.com/)

---
AIエージェントはこのファイルを参照し、プロジェクトの構成・開発方針・コマンド例を把握してください。
