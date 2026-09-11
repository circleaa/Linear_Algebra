# License Plate Perspective Transformation (車牌透視變換系統)

![C++](https://img.shields.io/badge/C++-00599C?style=flat-square&logo=c%2B%2B&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-5C3EE8?style=flat-square&logo=opencv&logoColor=white)
![Ubuntu](https://img.shields.io/badge/Ubuntu-22.04-E95420?style=flat-square&logo=ubuntu&logoColor=white)

## Introduction
本專案為線性代數與電腦視覺之實作應用。透過計算 **3x3 透視變換矩陣 (Perspective Transformation Matrix)**，將任意四邊形的車牌影像，精準映射並幾何校正至車輛圖片的指定視角中。

此技術可廣泛應用於圖像校正、擴增實境 (AR) 與影像拼接等領域。
[完整題目](./HW2.pdf)
[完整程式碼](./hw2-Perspective Transformation.cpp)

## Demo
| 輸入：車輛原圖 | 輸入：車牌原圖 | 輸出：透視變換合成結果 |
| :---: | :---: | :---: |
| <img src="car_images/Q4_car.png" width="250"> | <img src="car_images/Q4_plate.png" width="250"> | <img src="car_images/result4.png" width="250"> |

## Mathematical Theory
專案核心在於模擬相機的視角變化（距離、位置與角度）。透過影像座標系至像素座標系的離散抽樣處理，我們定義了針對 X、Y、Z 三維空間軸的旋轉矩陣。

例如，當物體繞 Z 軸旋轉 $\theta$ 角度時，其座標變換可由以下旋轉矩陣 $R_z$ 表示：

$$ \begin{bmatrix} x \\ y \\ z \end{bmatrix} = \begin{bmatrix} \cos\theta & -\sin\theta & 0 \\ \sin\theta & \cos\theta & 0 \\ 0 & 0 & 1 \end{bmatrix} \begin{bmatrix} x' \\ y' \\ z' \end{bmatrix} $$

同理，系統內部亦實作了針對 X 軸 ($R_x$) 與 Y 軸 ($R_y$) 的旋轉矩陣，以確保車牌在三維空間投影轉換時的精準度。

## Environment
*   **OS:** Ubuntu 22.04
*   **Compiler:** g++ 11.4.0
*   **Library:** OpenCV 4.5.3 (本專案僅使用 OpenCV 進行基礎讀寫，核心數學運算由 C++ 手工實作)

## Usage
編譯完成後，請透過命令列引數傳入三組參數：車輛圖片檔名、車牌圖片檔名，以及預期的輸出檔名。

```bash
# 執行範例
./main car.png plate.png output.png
