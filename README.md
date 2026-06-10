KASHIKA (可視化) - Global Open Policy Ledger
KASHIKAは、感情ではなく「データ（事実）」で政治と社会インフラをリファクタリングするための、自律分散型のシビックテック・プラットフォームです。国が作った古いシステムや不透明なプロセスを、市民の側の技術と労働力によって構造化データ（JSON）へとアップデートし、世界中で「信頼の循環」を半永続化させることを目指します。

🏛 基本理念（プロジェクトの憲法）
Facts Only (事実のみを扱う) 政治的な偏向、感情的な批判、スキャンダルは一切扱いません。記録（ログ）に基づく構造化データのみをプラットフォームの土台とします。
Identity & Accountability (責任と貢献の可視化) 「誰が、どの一次ソースを基にデータ化したか」を明確にします。検証された個人や団体には、行動実績に応じてSBT（Soulbound Token）がシステムから自動付与され、ガバナンスの信頼度係数となります。
Decentralized Multi-National Hub (自律分散型の多国籍ハブ) 情報は「それがあるべき場所（現地の国フォルダ）」で、最も詳しい現地の人々が作成します。他国はそれをコピーして囲い込むのではなく、共通語（英語）を介してポインタ参照し、翻訳データを元リポジトリへ「寄贈」する形で世界中の知見を同期します。
🌐 グローバル・ローカリゼーションルール
自国（Local）フォルダのルール: 自国の政策データを書き出す際は、必ず「現地語」に加えて、世界共通語である「英語（global）」のテキストを内包させてください。

他国（Global）事例の翻訳ルール: 日本側が海外（例: インドフォルダ 91/）の先行事例を参照・翻訳したい場合、日本側にコピーを作るのではなく、海外リポジトリの該当フォルダ内に _ja.json の形式で翻訳ファイルをプルリクエスト（寄贈）してください。

🏛 帝国期・旧外地データ（1895〜1945）の取扱における2つの鉄則
大日本帝国期における満州、台湾、朝鮮半島、東南アジア（南方軍政期）等の法整備やインフラ投資は、戦後の日本型官僚機構や社会システムの「プロトタイプ（実験場）」となっていたファクトが存在するため、本プロジェクトの追跡対象に含みます。ただし、歴史的・政治的に極めて繊細な領域であるため、国際社会のデータ（格子）と不必要な衝突を起こさないよう、以下の2つの鉄則を厳守してください。

① 「設計仕様書（ファクト）」に徹し、形容詞を排除する
政治的な善悪、主観的な評価（例：「近代化に貢献した」「搾取・植民地支配を行った」等）は人間の感情と解釈の領域であり、本プラットフォームでは一切扱いません。記録（ログ）に存在するデータ構造のみを記述してください。

❌ NG（形容詞・主観の混入）: 「日本が現地インフラの近代化と発展に大きく寄与した」 「抑圧的な軍政によって現地の物資を不当に剥奪した」
⭕ OK（純粋なファクトログ）: 「1938年、当時の大蔵省から満州国政府へ〇〇円の資金移動（ソース：大蔵省昭和財政史）」 「台湾総督府令第〇号に基づく、土地権利関係の近代化（構造化データ化）の執行ログ」
② 他国ゲートとの「相互参照（ポインタ結合）」を前提とする
日本側（81）のフォルダに格納するデータは、あくまで「日本側の公文書や予算から抽出した設計データ」です。 将来、台湾（886）や他の国・地域の独立ゲート（リポジトリ）が立ち上がった際、彼らが「現地側の視点・1次資料」に基づくデータを蓄積した場合、フロントエンド（画面）は双方のデータを1つのタイムライン上でカチッと結合（相互ポインタ参照）して可視化します。

自国のデータだけで歴史を完結させようとせず、他国リポジトリと接続可能な「開かれた格子」としてJSONを設計してください。

📂 フォルダの雛形（Directory Structure）
リポジトリは国際電話番号（国番号）の格子によってディレクトリが分離されています。これによって各国の独立性とマージ時の衝突回避を担保します。

kashika-core/
├── schema.json                 # 世界共通データ定義書
├── README.md                   # 本ドキュメント
├── 1/                          # 北米（アメリカ・カナダ等）
├── 81/                         # 日本（Japan）
│   ├── config.json             # 日本国内の設定・所属団体インデックス
│   └── policies/               # 政策・法案フォルダ（日本語＋英語必須）
│       └── 81_digital_infra.json
├── 886/                        # 台湾（Taiwan）
└── 91/                         # インド（India）
    └── policies/
        ├── 91_aadhaar.json     # 本家（インド語/英語）
        └── 91_aadhaar_ja.json  # 日本人コントリビューターが「寄贈」した日本語訳


Json形式記載例　コピーしてつかってください

{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "title": "KASHIKA Core Registry & Cross-Gate Mapping Schema",
  "description": "世界共通のアドレス帳、および国を跨いだデータのポインタ結合・自動矛盾検知（コンフリクトマーク）を定義するコア仕様書。",
  "type": "object",
  "required": [
    "version",
    "gates",
    "cross_gate_mappings"
  ],
  "properties": {
    "version": {
      "type": "string",
      "description": "コアスキーマのバージョン（セマンティックバージョニング）"
    },
    "gates": {
      "type": "array",
      "description": "世界に分散する独立ゲート（各国のリポジトリ）のアドレス帳",
      "items": {
        "type": "object",
        "required": [
          "gate_code",
          "country_name",
          "repository_url"
        ],
        "properties": {
          "gate_code": {
            "type": "string",
            "pattern": "^[0-9]+$",
            "description": "国際電話国番号をベースとしたリポジトリの識別子（例：日本='81', 台湾='886'）"
          },
          "country_name": {
            "type": "string",
            "description": "国・地域名（英語表記推奨）"
          },
          "repository_url": {
            "type": "string",
            "format": "uri",
            "description": "該当ゲートが管理されている公開リポジトリ（GitHub等）のURL"
          }
        }
      }
    },
    "cross_gate_mappings": {
      "type": "array",
      "description": "ARCHITECT（接続兵）が定義する、異なるゲート間における同一事象データのポインタ結合リスト。システムが自動で矛盾を検知する格子を形成します。",
      "items": {
        "type": "object",
        "required": [
          "mapping_id",
          "event_name",
          "assertion_target",
          "connections"
        ],
        "properties": {
          "mapping_id": {
            "type": "string",
            "description": "マッピングデータの一意のID（例：map_1935_railway_budget）"
          },
          "event_name": {
            "type": "string",
            "description": "格子上で結合する事象の名称（人間の可視化用）"
          },
          "assertion_target": {
            "type": "string",
            "enum": [
              "value",
              "date",
              "status"
            ],
            "description": "システムが自動バリデーション（不一致検証）を実行する対象フィールド。数値、日付、ステータス等を指定。"
          },
          "connections": {
            "type": "array",
            "description": "結合対象となる各ゲートのデータへの絶対ポインタ。最低2つ以上のポインタが必要です。",
            "minItems": 2,
            "items": {
              "type": "object",
              "required": [
                "gate_code",
                "file_path",
                "fact_id"
              ],
              "properties": {
                "gate_code": {
                  "type": "string",
                  "description": "参照先ターゲットの国番号ゲート（例：'81'）"
                },
                "file_path": {
                  "type": "string",
                  "description": "リポジトリ内における該当JSONファイルへの相対パス（例：'eras/1895_1945_imperial_era/policies/81_southern_military.json'）"
                },
                "fact_id": {
                  "type": "string",
                  "description": "ファイル内で定義されている、アサーション（比較）対象のファクトデータID"
                }
              }
            }
          }
        }
      }
    }
  }
}
