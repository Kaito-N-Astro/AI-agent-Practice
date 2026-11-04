# Workspace-A: Copilot Chat のセッション間方針継承サンプル

セッション A の継続方針や作業状況をファイルに保存し、セッション B で読むための最小構成。
ここでの continual learning は「記録の更新と再利用」を指す。モデルの重みの再学習、
会話の自動共有、バックグラウンドの記憶保存は行わない。

## 構成と役割

```text
Workspace-A/
├── AGENTS.md
├── .github/
│   ├── copilot-instructions.md
│   ├── skills/continual-learning/SKILL.md
│   └── hooks/
│       ├── README.md
│       └── continual-learning.json.example
├── memory/
│   ├── coding-guidelines.md
│   ├── lessons-learned.md
│   ├── architecture-decisions.md
│   └── current-context.md
└── README.md
```

| ファイル | 役割・実行性 |
| --- | --- |
| AGENTS.md | 対応するエージェントが読む共通指示。実行コードではない |
| .github/copilot-instructions.md | Copilot のプロジェクト指示。共通指示と記録を読むよう依頼する |
| .github/skills/continual-learning/SKILL.md | 関連タスクで選択・呼出される手順。毎ターン必ず読まれるものではない |
| memory/*.md | 通常の Markdown。名前だけで自動的に記憶として読み込まれる仕組みはない |
| .github/hooks/*.json.example | 未検証の疑似設定。無効状態の参考資料。動く自動化ではない |

## 使い方

1. ZIP を展開し、`Workspace-A` 自体を VS Code のフォルダーとして開く。
2. GitHub Copilot Chat が利用でき、ファイルを読む機能が使えるセッションを選ぶ。
3. Customizations の Instructions / Skills 等で検出を確認する。名称や対応状況はバージョン・セッション実装に依存する。
4. 次の文を新しいチャットに入力する。自動検出に依存せず、ファイルを明示して開始できる。

```text
AGENTS.md、.github/copilot-instructions.md、
memory/coding-guidelines.md、memory/current-context.md を開いて読んでください。
今回適用する方針、現在地、次の行動を要約してください。
必要なら .github/skills/continual-learning/SKILL.md の手順を使ってください。
```

ファイルの参照・ツール実行や References を確認する。読めない場合はファイルをチャットに添付する。
「読んだ」という返答だけで適用を保証したと判断しない。
対応する UI で `/continual-learning` が表示される場合は呼出にも利用できる。
表示されなくても SKILL.md を明示的に読ませる方法は使える。

### セッション A: 方針を保存

```text
今後このプロジェクトでは、公開 API の互換性を維持してください。
継続方針として memory/coding-guidelines.md に、適用範囲と今回の指示を根拠に保存してください。
```

終了前に次を入力する。

```text
今回はここまでです。continual-learning の手順で、完了・未完了、
変更ファイル、実施した検証、次の行動を memory/current-context.md に保存してください。
教訓や設計判断があれば対応する記録も更新し、差分を説明してください。
```

### セッション B: 再利用

別の新しいチャットで開始用の文を入力し、保存した方針が実際に適用されるか確認する。
A が保存していない内容は継承できない。別 PC・別 checkout では同じ記録も渡す。
ソース管理する場合は差分を確認して記録をコミットする。ZIP 内に Git リポジトリは含まれない。

## スコープと注意点

この構成はプロジェクト内の指示であり、ユーザー共通設定を変更しない。
ただし `.github` はアクセス制御や隔離の境界ではない。親リポジトリの探索、
複数ルート、個人・組織の指示、ツールの権限も別途影響する。
フォルダーを作っただけで、プロジェクト外への操作が技術的に禁止されるわけではない。

AGENTS.md と copilot-instructions.md の特別な優先順位に依存せず、
正本を一つにして矛盾を避ける。現在のユーザー指示と記録が食い違えば、差を説明して現在の依頼に従う。
指示はモデルの行動を導くもので、遵守や記録更新を保証するものではない。

hooks の実行ファイルや有効な JSON 設定、VS Code 設定、依存関係、テスト環境は含めていない。
突然のチャット終了で自動保存されることも想定しない。終了前に明示的に更新する。
本パッケージは構造サンプルであり、利用者環境での実動作は未検証。

## 公式資料

2026-11-05 に参照。対応状況は更新されるため導入時に確認する。

- [VS Code: Custom instructions](https://code.visualstudio.com/docs/agent-customization/custom-instructions)
- [VS Code: Agent Skills](https://code.visualstudio.com/docs/agent-customization/agent-skills)
- [VS Code: Hooks（Preview）](https://code.visualstudio.com/docs/agent-customization/hooks)
- [GitHub: Customization cheat sheet](https://docs.github.com/en/copilot/reference/customization-cheat-sheet)
