# 通信仕様

## 概要

- ルーティングについて
  - リソースがid, number, selectorにより指定できるルーティングは、指定を省略すると最初の要素を自動的に指定する。 ex. `/player` = `/player/1`
- `Reliable` のAPIはリクエストの到達が保証される。 `UnReliable` は保証されない。具体的には、 `Realiable` はTCP, `Unrealiable` はUDPで通信される（またはそれに相当するプロトコル）。

## State

State(状態)はサーバーが持ち、クライアントはそれをレプリケーションする。基本的には双方向の通信に基づいてベストエフォートで同期する。
同じStateであれば、ゲームの進行状況などの状態が一致する。

```json
{
    "player": {
        "inventory-items": [
            { "medipack": 3 }
            { "heavy-bullet": 10 }
            ],
        "achieved": {
        "beated-level-1": true,
        "beated-level-2": false,
        }
    },
    "director": {
        "gameplay": {
            "mode": "in-game",
            "level": "swamp",
        },
        "instances": [
            {
                "id": "player-1",
                "device-class": "player-kitune",
                "transform": {
                    "location": { "x": 1.23, "y": 2.34, "z": 5.67 },
                    "rotation": {},
                    "scale": {}
                },
                "animation-state": {}
            },
            {
                "id": "enemy-tanuki-1",
                "device-class": "enemy-tanuki",
            },
            {
                "id": "lazer-bullet-1",
                "device-class": "lazer-bullet",
            }
        ]
    },
}
```

## Front -> BFF

- /player/[ id, number ]
  - interaction プレイヤーのインタラクションを報告する。ボタン操作(Stick, A, X, RT...)を一段抽象化した形式。プレイヤーキャラクター（ゲーム内オブジェクト）等の動作は直接的には関係しない。
    - in-game
      - move
        - to-direction
        - to-point
      - attack/[ number ]
      - aim
      - interact
    - ui-general メニューなどの平面的な要素に対する操作
      - point-to-screen/[ X, Y ]
      - point-to-element/[ query-selector, id ]

## BFF -> Front

- /director すべての演出に関するルーティング。
  - gameplay ゲームプレイに関するロジック
    - mode ゲームモード。特に操作体系に関係する。
      - splash
      - title-menu
      - in-game
      - loading
    - level
      - load/[ selector ]
    - instance
      - spawn
      - remove
    - character
      - spawn
      - die
      - killed
  - sound
    - devices/[ id, number ]
    - channel
  - visual
    - camera
    - post-process
    - ...
- /system-exclusive
  - unity-editor
    - play-mode
    - up
    - shutdown
    - shipment
