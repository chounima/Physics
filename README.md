# Physics：從牛頓到量子重力

用模擬、符號推導和真實數據，一步步理解「量子力學 vs 廣義相對論」的衝突。
從高中物理程度出發，不需要微積分；每個單元前都有一本「觀看前須知」。

## 主線：cGh 立方體

牛頓力學隱含設定 $c = \infty$、$\hbar = 0$。每個單元打開一個常數，看世界怎麼變：

```
牛頓力學       ：都不打開                 → 01
量子力學       ：打開 ħ                   → 02
狹義相對論     ：打開 1/c                 → 03
廣義相對論     ：打開 G + 1/c             → 04
量子重力（空缺）：G + 1/c + ħ 全開          → 05
```

關鍵觀念：量子力學保留了牛頓的**絕對時間**，廣義相對論保留了牛頓的**確定性**，
兩者各自留著對方已經拆掉的零件，所以會衝突。

## 閱讀順序

| # | 檔案 | 內容 | 亮點 |
|---|---|---|---|
| 1 | `00_basics/01_before_newton` | 須知：向量、變化率、一小步模擬、能量、橢圓、進動、角秒 | 只用一行程式讓地球繞出軌道 |
| 2 | `01_newton/01_orbits` | 牛頓的太陽系 | 8 顆行星週期與觀測差 < 0.07%；水星缺 **42.5″** |
| 3 | `00_basics/02_before_quantum` | 須知：波、複數、機率、波包 | 用 200 個波疊出不確定性原理 |
| 4 | `02_quantum/01_wavepacket` | 波包散開、不確定性、ħ → 0 | Δx·Δp = ħ/2 精確到 1e-16 |
| 5 | `02_quantum/02_tunneling` | 穿隧效應 | 晶片漏電、Flash 記憶體、太陽核融合 |
| 6 | `02_quantum/03_double_slit` | 二維雙狹縫、測量問題 | **在家實驗**：雷射量頭髮、LED 量普朗克常數 |
| 7 | `00_basics/03_before_relativity` | 須知：參考系、光速不變、時空圖 | |
| 8 | `03_special_relativity/01_special_relativity` | 時間變慢、同時的相對性、雙生子、E = mc² | **真實數據**：1963 緲子實驗（預測 404，實測 408） |
| 9 | `00_basics/04_before_general_relativity` | 須知：等效原理、彎曲空間、度規、濾波 | 台北→紐約大圓航線 |
| 10 | `04_general_relativity/01_schwarzschild` | 史瓦西時空 | sympy **證明** R_μν = 0；GPS 與衛星出廠頻率差 0.14%；水星 **42.98″** 補上缺口 |
| 11 | `04_general_relativity/02_gravitational_waves` | 重力波 | **LIGO 原始數據** GW150914：時間差 7.3 ms、啁啾、變成聲音 |
| 12 | `00_basics/05_before_quantum_gravity` | 須知：因次分析、熵、黑體輻射、零點能量 | |
| 13 | `05_quantum_gravity/01_where_theories_collide` | 衝突地帶 | 普朗克尺度、霍金輻射、Page 曲線、真空能量差 10¹²¹ 倍、半古典重力 |

## 三種方法

| 方法 | 做什麼 | 工具 |
|---|---|---|
| 模擬 | 把理論跑出來，看它預測什麼 | numpy / scipy / matplotlib |
| 推導驗算 | 讓電腦做符號運算，驗證課本公式 | sympy |
| 對照現實 | 拿真實觀測數據比對理論數字 | 公開數據（LIGO、GPS、緲子）、在家實驗 |

## 環境

```powershell
(Set-ExecutionPolicy -Scope Process -ExecutionPolicy RemoteSigned) ; (& D:\Python\Physics\physics_env\Scripts\Activate.ps1)
```

在 VS Code 開 Notebook 時，kernel 選 **Python (physics_env)**（已註冊成 Jupyter kernel）。
所有 Notebook 都已執行過、結果存在檔案裡，打開就能看；要自己改參數再按 Shift+Enter 重跑。

執行時間較長的格子：`01_orbits` 實驗 4（3–6 分鐘）、`03_double_slit` 實驗 1–2（約 1–2 分鐘）。

重建環境：

```powershell
py -3.10 -m venv physics_env
.\physics_env\Scripts\Activate.ps1
pip install -r requirements.txt
python -m ipykernel install --user --name physics_env --display-name "Python (physics_env)"
```

> 刻意與 `d:\ImageRecognition\yolo_env` 分開，避免安裝套件時動到 YOLO 環境的 numpy。

## data/

`04_general_relativity/02_gravitational_waves` 第一次執行時會從 gwosc.org 下載 LIGO 數據（約 2 MB）到這裡，
並輸出 `GW150914_H1.wav`（重力波的聲音）。這個資料夾在 `.gitignore` 裡。
