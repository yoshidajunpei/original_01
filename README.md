# 基本仕様
【仕様】見積管理システム
・過去見積の参照機能
・決済簡略化機能（チャット機能を持たすことで決済処理をスムーズに対応出来る。）
・原価計算自動化機能
・受注確度ソート表示機能
・アラート表示機能 

## テーブル設計
##Usersテーブル
| Column             | Type   | Options                   |
| ------------------ | ------ | ------------------------- |
| nick_name          | string | null: false               |
| first_name         | string | null: false               |
| first_name_kana    | string | null: false               |
| last_name          | string | null: false               |
| last_name_kana     | string | null: false               |
| email              | string | null: false, unique: true |
| encrypted_passward | string | null: false               |
| birth              | date   | null: false               |
###アソシエーション
- has_many   :Estimates
- has_many   :chats


##Estimatesテーブル
| Column             | Type      | Options                        |
| ------------------ | --------- | ------------------------------ |
| name               | string    | null: false,                   |
| description        | text      | null: false,                   |
| category_id        | integer   | null: false,                   |
| status_id          | integer   | null: false,                   |
| price              | integer   | null: false,                   |
| user               | references| null: false, foreign_key: true |
###アソシエーション
- belongs_to   :user
- has_one      :purchase
- belongs_to_active_hash :category_id
- belongs_to_active_hash :status_id


##Itemテーブル
| Column             | Type       | Options                        |
| ------------------ | ---------- | ------------------------------ |
|   item             | string     | null: false                    |
|   cost_price       | string     | null: false                    |
|   purchase_price   | string     | null: false                    |
|   user             | references | null: false, foreign_key: true |


##chatテーブル
| Column             | Type       | Options                        |
| ------------------ | ---------- | ------------------------------ |
| item               | references | null: false, foreign_key: true |
| user               | references | null: false, foreign_key: true |
###アソシエーション
- belongs_to    :Estimate
- has_one       :delivery
- belongs_to    :user
