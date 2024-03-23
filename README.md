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
    "音波ダメージ",
    "スピナー弾数"
  ],
  "サポート": [
    "ブレ軽減",
    "カサ復活時間"
  ],
  "レンジ": [
    "メイントツゲキ塗り"
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
    "length": 4
  },
  {
    "level": 2,
    "length": 4
  },
  {
    "level": 3,
    "length": 54
  }
]
```
