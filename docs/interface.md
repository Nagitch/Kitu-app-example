# 通信仕様

## 概要

- ルーティングについて
    - リソースがid, number, selectorにより指定できるルーティングは、指定を省略すると最初の要素を自動的に指定する。 ex. `/player` = `/player/1`
- `Reliable` のAPIはリクエストの到達が保証される。 `UnReliable` は保証されない。具体的には、 `Realiable` はTCP, `Unrealiable` はUDPで通信される。

## Front -> BFF

- /player/[ id, number ]
    - interaction プレイヤーのインタラクションを報告する。ボタン操作(Stick, A, X, RT...)を一段抽象化した形式。プレイヤーキャラクター（ゲーム内オブジェクト）等の動作とは直接的には関係しない。
        - in-game 
            - move
                - to-direction
                - to-point
            - attack/[ number ]
            - aim
            - interact
        - ui-general メニューなどの平面的な要素に対する操作
            - point-to-screen/[ X, Y ]
            - point-to-instance/[ query-selector, id ]

## BFF -> Front

- /director すべての演出に関するルーティング。
    - gameplay ゲームプレイに関するロジック
        - mode
            - splash
            - title-menu
            - in-game
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
