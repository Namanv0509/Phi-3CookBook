# Whisperを使用したインタラクティブPhi 3 Mini 4K Instructチャットボット

## 概要

Whisperを使用したインタラクティブPhi 3 Mini 4K Instructチャットボットは、ユーザーがMicrosoft Phi 3 Mini 4K instructデモをテキストまたは音声入力で操作できるツールです。このチャットボットは、翻訳、天気の更新、一般的な情報収集など、さまざまなタスクに使用できます。

### 始めに

このチャットボットを使用するには、次の手順に従ってください：

1. 新しい[Jupyterノートブックを開き、提供されたコードを実行します](E2E_Phi-3-mini-4k-instruct-Whispser_Demo.ipynb)
2. ノートブックのメインウィンドウには、テキスト入力ボックスと「送信」ボタンがあるチャットボックスインターフェイスが表示されます。
3. テキストベースのチャットボットを使用するには、テキスト入力ボックスにメッセージを入力し、「送信」ボタンをクリックします。チャットボットは、ノートブック内で直接再生できる音声ファイルで応答します。

**注意**：このツールを使用するには、GPUとMicrosoft Phi-3およびOpenAI Whisperモデルへのアクセスが必要です。これらは音声認識と翻訳に使用されます。

### GPU要件

このデモを実行するには、12GBのGPUメモリが必要です。

**Microsoft-Phi-3-Mini-4K instruct**デモをGPUで実行するためのメモリ要件は、入力データ（音声またはテキスト）のサイズ、使用される翻訳言語、モデルの速度、およびGPU上の利用可能なメモリなど、いくつかの要因に依存します。

一般的に、WhisperモデルはGPU上で実行するように設計されています。Whisperモデルを実行するための推奨最小GPUメモリ量は8GBですが、必要に応じてより大きなメモリ量を処理できます。

大量のデータや高ボリュームのリクエストをモデルで実行する場合、より多くのGPUメモリが必要になる可能性があり、パフォーマンスの問題が発生する可能性があります。異なる構成で使用ケースをテストし、メモリ使用量を監視して、特定のニーズに最適な設定を決定することをお勧めします。

## Whisperを使用したインタラクティブPhi 3 Mini 4K InstructチャットボットのE2Eサンプル

「[Whisperを使用したインタラクティブPhi 3 Mini 4K Instructチャットボット](E2E_Phi-3-mini-4k-instruct-Whispser_Demo.ipynb)」というタイトルのJupyterノートブックは、Microsoft Phi 3 Mini 4K instructデモを使用して音声または書かれたテキスト入力からテキストを生成する方法を示しています。このノートブックには、いくつかの関数が定義されています：

1. `tts_file_name(text)`: この関数は、生成された音声ファイルを保存するためのファイル名を入力テキストに基づいて生成します。
2. `edge_free_tts(chunks_list,speed,voice_name,save_path)`: この関数は、Edge TTS APIを使用して、入力テキストのチャンクリストから音声ファイルを生成します。入力パラメータは、チャンクのリスト、音声速度、音声名、および生成された音声ファイルを保存する出力パスです。
3. `talk(input_text)`: この関数は、Edge TTS APIを使用して音声ファイルを生成し、/content/audioディレクトリ内のランダムなファイル名に保存します。入力パラメータは、音声に変換する入力テキストです。
4. `run_text_prompt(message, chat_history)`: この関数は、Microsoft Phi 3 Mini 4K instructデモを使用してメッセージ入力から音声ファイルを生成し、それをチャット履歴に追加します。
5. `run_audio_prompt(audio, chat_history)`: この関数は、WhisperモデルAPIを使用して音声ファイルをテキストに変換し、それを`run_text_prompt()`関数に渡します。
6. コードは、ユーザーがメッセージを入力したり音声ファイルをアップロードしたりしてPhi 3 Mini 4K instructデモと対話できるGradioアプリを起動します。出力はアプリ内のテキストメッセージとして表示されます。

## トラブルシューティング

Cuda GPUドライバのインストール

1. Linuxアプリケーションが最新であることを確認します

    ```bash
    sudo apt update
    ```

2. Cudaドライバをインストールします

    ```bash
    sudo apt install nvidia-cuda-toolkit
    ```

3. Cudaドライバの場所を登録します

    ```bash
    echo /usr/lib64-nvidia/ >/etc/ld.so.conf.d/libcuda.conf; ldconfig
    ```

4. Nvidia GPUメモリサイズを確認します（12GBのGPUメモリが必要です）

    ```bash
    nvidia-smi
    ```

5. キャッシュを空にする：PyTorchを使用している場合、torch.cuda.empty_cache()を呼び出して、他のGPUアプリケーションが使用できるように未使用のキャッシュメモリをすべて解放できます

    ```python
    torch.cuda.empty_cache()
    ```

6. Nvidia Cudaを確認します

    ```bash
    nvcc --version
    ```

7. Hugging Faceトークンを作成するために次のタスクを実行します。

    - [Hugging Faceトークン設定ページ](https://huggingface.co/settings/tokens)に移動します。
    - **New token**を選択します。
    - 使用するプロジェクト**Name**を入力します。
    - **Type**を**Write**に設定します。

> **注意**
>
> 次のエラーが発生した場合：
>
> ```bash
> /sbin/ldconfig.real: Can't create temporary cache file /etc/ld.so.cache~: Permission denied 
> ```
>
> これを解決するには、ターミナル内で次のコマンドを入力します。
>
> ```bash
> sudo ldconfig
> ```