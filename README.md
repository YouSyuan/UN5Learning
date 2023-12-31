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
12. 製作過場動畫：
    - 錄製兩段畫面並銜接。
    - 讓場景中的物件隨著鏡頭畫面的推進產生縮放。
    - 讓太陽(場景光源)產生升起的樣式。
    - 加入移動中的角色。
    - 加入不同動畫間的漸變軌道。
    - 加入 BGM。
    - 導出影片。
13. 角色設定：
    - 綁定骨架
    - 綁定基本動作：
        - 已綁定：待機、走路、跑步。
    - 按下指定鍵顯示滑鼠鼠標。
        - 目前遇到的問題：在顯示滑鼠時移動滑鼠，視角也會跟著轉動。
            - 已暫時解決：再預設的 Enhanced Input Action IA_Look 加入判斷滑鼠是否顯示。
        - 新問題：當滑鼠消失後，還要再點一下才有辦法旋轉鏡頭。
    - 加入超級跳：
        - 使用 ctrl + space 觸發。
    - 設定超級跳的冷卻時間：
        - 加一個 delay 來重製觸發。
    - 添加超級跳的起跳特效與音效。
    - 創建道具石，可提升跳躍次數為 2 次：
        - 使用 Get Player Character 取得角色資訊。
        - 再使用 set JumpMaxCount 設定最大跳躍次數。
    - 讓道具石產生上下漂浮的效果：
        - 使用 Timeline 來創建動畫的時間軸。
        - 使用 Lerp(Vector) 依據 Timeline 中設定的時間軸變化，輸出不同的向量值。
        - 使用 Set Relative Transform 接收 Lerp 的值來改變道具石的相對位置。
14. 角色技能：
    - 添加技能 01 - 召喚螢火蟲：
        - 設定一個要召喚的發光粒子。
        - 在動畫藍圖添加判斷釋放技能和回到原本的動作(在移動時會變成平移狀態XD)。
        - 在 Event BeginPlay 建立，從骨骼網格體取得動畫實例，再轉換成角色的動畫藍圖，並轉換成變量來保存(保存在動畫藍圖中的變量)。
        - 將上面保存的變量：
            - 設置為 True (動畫藍圖中的變量)，加上 Spawn System Attached 來指定釋放技能的位置(加入一個延遲確保動畫和釋放特效可以一致)。
            - 設置為 False 停止釋放技能的動作。
        - 如果在移動中釋放技能，將移動速度調整為 0，解決邊釋放邊平移的情況。
    - 添加技能 02 - 在身邊釋放衝擊力:
        - 在動畫藍圖添加判斷釋放技能和回到原本的動作。
        - 從角色動畫藍圖所保存的變數來設置技能是否的 True, False。
        - 在角色建立一個徑向力組件來模擬技能所釋放出來的衝擊力，並使用 Set Active 來做開關。
        - 使用 Spawn Emitter at Location 來指定技能在角色身上釋放的位置：
            - 使用 Get Actor Location 來取的角色的向量位置。
            - 將向量分割後，將 Z 軸的數值降低。
        - 建立一個客製化事件，用來判斷技能的 CD 時間是否已經結束。
        - 添加攝影機震動：
            - 使用 LegacyCameraShake 創建產生震動的藍圖。
            - 連接玩家的攝影機(Player Camera Manager)。
15. 掉落深淵：
    - 當角色掉落到一定位置時，會從天上掉下來。
    - 建立一個目標點，用來當重置角色位置時，會出現的地點。    
    - 建立一個 BP 碰撞體，用來判斷角色應該重置位置：
        - 建立一個目標點的位置的變數，並開啟公有，用來保存目標點。
        - 建立 Begin Overlap 事件，並將 Other Actor 連接到判斷接觸的是否為玩家角色。
        - 取得目標點位置後，傳給玩家角色，設定現在向量。
16. 建立旋轉風扇：
    - 在藍圖中使用一個場景組件將風扇的靜態網格體組合在一起。
    - 新增一個時間軸，用來控制風扇旋轉：
        - 新增一個向量型軌道。
        - 調整 Z 軸在不同時間點的角度位置(0 秒在 360 度，3 秒在 0 度)。
        - 取得風扇組鍵 rotation 的值，再將時間軸 Rotation Z 接到 Z 軸。
17. 建立順移門：
    - 使用碰撞體積連接目標點，達到瞬間移動的效果。
    - 沒有設定使用目標的限制，每個可以移動的個體都可以瞬間移動。
18. 建立互動開關：
    - 建立一個開關藍圖。
    - 建立時間軸，用來呈現把手的動畫過程的時間變化(關閉 自動播放、循環)。
    - 使用 set relative rotation 接收來置時間軸(透過Lerp(Rotator))來控制開關的旋轉。
    - 在角色藍圖添加 set Enable Click Events 來啟用滑鼠點擊。
    - 物件添加 On Clicked 事件，搭配 Flip Flop 來判斷點擊時，動畫是要從開始到結束，還是從結束到開始。
    - 增加一個控制範圍限制，在範圍內才可以進行開關：
        - 使用 Gate 來判斷角色是否在指定範圍內。
        - 是就使用 Open，否則使用 Close。
    - 增加一道控制的門：
        - 使用時間軸控制門開關的位置變化。
        - 設置兩個客製化 Event：OpenGate, CloseGate。
        - 在開關的藍圖添加一個門的變量，並且設置為公開。
        - 將兩個客製化 Event 分別接在 FlipFlop 的 A 和 B，讓在用滑鼠操作開關時可以一起執行動畫。
19. 建立點擊開啟的火把：
    - 建立一個 bool 變數來判斷當前是否點燃。
    - 未點燃：點燃火焰(開啟光源、火焰特效、音效)，並將 bool 變數設置為 True。
    - 使用時間軸來控制光源從暗到亮的變化。
20. 使用繼承建立開關的子藍圖(子類)：
    - 在父類別中定義好把手的動畫。
    - 建立兩個虛函式( Open, Close )的客製類別給子藍圖 overloading。
    - 建立開關的子藍圖：
        - 子藍圖 1：開關門
            - 重載父類的 Open, Close 分別用來給指定門開與關。
        - 子藍圖 2：開關火把。
            - 重載父類的 Open, Close 分別用來給指定門開與關。
            - 將指定的多個火把加上一樣的標籤。
            - 使用 Get All Actors Of Class with Tag 來取得所有同類別與同標籤的數組。
            - 並且使用 For Each Loop 來讀取數組中全部的火把，並一次操作開關。
21. 添加事件分發器：
    - 在父類添加式建分發器，用來執行只會出現一次的功能。
22. 按路徑移動：
    - 創建一個藍圖，將要移動的物件放入，並加上樣條組件(用來規畫路徑)。
    - 將藍圖放入地圖中，並用樣條規劃好路徑。
    - 創建一個時間軸，用來輸出百分比。
    - 用時間軸輸出的百分比乘上樣條的長度，得到移動距離。
    - 將這個距離與樣條物件傳到 Get Location at Distance Along Spline 來計算位置。
    - 將計算出來的位置傳給要移動的物件來重製當前的相對位置。
23. 關卡切換：
    - 方法 1：使用關卡門
        - 在碰撞體積建立一個 Begin Overlap 事件。
        - 使用 Cast to 角色，限制只有玩家角色可以通過。
        - 使用 Open Level 加入切換後的關卡名稱即可。
        - 如果角色外觀與本身素質沒有切換過去，要更改遊戲模式。
    - 方法 2：關卡流送
        - 當角色走到一定位置後，就可以看到更多的地圖資訊。
        - 窗口 -> 關卡 -> 新建關卡。
        - 點擊新建的關卡兩下後，即可在地圖上直接加入需要的物件(保存後進入新建好的關卡看不到東西是正常的，因為沒開燈)。
        - 添加項目 -> 體積 -> 關卡流送體積。 
        - 將要看到上面關卡的範圍全部包含進這個體積裡面(新建關卡的物件也要全部放進去)。
        - 點擊新建的關卡，在點擊關卡細節訊息，將設定好範圍的流送體積添加進去，並將靜態打勾。
24. 構造腳本：
    - 可以動態的調整要放到地圖中的物件，如果要放入多個，可以直接在地圖中調整，不用在手動一個一個加入。
    - 一排柵欄：
        - 使用 Add Static Mesh Component 將製作好的靜態網格加入。
        - 使用 Set Static Mesh 設置靜態網格的位置向量。
        - 創建 Count 變數來統計需要的數量，並設為公開。
        - 使用 For Loop 搭配運算來將多個柵欄一次排開。
        - 創建靜態網格的數組，用來儲存做好的不同柵欄靜態網格。
        - 搭配 Random Int 來隨機取得數組中的任一個柵欄來設置。
    - 石牆：
        - 使用 Add Static Mesh Component 將製作好的靜態網格加入。
        - 使用 Set Static Mesh 設置靜態網格的位置向量。
        - 創建 Count 變數來統計需要的數量，並設為公開。
        - 創建一個 Spline 樣條組件，用來規劃石頭生成的路徑。
        - 使用 Get Spline Length 取得樣條長度。
        - 使用 Get Location at Distance Along Spline 取得樣條距離初始位置的距離位置。
        - 使用 For Loop 搭配運算來將多個石頭沿著 Spline 的路徑與長度排開。
        - 在使用兩個隨機浮點數來讓石頭的旋轉與大小產生變化。
        - 創建靜態網格的數組，用來儲存做好的不同柵欄靜態網格。
        - 搭配 Random Int 來隨機取得數組中的任一個石頭來設置。
- [學習範例](https://www.youtube.com/watch?v=lR6O08vikoE&list=PLXuT93fbHR3gDNl18mdPgqtXIV5rpnGD9&index=2)
    