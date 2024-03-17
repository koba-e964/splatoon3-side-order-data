# サイドオーダー (Splatoon3 DLC) 情報まとめ

<big>**ネタバレを含みます! 未プレイの方は閲覧をご遠慮ください!**</big>

## パレットについて
以下が正しい値である。
```
$ toml get palette.toml . | jq 'map_values(length)'
{
  "パワー": 9,
  "サポート": 13,
  "レンジ": 10,
  "ムーブ": 13,
  "ラッキー": 8,
  "ドローン": 9
}
```

フルコンプリートしていないチップは以下のコマンドで列挙できる。
```
toml get palette.toml . | jq 'map_values(map(select(.level != 3).name))'
```

現状は以下の通り。
```
$ toml get palette.toml . | jq 'map_values(map(select(.level != 3).name))'
{
  "パワー": [
    "インクショットダメージ",
    "爆発ダメージ",
    "音波ダメージ",
    "スピナー弾数",
    "メインショットダメージ(近)",
    "メインショットダメージ(遠)",
    "インクパチパチ"
  ],
  "サポート": [
    "インク回復速度",
    "インクネバネバ",
    "ノックバック",
    "爆発ふき飛ばし",
    "ブレ軽減",
    "ホーミング",
    "チャージ時間",
    "カサ復活時間"
  ],
  "レンジ": [
    "メインショットサイズ",
    "メインショット塗り",
    "メイントツゲキ塗り",
    "スペシャル増加量",
    "塗りラッキーコンボ",
    "おそくした敵ダメージ"
  ],
  "ムーブ": [
    "塗り進み速度",
    "スライド回数",
    "移動スペシャル"
  ],
  "ラッキー": [],
  "ドローン": []
}
```

統計情報は以下で出力できる。
```bash
toml get palette.toml . | jq 'to_entries | map(.value) | flatten | group_by(.level) | map({level: .[0].level, length: length})'
```

現状は以下の通り。
```
$ toml get palette.toml . | jq 'to_entries | map(.value) | flatten | group_by(.level) | map({level: .[0].level, length: length})'
[
  {
    "level": 1,
    "length": 13
  },
  {
    "level": 2,
    "length": 11
  },
  {
    "level": 3,
    "length": 38
  }
]
```
