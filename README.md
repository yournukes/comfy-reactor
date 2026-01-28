<div align="center">

  <img src="https://github.com/Gourieff/Assets/raw/main/sd-webui-reactor/ReActor_logo_NEW_EN.png?raw=true" alt="logo" width="180px"/>

  ![Version](https://img.shields.io/badge/node_version-0.6.2_beta1-green?style=for-the-badge&labelColor=darkgreen)

  <!--<sup>
  <font color=brightred>

  ## !!! [重要な更新](#latestupdate) !!!<br>既存のワークフローにノードを再追加するのを忘れずに
  
  </font>
  </sup>-->
  
  <a href="https://boosty.to/artgourieff" target="_blank">
    <img src="https://lovemet.ru/img/boosty.jpg" width="108" alt="Boosty で支援"/>
    <br>
    <sup>
      このプロジェクトを支援
    </sup>
  </a>

  <a href="https://t.me/reactor_faceswap" target="_blank"><img src="https://img.shields.io/badge/ReActor-2CA5E0?style=for-the-badge&logo=Telegram&logoColor=white&labelColor=blue"></img></a>
  <a href="https://t.me/artgourieff" target="_blank"><img src="https://img.shields.io/badge/ArtGourieff-2CA5E0?style=for-the-badge&logo=Telegram&logoColor=white&labelColor=blue"></img></a>

  <hr>
  
  [![Commit activity](https://img.shields.io/github/commit-activity/t/Gourieff/ComfyUI-ReActor/main?cacheSeconds=0)](https://github.com/Gourieff/ComfyUI-ReActor/commits/main)
  ![Last commit](https://img.shields.io/github/last-commit/Gourieff/ComfyUI-ReActor/main?cacheSeconds=0)
  [![Opened issues](https://img.shields.io/github/issues/Gourieff/ComfyUI-ReActor?color=red)](https://github.com/Gourieff/ComfyUI-ReActor/issues?cacheSeconds=0)
  [![Closed issues](https://img.shields.io/github/issues-closed/Gourieff/ComfyUI-ReActor?color=green&cacheSeconds=0)](https://github.com/Gourieff/ComfyUI-ReActor/issues?q=is%3Aissue+state%3Aclosed)
  ![License](https://img.shields.io/github/license/Gourieff/ComfyUI-ReActor)

  日本語 | [Русский](/README_RU.md)

# ComfyUI 用 ReActor ノード

</div>

### [ブロックされた ReActor](https://web.archive.org/web/20241230084620/https://github.com/Gourieff/comfyui-reactor-node) をベースにした、ComfyUI 向けの高速で簡単なフェイススワップ拡張ノード

> このノードを使用することで、[責任](#disclaimer)に同意し、受諾したものとみなされます。

<div align="center">

---
[**最新情報**](#latestupdate) | [**インストール**](#installation) | [**使い方**](#usage) | [**トラブルシューティング**](#troubleshooting) | [**更新**](#updating) | [**免責事項**](#disclaimer) | [**クレジット**](#credits) | [**注意!**](#note)

---

</div>

## クイックスタート

とりあえず動かすための最短手順と、よく使う基本設定の概要です。

### 最短手順（ざっくり）

1. **インストール**（[インストール](#installation) を参照）
2. **モデル配置**（[モデル](#models) を参照）
3. **ComfyUI でノードを追加**
   - メニュー `ReActor` から `ReActorFaceSwap` を追加
4. **最低限の接続**
   - `input_image`（ターゲット画像）
   - `source_image`（差し替える顔画像）
5. **実行して結果を確認**

### 基本設定のポイント

- **顔の順序（インデックス）**
  - デフォルトは大きい顔から順に検出します。順序を変えたい場合は `ReActorFaceSwapOpt` + `ReActorOptions` を使ってください。
  - 特定の顔だけを指定したい場合は `source_image` と `input_image` それぞれのインデックスを指定します（例: `0,1,2`）。
- **フェイススワップ強度**
  - `ReActorSetWeight` で強度を 0〜100%（12.5%刻み）で調整できます。
- **フェイス復元**
  - 復元モデルを用意すれば、スワップ後の顔を高品質化できます。モデル配置は [モデル](#models) を参照してください。
- **マスク（精度重視）**
  - `ReActorMaskHelper` を使うと、顔の切り抜き精度が上がります。精度優先のときにおすすめです。

<a name="latestupdate">

## 最新アップデート情報

### 0.6.2 <sub><sup>BETA1</sup></sub>

- FaceFusion Labs の HyperSwap モデルに対応（貢献してくれた [@Buumcode](https://github.com/Buumcode) に感謝）<br>[こちら](https://huggingface.co/facefusion/models-3.3.0/tree/main)からダウンロードできます。<br>(hyperswap_1a_256.onnx, hyperswap_1b_256.onnx, hyperswap_1c_256.onnx)<br>`ComfyUI\models\hyperswap` ディレクトリに配置してください。

<center>
<img src="https://github.com/Gourieff/Assets/blob/main/comfyui-reactor-node/0.6.2-whatsnew-04-3.jpg?raw=true" alt="0.6.2-whatsnew-04-3" width="100%"/>
</center>

Inswapper / Reswapper / HyperSwap の[比較グリッド](https://github.com/Gourieff/Assets/blob/main/comfyui-reactor-node/0.6.2_swapmodels_compare.png)

- 修正と改善

### 0.6.2 <sub><sup>ALPHA2, ALPHA3, ALPHA4</sup></sub>

- 小さいながら重要な修正

### 0.6.2 <sub><sup>ALPHA1</sup></sub>

- [実験的] ついに！フェイス復元が交換された顔のみに適用されます。

<center>
<img src="https://github.com/Gourieff/Assets/blob/main/comfyui-reactor-node/0.6.2-whatsnew-01.jpg?raw=true" alt="0.6.2-whatsnew-01" width="100%"/>
</center>

- [実験的] 新ノード「Restore Face Advanced」とフェイス復元フィルターを追加（"Restore Face Filter" の実装に感謝 https://github.com/Buumcode）<br>このノードで、必要な顔だけに復元プロセスを適用できます。

<center>
<img src="https://github.com/Gourieff/Assets/blob/main/comfyui-reactor-node/0.6.2-whatsnew-02.jpg?raw=true" alt="0.6.2-whatsnew-02" width="100%"/>
</center>

- 「Load Face Model」ノードに FACE_MODEL_NAME 出力を追加

<center>
<img src="https://github.com/Gourieff/Assets/blob/main/comfyui-reactor-node/0.6.2-whatsnew-03.jpg?raw=true" alt="0.6.2-whatsnew-03" width="50%"/>
</center>

### 0.6.1

- 複数顔・複数インデックス向けの性別検出ロジックを改善
- MaskHelper ノードを 2 倍高速化（まだ完璧ではありませんが、従来より 1.5〜2 倍高速）
- 各ステップで ComfyUI のネイティブ ProgressBar を使用
- メインノードに ORIGINAL_IMAGE 出力を追加
- 各種修正と改善（https://github.com/Gourieff/ComfyUI-ReActor/issues/25 の修正）

### 0.6.0

- 新ノード `ReActorSetWeight` を追加。`source_image` または `face_model` のフェイススワップ強度を 0%〜100% まで（12.5%刻み）指定可能。

<center>
<img src="https://github.com/Gourieff/Assets/blob/main/comfyui-reactor-node/0.6.0-whatsnew-01.jpg?raw=true" alt="0.6.0-whatsnew-01" width="100%"/>
<img src="https://github.com/Gourieff/Assets/blob/main/comfyui-reactor-node/0.6.0-whatsnew-02.jpg?raw=true" alt="0.6.0-whatsnew-02" width="100%"/>
<img src="https://github.com/Gourieff/Assets/blob/main/comfyui-reactor-node/0.6.0-alpha1-01.gif?raw=true" alt="0.6.0-whatsnew-03" width="540px"/>
</center>

<details>
	<summary><a>過去のバージョン</a></summary>

### 0.5.2

- ReSwapper モデルに対応。Inswapper が最も類似性が高いものの、ReSwapper は進化中です。@somanchiu https://github.com/somanchiu/ReSwapper の ReSwapper モデルとプロジェクトに感謝！Inswapper の代替をコミュニティで作る大きな一歩です！

<center>
<img src="https://github.com/Gourieff/Assets/blob/main/comfyui-reactor-node/0.5.2-whatsnew-03.jpg?raw=true" alt="0.5.2-whatsnew-03" width="75%"/>
<img src="https://github.com/Gourieff/Assets/blob/main/comfyui-reactor-node/0.5.2-whatsnew-04.jpg?raw=true" alt="0.5.2-whatsnew-04" width="75%"/>
</center>

ReSwapper モデルはこちらからダウンロードできます:
https://huggingface.co/datasets/Gourieff/ReActor/tree/main/models
"models/reswapper" ディレクトリに配置してください。

- 新ノード「Unload ReActor Models」追加。複雑なワークフローで ReActor が使用する VRAM を解放したいときに便利です。

<img src="https://github.com/Gourieff/Assets/blob/main/comfyui-reactor-node/0.5.2-whatsnew-01.jpg?raw=true" alt="0.5.2-whatsnew-01" width="100%"/>

- ORT CoreML と ROCM EP をサポート（必要な onnxruntime をインストールしてください）
- ORT-GPU の最新バージョンをインストールするためのインストールスクリプトを改善

<center>
<img src="https://github.com/Gourieff/Assets/blob/main/comfyui-reactor-node/0.5.2-whatsnew-02.jpg?raw=true" alt="0.5.2-whatsnew-02" width="50%"/>
</center>

- 修正と改善


### 0.5.1

- GPEN 1024/2048 復元モデルに対応（HF データセット https://huggingface.co/datasets/Gourieff/ReActor/tree/main/models/facerestore_models）
- ReActorFaceBoost ノード：スワップされた顔の品質を向上させる試み。`face_size` パラメータに応じて復元＋スケールを行い、inswapper アルゴリズムでターゲットに貼り付けます。詳細は [PR#321](https://github.com/Gourieff/comfyui-reactor-node/pull/321) を参照してください。

<img src="https://github.com/Gourieff/Assets/blob/main/comfyui-reactor-node/0.5.1-whatsnew-01.jpg?raw=true" alt="0.5.1-whatsnew-01" width="100%"/>

[フルサイズのデモプレビュー](https://github.com/Gourieff/Assets/blob/main/comfyui-reactor-node/0.5.1-whatsnew-02.png)

- フェイスモデルのアルファベット順ソート
- 多数の修正と改善

### [0.5.0 <sub><sup>BETA4</sup></sub>](https://web.archive.org/web/20241127121952/https://github.com/Gourieff/comfyui-reactor-node/releases/tag/v0.5.0)

- GFPGAN 用 Spandrel ライブラリ対応

### 0.5.0 <sub><sup>BETA3</sup></sub>

- 修正：「RAM issue」「No detection」(MaskingHelper)

### 0.5.0 <sub><sup>BETA2</sup></sub>

- 既存のフェイスモデルのバッチからブレンドフェイスモデルを作成可能に。"Make Face Model Batch" を追加し、"Load Face Model" で複数モデルを接続してください。
- 画像アナライザーのモジュールで大幅な性能向上！10倍高速化。動画の処理が快適に！

<img src="https://github.com/Gourieff/Assets/blob/main/comfyui-reactor-node/0.5.0-whatsnew-05.png?raw=true" alt="0.5.0-whatsnew-05" width="100%"/>

### 0.5.0 <sub><sup>BETA1</sup></sub>

- Masking Helper ノードに SWAPPED_FACE 出力を追加
- 修正：Masking Helper の IMAGE 出力の A チャンネルが空になる問題を解消

### 0.5.0 <sub><sup>ALPHA1</sup></sub>

- ReActorBuildFaceModel ノードに "face_model" 出力を追加し、ブレンドフェイスモデルをメインノードへ直接渡せるように。

基本ワークフロー [💾](https://github.com/Gourieff/Assets/blob/main/comfyui-reactor-node/workflows/ReActor--Build-Blended-Face-Model--v2.json)

- フェイスマスク機能が利用可能に。"ReActorMaskHelper" を追加し、以下のように接続してください。

<img src="https://github.com/Gourieff/Assets/blob/main/comfyui-reactor-node/0.5.0-whatsnew-01.jpg?raw=true" alt="0.5.0-whatsnew-01" width="100%"/>

"face_yolov8m.pt" Ultralytics モデルがない場合は、[Assets](https://huggingface.co/datasets/Gourieff/ReActor/blob/main/models/detection/bbox/face_yolov8m.pt) からダウンロードして "ComfyUI\models\ultralytics\bbox" に配置してください。<br>
または ["sam_vit_b_01ec64.pth"](https://huggingface.co/datasets/Gourieff/ReActor/blob/main/models/sams/sam_vit_b_01ec64.pth) をダウンロードして "ComfyUI\models\sams" に配置してください。

このノードを使うとフェイススワップの結果を最大限に引き出せます：

<img src="https://github.com/Gourieff/Assets/blob/main/comfyui-reactor-node/0.5.0-whatsnew-02.jpg?raw=true" alt="0.5.0-whatsnew-02" width="100%"/>

- ReActorImageDublicator ノード：動画を作る人向け。1枚の画像を複数フレームに複製して VAE エンコーダに渡せます（例：ライブアバター）。

<img src="https://github.com/Gourieff/Assets/blob/main/comfyui-reactor-node/0.5.0-whatsnew-03.jpg?raw=true" alt="0.5.0-whatsnew-03" width="100%"/>

- ReActorFaceSwapOpt（メインノードの簡易版）と ReActorOptions ノードで追加オプション（新しい "input/source faces separate order"）を設定可能。インデックス順序を自由に指定できます（デフォルトは "大きい順"）。

<img src="https://github.com/Gourieff/Assets/blob/main/comfyui-reactor-node/0.5.0-whatsnew-04.jpg?raw=true" alt="0.5.0-whatsnew-04" width="100%"/>

- ターゲット画像解析の速度を少し向上（ただし、スワップや復元に比べるとまだ遅い）

### [0.4.2](https://web.archive.org/web/20241127034727/https://github.com/Gourieff/comfyui-reactor-node/releases/tag/v0.4.2)

- GPEN-BFR-512 と RestoreFormer_Plus_Plus のフェイス復元モデルに対応

モデルは https://huggingface.co/datasets/Gourieff/ReActor/tree/main/models/facerestore_models からダウンロードできます。<br>`ComfyUI\models\facerestore_models` に配置してください。

<img src="https://github.com/Gourieff/Assets/blob/main/comfyui-reactor-node/0.4.2-whatsnew-04.jpg?raw=true" alt="0.4.2-whatsnew-04" width="100%"/>

- 要望により、複数の人物画像を 1 つのフェイスモデルにブレンド可能に。

ImpactPack の "Make Image Batch" ノードを ReActor の入力に接続し、複数画像をブレンドしてください。

<img src="https://github.com/Gourieff/Assets/blob/main/comfyui-reactor-node/0.4.2-whatsnew-01.jpg?raw=true" alt="0.4.2-whatsnew-01" width="100%"/>

結果例（4 人の女優の顔から作成された新しい顔）:

<img src="https://github.com/Gourieff/Assets/blob/main/comfyui-reactor-node/0.4.2-whatsnew-02.jpg?raw=true" alt="0.4.2-whatsnew-02" width="75%"/>

基本ワークフロー [💾](https://github.com/Gourieff/Assets/blob/main/comfyui-reactor-node/workflows/ReActor--Build-Blended-Face-Model--v1.json)

### [0.4.1](https://web.archive.org/web/20241127044707/https://github.com/Gourieff/comfyui-reactor-node/releases/tag/v0.4.1)

- CUDA 12 をサポート。（Windows）`install.bat` または（Linux/MacOS）`install.py` を ComfyUI の Python 環境で実行するか、CU12 用 ORT-GPU を手動でインストールしてください (https://onnxruntime.ai/docs/install/#install-onnx-runtime-gpu-cuda-12x)
- Issue [comfyui-reactor-node/issues/173](https://web.archive.org/web/20240919043728/https://github.com/Gourieff/comfyui-reactor-node/issues/173) の修正

- フェイス復元の後処理用に専用ノードを追加（FR [comfyui-reactor-node/issues/191](https://web.archive.org/web/20241127040848/https://github.com/Gourieff/comfyui-reactor-node/issues/191)）。ReActor メニュー内に「RestoreFace Node」として表示されます。
- (Windows) Python がシステム PATH にある環境でもインストール可能
- その他の修正・改善

- Face Restore Visibility と CodeFormer Weight (Fidelity) を追加。既存ワークフローではノードを再読み込みしてください。

<img src="https://github.com/Gourieff/Assets/blob/main/comfyui-reactor-node/0.4.1-whatsnew-01.jpg?raw=true" alt="0.4.1-whatsnew-01" width="100%"/>

### [0.4.0](https://web.archive.org/web/20241119155323/https://github.com/Gourieff/comfyui-reactor-node/releases/tag/v0.4.0)

- 入力 "input_image" を先頭に変更。正しいバイパスが可能になり、メイン入力として扱えるようになりました。
- フェイスモデルを "safetensors" 形式で保存可能に（`ComfyUI\models\reactor\faces`）。さまざまなシナリオで軽量なフェイスモデルを使えます。

<img src="https://github.com/Gourieff/Assets/blob/main/comfyui-reactor-node/0.4.0-whatsnew-01.jpg?raw=true" alt="0.4.0-whatsnew-01" width="100%"/>
<img src="https://github.com/Gourieff/Assets/blob/main/comfyui-reactor-node/0.4.0-whatsnew-02.jpg?raw=true" alt="0.4.0-whatsnew-02" width="100%"/>

- 画像から直接フェイスモデルを作成可能に。

<img src="https://github.com/Gourieff/Assets/blob/main/comfyui-reactor-node/0.4.0-whatsnew-03.jpg?raw=true" alt="0.4.0-whatsnew-03" width="50%"/>

- 両方の入力はオプションで、どちらか 1 つを接続すれば OK。両方接続した場合は `image` が優先。
- 各種修正で拡張を改善。

バグ報告や機能提案、支援をしてくださる皆さんに感謝！

</details>

## インストール

<details>
	<summary>Windows 用 <a href="https://github.com/comfyanonymous/ComfyUI">ComfyUI</a>（Standalone/Portable）</summary>

1. 次のいずれかを実施:
   - [Visual Studio 2022](https://visualstudio.microsoft.com/downloads/)（Community 版）をインストール（Insightface ビルドのために必要）
   - もしくは [VS C++ Build Tools](https://visualstudio.microsoft.com/visual-cpp-build-tools/) をインストールし、「Desktop Development with C++」を選択
   - もしくは VS/Build Tools を入れたくない場合は [この手順 (I. 節)](#insightfacebuild) を参照
2. 2 つの方法のいずれかを選択:
   - (ComfyUI Manager) ComfyUI Manager を開き、「Install Custom Nodes」をクリック。検索欄に「ReActor」を入力して「Install」。完了後、サーバーを再起動。
   - (手動) `ComfyUI\custom_nodes` に移動し、コンソールで `git clone https://github.com/Gourieff/ComfyUI-ReActor` を実行
3. `ComfyUI\custom_nodes\ComfyUI-ReActor` に移動し、`install.bat` を実行（ComfyUI の `python_embeded` または `venv` の Python を使用）
4. "face_yolov8m.pt" Ultralytics モデルがない場合は [Assets](https://huggingface.co/datasets/Gourieff/ReActor/blob/main/models/detection/bbox/face_yolov8m.pt) からダウンロードして `ComfyUI\models\ultralytics\bbox` に配置してください。<br>同様に "Sams" モデルのいずれか（または両方）を [こちら](https://huggingface.co/datasets/Gourieff/ReActor/tree/main/models/sams) からダウンロードし、`ComfyUI\models\sams` に配置してください。
5. ComfyUI を起動し、メニュー `ReActor` または検索欄から ReActor ノードを探します。

</details>

## モデル

 - buffalo_l: 初回起動時に `ComfyUI\models\insightface\models\buffalo_l` に自動ダウンロード、または [こちら](https://huggingface.co/datasets/Gourieff/ReActor/tree/main/models) から手動ダウンロード
 - inswapper_128: インストール時に `ComfyUI\models\insightface` にダウンロード、または [こちら](https://huggingface.co/datasets/Gourieff/ReActor/tree/main/models) から手動ダウンロード
 - reswapper_128/256: https://huggingface.co/datasets/Gourieff/ReActor/tree/main/models を `ComfyUI\models\reswapper` に配置
 - hyperswap_256: https://huggingface.co/facefusion/models-3.3.0/tree/main（hyperswap_1a_256.onnx, hyperswap_1b_256.onnx, hyperswap_1a_256.onnx）を `ComfyUI\models\hyperswap` に配置
 - フェイス復元モデル: https://huggingface.co/datasets/Gourieff/ReActor/tree/main/models/facerestore_models から好みのものを `ComfyUI\models\facerestore_models` に配置
 - Ultralytics モデル: https://huggingface.co/datasets/Gourieff/ReActor/blob/main/models/detection/bbox/face_yolov8m.pt を `ComfyUI\models\ultralytics\bbox` に配置
 - SAM モデル: https://huggingface.co/datasets/Gourieff/ReActor/tree/main/models/sams を `ComfyUI\models\sams` に配置

## 使い方

メニュー `ReActor` 内、または検索欄で "ReActor" と入力して ReActor ノードを探せます。

ノード一覧:
- ••• メインノード •••
  - ReActorFaceSwap (メインノード)
  - ReActorFaceSwapOpt (追加オプション入力付きメインノード)
  - ReActorOptions (ReActorFaceSwapOpt 用オプション)
  - ReActorFaceBoost (フェイスブースターノード)
  - ReActorMaskHelper (マスキングヘルパー)
  - ReActorSetWeight (フェイススワップ強度設定)
- ••• フェイスモデル操作 •••
  - ReActorSaveFaceModel (フェイスモデル保存)
  - ReActorLoadFaceModel (フェイスモデル読み込み)
  - ReActorBuildFaceModel (ブレンドフェイスモデル作成)
  - ReActorMakeFaceModelBatch (フェイスモデルバッチ作成)
- ••• 追加ノード •••
  - ReActorRestoreFace (フェイス復元)
  - ReActorImageDublicator (1枚の画像を複数枚に複製)
  - ImageRGBA2RGB (RGBA を RGB に変換)
  - ReActorUnload (VRAM から ReActor モデルを解放)

必要なスロットを接続して実行してください。

### メインノードの入力

- `input_image` - 処理対象の画像（SD WebUI の "target image" に相当）
  - 対応ノード: "Load Image"、"Load Video"、または画像を出力する任意ノード
- `source_image` - `input_image` にスワップする顔画像（SD WebUI の "source image" に相当）
  - 対応ノード: "Load Image"、または画像を出力する任意ノード
- `face_model` - "Load Face Model" ノード、または "Save Face Model" で作成したフェイスモデルファイルの入力
  - 対応ノード: "Load Face Model"、"Build Blended Face Model"
- `options` - ReActorOptions を接続
  - 対応ノード: "ReActorOptions"
- `face_boost` - ReActorFaceBoost を接続
  - 対応ノード: "ReActorFaceBoost"

### メインノードの出力

- `IMAGE` - 出力画像
  - 対応ノード: 画像入力を受ける任意のノード
- `FACE_MODEL` - スワップ処理中に作成されるソース顔のモデル
  - 対応ノード: "Save Face Model"、"ReActor"、"Make Face Model Batch"
- `ORIGINAL_IMAGE` - `input_image` のバイパス

### フェイス復元

バージョン 0.3.0 以降、ReActor ノードには組み込みのフェイス復元機能があります。<br>
使用したいモデルをダウンロードし（[インストール](#installation) を参照）、フェイススワップ中に復元モデルを選択するだけです。顔のディテールが向上し、より正確な結果になります。

### フェイスインデックス

デフォルトでは、ReActor は "大きい顔" から "小さい顔" の順に検出します。<br>
ReActorFaceSwapOpt ノードと ReActorOptions で順序を変更できます。

また、特定の顔を指定する場合は、ソース画像と入力画像のインデックスを指定してください。

最初に検出された顔のインデックスは 0 です。

必要な順番でインデックスを指定できます。<br>
例: ソース 0,1,2 / 入力 1,0,2<br>
→ 入力の 2 番目の顔（index=1）にソースの 1 番目の顔（index=0）が適用されます。

### 性別

検出対象の性別を指定できます。<br>
ReActor は条件を満たす顔のみをスワップします。

### フェイスモデル

バージョン 0.4.0 以降、フェイスモデルを "safetensors" 形式で保存できます（`ComfyUI\models\reactor\faces`）。

"Load Face Model" ノードに新しいモデルを表示するには、ComfyUI のページを更新してください。<br>
（ComfyUI Manager を使うことを推奨します。未保存のワークフローがあると、リロードで失われることがあります。）

### Masking Helper

フェイスマスク機能は 0.5.0 以降で利用できます。"ReActorMaskHelper" をワークフローに追加し、以下のように接続してください：

<img src="https://github.com/Gourieff/Assets/blob/main/comfyui-reactor-node/0.5.0-whatsnew-01.jpg?raw=true" alt="0.5.0-whatsnew-01" width="100%"/>

"face_yolov8m.pt" Ultralytics モデルがない場合は、[Assets](https://huggingface.co/datasets/Gourieff/ReActor/blob/main/models/detection/bbox/face_yolov8m.pt) からダウンロードして `ComfyUI\models\ultralytics\bbox` に配置してください。<br>
または ["sam_vit_b_01ec64.pth"](https://huggingface.co/datasets/Gourieff/ReActor/blob/main/models/sams/sam_vit_b_01ec64.pth) または ["sam_vit_l_0b3195.pth"](https://huggingface.co/datasets/Gourieff/ReActor/blob/main/models/sams/sam_vit_l_0b3195.pth)（遮蔽が多い場合に有利）をダウンロードし、`ComfyUI\models\sams` に配置してください。

このノードを使用すると、フェイススワップの結果を最大限に引き出せます：

<img src="https://github.com/Gourieff/Assets/blob/main/comfyui-reactor-node/0.5.0-whatsnew-02.jpg?raw=true" alt="0.5.0-whatsnew-02" width="100%"/>

### Face Swap Weigth

`ReActorSetWeight` ノードで `source_image` または `face_model` のフェイススワップ強度を 0%〜100%（12.5%刻み）で設定できます。

<center>
<img src="https://github.com/Gourieff/Assets/blob/main/comfyui-reactor-node/0.6.0-whatsnew-01.jpg?raw=true" alt="0.6.0-whatsnew-01" width="100%"/>
</center>

## トラブルシューティング

<a name="insightfacebuild">

### **I. (Windows ユーザー向け) Insightface のビルドに失敗する、または Visual Studio / VS C++ Build Tools を入れたくない場合**

1. （ComfyUI Portable）ルートフォルダで Python のバージョンを確認します:<br>CMD で `python_embeded\python.exe -V` を実行
2. 上記で確認した Python バージョンに合った事前ビルドの Insightface をダウンロードし、ComfyUI のルートフォルダに配置してください（ComfyUI Portable の場合）:<br>
   [Python 3.10 用](https://github.com/Gourieff/Assets/raw/main/Insightface/insightface-0.7.3-cp310-cp310-win_amd64.whl), [Python 3.11 用](https://github.com/Gourieff/Assets/raw/main/Insightface/insightface-0.7.3-cp311-cp311-win_amd64.whl), [Python 3.12 用](https://github.com/Gourieff/Assets/raw/main/Insightface/insightface-0.7.3-cp312-cp312-win_amd64.whl), [Python 3.13 用](https://github.com/Gourieff/Assets/raw/main/Insightface/insightface-0.7.3-cp313-cp313-win_amd64.whl)
3. PIP を更新:<br>
   `python_embeded\python.exe -m pip install -U pip`
4. Insightface をインストール:
  <br>(3.10) `python_embeded\python.exe -m pip install insightface-0.7.3-cp310-cp310-win_amd64.whl`
  <br>(3.11) `python_embeded\python.exe -m pip install insightface-0.7.3-cp311-cp311-win_amd64.whl`
  <br>(3.12) `python_embeded\python.exe -m pip install insightface-0.7.3-cp312-cp312-win_amd64.whl`
  <br>(3.13) `python_embeded\python.exe -m pip install insightface-0.7.3-cp313-cp313-win_amd64.whl`
5. 完了！

### **II. "AttributeError: 'NoneType' object has no attribute 'get'"**

このエラーは `inswapper_128.onnx` モデルファイルが壊れている場合に発生することがあります。

[こちら](https://huggingface.co/datasets/Gourieff/ReActor/resolve/main/models/inswapper_128.onnx)から手動でダウンロードし、`ComfyUI\models\insightface` の既存ファイルと置き換えてください。

### **III. "reactor.execute() got an unexpected keyword argument 'reference_image'"**

最新アップデートで入力ポイントが変更されたことを示します。<br>
現在の ReActor ノードをワークフローから削除し、再追加してください。

### **IV. ReActor ノードと使用時に ControlNet Aux Node の IMPORT 失敗エラー**

1. ComfyUI を終了
2. ComfyUI のルートフォルダで CMD を開き、以下を実行:
   - `python_embeded\python.exe -m pip uninstall -y opencv-python opencv-contrib-python opencv-python-headless`
   - `python_embeded\python.exe -m pip install opencv-python==4.7.0.72`
3. 以上です！

<img src="https://github.com/Gourieff/Assets/blob/main/comfyui-reactor-node/uploads/reactor-w-controlnet.png?raw=true" alt="reactor+controlnet" />

### **V. "ModuleNotFoundError: No module named 'basicsr'" または future-0.18.3 インストール時の "subprocess-exited-with-error"**

- https://github.com/Gourieff/Assets/raw/main/comfyui-reactor-node/future-0.18.3-py3-none-any.whl をダウンロード
- ComfyUI ルートに配置して以下を実行:

      python_embeded\python.exe -m pip install future-0.18.3-py3-none-any.whl

- その後:

      python_embeded\python.exe -m pip install basicsr

### **VI. "fatal: fetch-pack: invalid index-pack output"（`git clone` 時）**

`--depth=1`（最新コミットのみ）でクローンを試してください:

     git clone --depth=1 https://github.com/Gourieff/ComfyUI-ReActor

必要であれば残りを取得:

     git fetch --unshallow

## 更新

この [リポジトリ](https://github.com/Gourieff/sd-webui-extensions-updater) の .bat または .sh スクリプトを `ComfyUI\custom_nodes` に配置し、必要に応じて実行してください。

### 免責事項

このソフトウェアは、急速に拡大する AI 生成メディア産業への生産的な貢献を目的としています。カスタムキャラクターのアニメーションや衣服のモデルとしての利用など、アーティストの作業を支援します。

開発者は、本ソフトウェアが持つ不適切な用途を認識しており、それを防ぐための対策に取り組んでいます。法と倫理に従い、ポジティブな方向でプロジェクトを継続します。

ユーザーは、地域の法律に従い、責任を持って本ソフトウェアを使用する必要があります。実在人物の顔を使用する場合は、関係者の同意を得て、オンライン投稿時にはディープフェイクであることを明記してください。**本ソフトウェアの開発者および貢献者は、エンドユーザーの行為に責任を負いません。**

本拡張を使用することで、次のようなコンテンツを作成しないことに同意したものとみなされます:
- 法律に違反する内容
- 人に危害を加える内容
- 害意を伴う情報（公的・私的を問わず）や画像（公的・私的を問わず）の拡散
- 誤情報の拡散
- 脆弱な人々を標的にすること

本ソフトウェアは、[InsightFace](https://github.com/deepinsight/insightface/) が提供する学習済みモデル `buffalo_l` と `inswapper_128.onnx` を使用しています。これらのモデルは以下の条件に従って提供されます:

[insightface ライセンスより](https://github.com/deepinsight/insightface/tree/master/python-package): InsightFace の学習済みモデルは非商用の研究目的にのみ利用可能です。自動ダウンロード、手動ダウンロードのどちらも対象です。

ユーザーはこれらの利用条件を厳守する必要があります。本ソフトウェアの開発者・メンテナーは、InsightFace の学習済みモデルの誤用に責任を負いません。

商用利用を意図する場合は、自分でモデルを学習するか、商用利用可能なモデルを入手してください。

### モデルのハッシュ

#### 安全に使用できるモデルのハッシュは以下の通りです:

inswapper_128.onnx
```
MD5:a3a155b90354160350efd66fed6b3d80
SHA256:e4a3f08c753cb72d04e10aa0f7dbe3deebbf39567d4ead6dce08e98aa49e16af
```

1k3d68.onnx

```
MD5:6fb94fcdb0055e3638bf9158e6a108f4
SHA256:df5c06b8a0c12e422b2ed8947b8869faa4105387f199c477af038aa01f9a45cc
```

2d106det.onnx

```
MD5:a3613ef9eb3662b4ef88eb90db1fcf26
SHA256:f001b856447c413801ef5c42091ed0cd516fcd21f2d6b79635b1e733a7109dbf
```

det_10g.onnx

```
MD5:4c10eef5c9e168357a16fdd580fa8371
SHA256:5838f7fe053675b1c7a08b633df49e7af5495cee0493c7dcf6697200b85b5b91
```

genderage.onnx

```
MD5:81c77ba87ab38163b0dec6b26f8e2af2
SHA256:4fde69b1c810857b88c64a335084f1c3fe8f01246c9a191b48c7bb756d6652fb
```

w600k_r50.onnx

```
MD5:80248d427976241cbd1343889ed132b3
SHA256:4c06341c33c2ca1f86781dab0e829f88ad5b64be9fba56e56bc9ebdefc619e43
```

**未検証（信頼できない）ソースからモデルをダウンロードした場合は、必ずハッシュを確認してください。**

<a name="credits">

## 感謝とクレジット

<details>
	<summary><a>クリックして展開</a></summary>

<br>

|file|source|license|
|----|------|-------|
|[buffalo_l.zip](https://huggingface.co/datasets/Gourieff/ReActor/blob/main/models/buffalo_l.zip) | [DeepInsight](https://github.com/deepinsight/insightface) | ![license](https://img.shields.io/badge/license-non_commercial-red) |
| [codeformer-v0.1.0.pth](https://huggingface.co/datasets/Gourieff/ReActor/blob/main/models/facerestore_models/codeformer-v0.1.0.pth) | [sczhou](https://github.com/sczhou/CodeFormer) | ![license](https://img.shields.io/badge/license-non_commercial-red) |
| [GFPGANv1.3.pth](https://huggingface.co/datasets/Gourieff/ReActor/blob/main/models/facerestore_models/GFPGANv1.3.pth) | [TencentARC](https://github.com/TencentARC/GFPGAN) | ![license](https://img.shields.io/badge/license-Apache_2.0-green.svg) |
| [GFPGANv1.4.pth](https://huggingface.co/datasets/Gourieff/ReActor/blob/main/models/facerestore_models/GFPGANv1.4.pth) | [TencentARC](https://github.com/TencentARC/GFPGAN) | ![license](https://img.shields.io/badge/license-Apache_2.0-green.svg) |
| [inswapper_128.onnx](https://huggingface.co/datasets/Gourieff/ReActor/resolve/main/models/inswapper_128.onnx) | [DeepInsight](https://github.com/deepinsight/insightface) | ![license](https://img.shields.io/badge/license-non_commercial-red) |
| [inswapper_128_fp16.onnx](https://huggingface.co/datasets/Gourieff/ReActor/resolve/main/models/inswapper_128_fp16.onnx) | [Hillobar](https://github.com/Hillobar/Rope) | ![license](https://img.shields.io/badge/license-non_commercial-red) |

[BasicSR](https://github.com/XPixelGroup/BasicSR) - [@XPixelGroup](https://github.com/XPixelGroup) <br>
[facexlib](https://github.com/xinntao/facexlib) - [@xinntao](https://github.com/xinntao) <br>

[@s0md3v](https://github.com/s0md3v), [@henryruhs](https://github.com/henryruhs) - 元の Roop アプリ <br>
[@ssitu](https://github.com/ssitu) - [ComfyUI_roop](https://github.com/ssitu/ComfyUI_roop) 拡張の初期バージョン

</details>

<a name="note">

### 注意!

**ReActor ノード使用時にエラーが起きた場合、すぐに Issue を立てるのではなく、ワークフロー内の ReActor ノードを一度削除して再追加してみてください。**

**ReActor ノードは随時更新され、新機能が追加されるため、古いノードは動作不良になることがあります。**
