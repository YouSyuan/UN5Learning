# 從零開始學習 Unreal Engin 5


BluePrint：
1. 使用 Event Tick 顯示現在時間。
2. 添加 ThirdPersonMap 標題的聚光燈，並關閉場景光線。
3. 製作感應火炬：靠近會生火，離開後一段時間熄滅：
    - 使用 Begin Overlap 來生火(點光源+粒子)，End Overlap 來熄滅
4. 製作感應燈：靠近發亮，離開後關閉。
    - 使用 Begin Overlap 來開燈，End Overlap 來關閉
5. 設定角色 HP：
    - 使用腳本來顯是當前 HP。
6. 製作場景藥水道具：
    使用 Begin Overlap 與 Destroy Actor，使角色碰處後道具消失。
7. 當角色碰到場景中道具時的血量變化：
    - 使用 Begin Overlap 來處理是角色的膠囊體是否碰觸到藥水。
    - 使用 Cast To 來判斷碰觸到的是補血藥水或毒藥水，已進行後續血量變化的處理，並會播放音效。    
8. 製作記分板：
    - 當角色碰到場地上的方塊時，會加減顯示的分數。
    - 設置客製事件，分別處理加分與扣分。
    - 將角色與計分板連接。
    - 使用 Cast To 來判斷碰觸到方塊，已進行後續處理，並會播放音效。  
9. 製作接觸會產生爆炸特效的 Box。
10. 第一人稱射擊，擊中 Box 會計算新分數。
11. 將 ScoreBoard 的 Score 變數移動到 GameMode：
    - 遇到的問題：在 GameMode 預設的 Score 不會顯示在計分板上
12. 設置不同方塊：
    - 每次擊中時會累計受到傷害。
    - 用 Branch 判斷，當累計傷害 >= 分數時，方塊會消失並累計分數。
    - 在受到傷害與爆炸時，設置不同大小的爆炸效果。
    - 遇到的問題：用角色觸碰到也會計算傷害量。
    - 解決辦法：添加 Cast To 確保只會在受到子彈碰撞時才會累計受到傷害。
13. for loop / while loop 產生多個物件：
    - 製作要產生的物件，並加入 ShowNumber 事件，在上面顯示編號。
    - 創建一個 Random_Location 函數，產生隨機向量，提供物件生成的位置。
    - 在地圖藍圖用鍵盤指定按鍵，分別用 for loop (鍵盤2)和 while loop (鍵盤3)搭配 SpawnActor 在角色周圍隨機位置生成多個物件。
14. 確保生成期望數量的物件：
    - 調整 collision handling override 指令，確保產生的物件不會重疊。
    - 使用 while loop 搭配 is Vaild 檢查 SpawnActor 是否有生成物件。
    - 如果沒有生成的話，會藉由客製化事件跳到迴圈最前面重新執行。
    - 如果有生成，就會將計數變數 +1 來判斷目前生成的編號。
- [學習範例](https://www.youtube.com/watch?v=xPEGSgXaTzQ&list=PLWaDU4I4My4RBwegzH8LnhAo5YN4krysV&index=2&ab_channel=%E8%94%A1%E6%98%8E%E6%AC%A3)


場景設計基礎：
1. 幾何物件 Geometry：
    - 建立桌子、椅子
2. 從 Quixel Bridge 下載資源。
- [學習範例](https://www.youtube.com/watch?v=3XWNR9IJnPo&list=PLWaDU4I4My4RRuRocZ2-AQDum5xt2Con1&index=1&pp=iAQB&ab_channel=%E8%94%A1%E6%98%8E%E6%AC%A3)


使用 Unreal Learning Kit：
1. 從市集導入 unreal Learning Kit 資源內容。
2. 修改遊戲模式。
3. 調整攝影機觀看視角。
4. 調整角色移動屬性：
    - 行走。
    - 跳要。
    - 重力。
5. 模擬手電筒效果，按 F 開關。
6. 導入模型：
    - 調整大小。
    - 增加碰撞。
7. 初設地形：
    - 創建平地。
    - 雕刻地形。
    - 添加海洋。
    - 添加花草。
8. 調整環境：
    - 添加霧氣。
    - 調整光源(陽光)。
    - 調整 skylight。
    - 調整後期處理體積。
9. 加入粒子。
10. 加入聲音：
    - P.S. 音檔格式 wav, aif， 16位
    - 導入 BGM。
    - 加入火的音效，並隨距離衰減。
11. 建立材質：
    - 設定基礎顏色。
    - 設定雙面，避免從內往外看是透明的。
    - 設定 Metallic, 高光度, 粗糙度, 自發光。
    - 添加木頭紋理與增加表面凹凸(法線 Normal)。
    - 導入紋理，並創建材質。
    - 將創建的材質轉貼花。
    - 調整物件是否接受貼花。
    - 在貼花上添加法向量，增加表面層次(用Photoshop 製作再導入)。
        - 問題：我沒有 Photoshop，用 unreal 的 NormalFromHeightmap 搭配一個載有一樣貼花的 Param Tex Object 可以達到類似的效果。
    - 製作過場動畫：
        - 錄製兩段畫面並銜接。
        - 讓場景中的物件隨著鏡頭畫面的推進產生縮放。
        - 讓太陽(場景光源)產生升起的樣式。
        - 加入移動中的角色。
        - 加入不同動畫間的漸變軌道。
        - 加入 BGM。
        - 導出影片。
    - 角色設定：
        - 綁定骨架(研究中...)
        - 動作設定(研究中...)
        - 按下指定鍵顯示滑鼠鼠標。(目前遇到的問題：在顯示滑鼠時移動滑鼠，視角也會跟著轉動)
        - 加入超級跳按法
- [學習範例](https://www.youtube.com/watch?v=lR6O08vikoE&list=PLXuT93fbHR3gDNl18mdPgqtXIV5rpnGD9&index=2)
    