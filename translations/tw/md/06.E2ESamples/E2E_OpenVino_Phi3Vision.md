這個示範展示了如何使用預訓練模型根據圖片和文字提示生成Python代碼。

[Sample Code](../../../../code/06.E2E/E2E_OpenVino_Phi3-vision.ipynb)

以下是逐步說明：

1. **導入和設置**：
   - 導入必要的庫和模組，包括處理圖片的`requests`, `PIL`，以及處理模型和處理的`transformers`。

2. **加載和顯示圖片**：
   - 使用`PIL`庫打開一個圖片文件(`demo.png`)並顯示。

3. **定義提示**：
   - 創建一個包含圖片的消息，並請求生成處理圖片並使用`plt`（matplotlib）保存它的Python代碼。

4. **加載處理器**：
   - 從指定的`out_dir`目錄加載預訓練模型的`AutoProcessor`。這個處理器將處理文本和圖片輸入。

5. **創建提示**：
   - 使用`apply_chat_template`方法將消息格式化為適合模型的提示。

6. **處理輸入**：
   - 將提示和圖片處理成模型可以理解的張量。

7. **設置生成參數**：
   - 定義模型生成過程的參數，包括生成的新標記的最大數量以及是否對輸出進行抽樣。

8. **生成代碼**：
   - 模型根據輸入和生成參數生成Python代碼。使用`TextStreamer`處理輸出，跳過提示和特殊標記。

9. **輸出**：
   - 打印生成的代碼，應包括按照提示規定處理圖片並保存的Python代碼。

這個示範說明了如何利用OpenVino的預訓練模型根據用戶輸入和圖片動態生成代碼。

**免責聲明**：
本文件已使用基於機器的人工智能翻譯服務進行翻譯。儘管我們努力確保準確性，但請注意，自動翻譯可能包含錯誤或不準確之處。應以原語言的原始文件為權威來源。對於關鍵信息，建議進行專業人工翻譯。我們不對因使用此翻譯而產生的任何誤解或誤讀承擔責任。