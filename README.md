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
- [學習範例](https://www.youtube.com/watch?v=xPEGSgXaTzQ&list=PLWaDU4I4My4RBwegzH8LnhAo5YN4krysV&index=2&ab_channel=%E8%94%A1%E6%98%8E%E6%AC%A3)