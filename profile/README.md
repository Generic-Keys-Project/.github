# Generic Keys

**Generic Keys** は、
**アプリケーションに依存しない「操作（Action）」を中心にした入力抽象化フレームワーク／プロトコル**です。

キーボード、マウス、ゲームパッド、タブレット、OSC、MIDI、ネットワーク入力など
**あらゆる入力を「何をしたいか（Intent）」として統一的に扱う**ことを目的としています。

---

## 🎯 何を解決するのか

* アプリごとにバラバラなキーバインド
* ソフト間で共有できない操作体系
* UI フレームワークに強く依存したショートカット実装
* 外部デバイスや自作デバイスとの連携の難しさ

Generic Keys はこれらを
**「操作は UI とは独立した第一級の概念である」**
という立場で再設計します。

---

## 🧠 基本思想

### 操作は UI ではなく PUI（Physical User Interface）

* ボタン、キー、軸、ジェスチャは **入力**
* Generic Keys が扱うのは **操作（redo / undo / zoom / move / rotate …）**
* UI・GUI・TUI・CLI・ネットワークはすべて同列のプレゼンテーション層

---

### Path ベースの操作

操作はパスで表現されます：

```
/general/undo
/general/redo
/app/view/zoom
/app/object/transform/move
```

* REST / OSC / Express 風の階層構造
* アプリ・デバイス非依存
* 列挙・補完・検証が可能

---

### トランスポート非依存

Generic Keys 自体は **通信手段を持ちません**。

* OSC
* MQTT
* WebSocket
* StdIO
* In-process

など、用途に応じて差し替え可能です。

---

## 🧩 構成リポジトリ

この Organization には以下の役割別リポジトリが配置されます。

### 📐 Specification

* `generic-keys-spec`

  * プロトコル仕様
  * パス設計
  * Payload / StatusCode
  * ライフサイクル（hi / die / focus）

---

### 🧠 Core / SDK

* `generic-keys-core`

  * Host / Client 抽象
  * Action / Axis / Value モデル
  * Serializer / Transport インターフェース

---

### 🔌 Transport 実装

* `generic-keys-transport-osc`
* `generic-keys-transport-mqtt`
* `generic-keys-transport-ws`
* etc.

---

### 🧪 Reference / Example

* `generic-keys-example-blender`
* `generic-keys-example-cli`
* `generic-keys-example-device`

---

### ⌨️ Integration / Tooling

* Keybind YAML
* Catalog / Operator List
* Converter / Validator
* CLI / Debug tools

---

## ✨ ユースケース例

* Blender / Unity / Unreal 間で共通の操作体系を持ちたい
* 左手デバイス・フットペダル・自作キーボードをアプリ横断で使いたい
* VR / AR / 3D 制作で操作の一貫性を保ちたい
* キーバインドを **共有・バックアップ・バージョン管理**したい
* GUI を持たないアプリでも「操作」を公開したい

---

## 🚧 ステータス

* 🧪 Experimental
* 仕様・API は流動的です
* 破壊的変更を含む可能性があります

ただし、

> **思想と方向性は安定しています**

---

## 🤝 コントリビュート

* Issue / Discussion 大歓迎
* 実装言語は問いません
* Transport / Example / Adapter だけの追加も歓迎します

---

## 📜 ライセンス

* 各リポジトリに準拠
  （基本は MIT / Apache-2.0 を想定）

---

## 🔑 最後に

Generic Keys は
**「ショートカットは設定ではなく、設計である」**
という考えから生まれています。

GUI の外へ、
デバイスの外へ、
アプリケーションの外へ。

操作を解放しましょう。
