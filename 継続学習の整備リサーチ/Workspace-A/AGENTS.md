# Workspace-A の共通指示

この指示の対象は Workspace-A 内の作業。ユーザーの現在の依頼を優先する。

## 作業開始
- 最初に [coding-guidelines](memory/coding-guidelines.md) と [current-context](memory/current-context.md) を開いて読む。
- 設計判断には [architecture-decisions](memory/architecture-decisions.md)、同種の問題には [lessons-learned](memory/lessons-learned.md) も読む。
- 記録と実ファイルに差があれば実ファイルを確認し、食い違いを報告する。過去のチャットを読めたと仮定しない。

## 記録の扱い
- memory の「例」「提案中」は確定ルールとして扱わない。
- ユーザーが明示した継続方針は、今回の依頼の範囲で coding-guidelines に根拠と適用範囲を付けて保存する。
- 一時的な要望を永続ルールへ昇格させない。不明なら提案として残す。
- 終了・引き継ぎを依頼されたら current-context を更新する。未実施の検証を実施済みにしない。
- 秘密情報、個人情報、会話全文を記録しない。必要な判断と事実だけを残す。

## 引き継ぎ
セッション開始・終了、方針の保存、失敗からの知見整理には
[continual-learning Skill](.github/skills/continual-learning/SKILL.md) を使う。
Skill が検出されない場合は、このファイルを明示的に読んで同じ手順を行う。
