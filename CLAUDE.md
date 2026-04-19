# CLAUDE.md

> このファイルは Claude Code（claude.ai/code CLI）専用の設定ファイルです。
> プロジェクト全体のガイドラインは **AGENTS.md** が正として管理されています。
> 両ファイルは連動して更新してください（どちらかを変更したら、もう一方も確認すること）。

---

## プロジェクト概要

React コードレビューエージェント。ブランチ名または PR 番号を受け取り、React ベストプラクティスに基づくレビューを Strands フレームワーク上で実行する Python 3.12+ プロジェクト。

詳細: AGENTS.md「プロジェクト概要」セクション参照。

---

## よく使うコマンド（クイックリファレンス）

```sh
# 依存インストール
uv pip install -e .

# テスト実行
pytest

# カバレッジ付きテスト
pytest --cov=src --cov-report=term-missing --cov-report=html

# フォーマット
black src/ tests/

# Lint
ruff src/ tests/

# 型チェック
mypy src/
```

---

## 開発フロー（SDD + TDD）

1. 仕様不明点はユーザーに確認する（推測で補完しない）
2. Red: 失敗するテストを書いてから `pytest` で失敗を確認する
3. Green: 最小実装で通す → `pytest` で成功を確認する
4. Refactor: 振る舞いを維持して設計を改善 → `pytest` で回帰がないことを確認する
5. すべての変更は TDD サイクル内でテスト実行を伴うこと
6. 最終的にすべてのラインカバレッジを通過していること

詳細: AGENTS.md「開発フロー」セクション参照。

---

## Claude Code 固有の指示

### ツール使用方針

- ファイルを読む前に Glob でディレクトリ構造を確認する
- `src/frontend_review_agent/` が実装ディレクトリ、`tests/` がテストディレクトリ
- コマンド実行は必ず仮想環境が有効な状態で行う（`.venv` を使用）
- Windows 環境では `.venv\Scripts\activate`、Mac/Linux では `source .venv/bin/activate`

### コーディング規約（必須）

- 型ヒント（Type Hint）は必須
- docstring は Google スタイルを使用
- 依存追加時は `pyproject.toml` を更新する
- PEP8 準拠（ruff / black で自動チェック）

詳細: AGENTS.md「コーディング規約・推奨事項」セクション参照。

### Git・レビュー運用

- 実装作業はすべて worktree 内で行う
- マージは LGTM コメントがついた場合のみ main に行う
- すべてのレビューコメントに reply する（修正の有無にかかわらず）
- マージ後: worktree 削除 → ブランチ削除 → ローカル main を最新化

詳細: AGENTS.md「Git運用」「レビュー運用」セクション参照。

---

## AGENTS.md との同期メモ

| 更新内容 | AGENTS.md | CLAUDE.md |
|---|---|---|
| コマンド変更 | 更新 | 「よく使うコマンド」も更新 |
| 開発フロー変更 | 更新 | 要約箇所も更新 |
| 規約変更 | 更新 | 「コーディング規約」箇所も更新 |
| Claude Code 固有設定 | 不要 | CLAUDE.md のみ更新 |
