# 📝 基本的 RAG 實現

這是一個非常簡單的專案，旨在演示檢索增強生成（RAG）的基本概念。

程式碼包含在 `main.ipynb` Jupyter Notebook 中，它使用一個本地文件（`doc.md`）作為知識庫，並圍繞它實現了一個問答流程。

## ⚙️ 運作方式

這個專案遵循一個經典的 RAG 流程：

1.  **文本分塊 (Chunking)**：將 `doc.md` 文件分割成較小的文本片段。
2.  **向量嵌入 (Embedding)**：使用 `sentence-transformers` 模型將每個文本片段轉換為向量。
3.  **索引 (Indexing)**：將這些向量儲存在 `ChromaDB`（一個內存向量數據庫）中。
4.  **檢索 (Retrieval)**：當使用者提出問題時，程式會將問題轉換為向量，並在 `ChromaDB` 中搜索最相關的文本片段。
5.  **重排 (Reranking)**：使用 `CrossEncoder` 模型對檢索到的片段進行重新排序，以提高其相關性。
6.  **生成 (Generation)**：將原始問題和經過重排的文本片段發送到 Google Gemini API（本專案使用 `gemini-2.5-flash` 模型），以生成最終的回答。

## 🛠️ 環境設定

本專案建議使用 `uv` 來管理 Python 虛擬環境和依賴套件，以確保環境的一致性。

1.  **安裝 uv**

    如果您尚未安裝 `uv`，可以透過 pip 或官方推薦的方式安裝：
    ```bash
    # 使用 pip
    pip install uv
    ```

2.  **建立並啟用虛擬環境**

    在專案的根目錄下，執行以下指令來建立虛擬環境（uv 會將其建立在 `.venv` 資料夾中）：
    ```bash
    uv venv
    ```
    接著，啟用虛擬環境。在 Windows (PowerShell) 中：
    ```bash
    .venv\Scripts\activate
    ```
    在 macOS 或 Linux 中：
    ```bash
    source .venv/bin/activate
    ```

3.  **安裝依賴套件**

    啟用虛擬環境後，使用 `uv pip sync` 來安裝 `uv.lock` 文件中鎖定的所有依賴套件。這能確保您安裝的版本與專案開發時完全一致。同時，我們也需要 `jupyter` 來運行筆記本。
    ```bash
    uv pip sync
    
    ```

4.  **設定 API 金鑰**

    這個專案需要使用 Google Gemini API。請在專案根目錄下建立一個 `.env` 文件，並在其中加入您的 API 金鑰：
    ```
    GOOGLE_API_KEY="YOUR_API_KEY_HERE"
    ```

## 🚀 如何運行

完成環境設定後，建議使用 `uv run` 指令來啟動 Jupyter Notebook。這個指令會自動在 `uv` 管理的虛擬環境中執行，無需手動啟用 (`activate`) 環境。

1.  **啟動 Jupyter Notebook**

    在專案的根目錄下，執行以下指令：
    ```bash
    uv run jupyter lab
    ```

2.  **開啟筆記本**

    上述指令會自動在您的預設瀏覽器中開啟 Jupyter 介面。如果沒有，您可以手動複製終端機中顯示的網址（通常包含一個 token）。

    接著，點擊並打開 `main.ipynb` 文件。

3.  **運行儲存格**

    您可以從頭到尾依次運行每個儲存格，以觀察整個 RAG 流程的運作。

---

這只是一個基礎的學習和演示專案，還有很多可以改進的地方。