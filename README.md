# java-SimpleGame
### 遊戲說明:
以類似大富翁的形式,配合闖關遊戲,讓玩家可以體驗到以智力取勝的樂趣,也能透過運氣闖關成功。
用逃脫的故事為主軸,搭配中間穿插的小遊戲,能展示出平日的學習成果,並融會貫通。
### 遊戲關卡:
1. 猜拳(Mora)
2. 貓圍棋(Cat)
3. 四子棋(Connect4)
4. 井字遊戲(Ox)
5. 比大小(Highlow)
### 程式說明
在程式的構成上,我們分成了一個主類別與五個一般類別,在主類別程式
碼中,我們主要是建立整個大逃脫的架構,而大逃脫中所需的小遊戲則是使用
一般類別來建立。
#### 主類別
在主類別中,我們使用了 4*7 的二維陣列(game[][])來建立大逃脫遊戲的
棋盤。首先在初始棋盤的方法(createMap)中,使用了 for 迴圈對二維陣列進行
初始化,由於我們的棋盤中有分為可以走的白格與無法通行的黑格,所以在
for 迴圈中加上了 if-else 來進行黑白格的判斷。因為在一開始的棋盤中起點
與終點都並非白格或黑格,所以在 for 迴圈結束後,我們直接指定終點[3][6]
為終點符號(✪),在起點方面則因為只有一開始玩家才會站在起點,故使用了
if-else 設定只有當玩家累積骰子點數(disum)為 0 時,才將起點設置為玩家符號(☺)。在畫出棋盤的方法(drawMap)中也是同樣使用了 for 迴圈將二維陣列印出。

列出初始棋盤後,玩家就可以開始擲骰啦!我們是設定讓玩家輸入 1 來擲
骰,為了避免玩家輸入錯誤導致程式無法運行,所以使用了 while 迴圈(a=0)包
住整個擲骰過程,並使用 if-else 判斷是否跳出擲骰迴圈,若玩家輸入為 1,
則隨機 1~6 中一個數字,並將該數字(dice)累計在 disum 中,最後指定 a=1 來
跳出擲骰迴圈。
有了點數之後就需先將原棋盤初始化,避免出現棋盤上有多個玩家符號,
再來需判斷玩家骰到的位置與鬼目前所在位置,在判斷玩家位置的方法(move)
中,我們使用了較暴力的方法,使用 if-else 一個一個點數判斷,此外我們將
遊戲設定為如果骰超過終點就必須走回頭路,所以我們用 while 迴圈將判斷式
包起來以便重新判斷。而在判斷鬼所在格子的方法(gsmove)中,也使用了同樣
的判斷式來進行判斷,由於鬼抓到玩家時,也就是鬼的點數總和(gssum)等於
disum 或大於 disum 時,玩家失敗,且結束此次遊戲,所以多加了這兩個條件
判斷。

判斷完玩家與鬼的位置後,就可以呼叫 drawMap 印出目前棋盤了!接下來就
要開始判斷玩家踩到的格子會觸發什麼遊戲或陷阱,所以建立一個進入該位置
遊戲的方法(movegm),同樣使用 if-else 判斷式,因為這邊需要用到一般類別
中的小遊戲,所以需要先建立該類別物件,並在需要用到該小遊戲的條件式中
呼叫執行。在完成關卡任務後玩家的位置可能會有所變動,且小遊戲輸了或踩
到陷阱,則會召喚出鬼,所以除了特定幾格外,完成任務後皆需重新判斷玩家
與鬼的位置,並將新的棋盤畫出,此外因為在新位置中可能會有新的任務,所
以需將判斷進入小遊戲的程式碼用 while 迴圈(b=0)包起來,若不需重新進入遊
戲則使 b=1 並離開迴圈。

最後使用 if-else 判斷玩家是否抵達終點或被鬼抓到,若遊戲結束,則同
樣使用判斷式詢問玩家是否開始新一輪的遊戲。若遊戲尚未結束,為了使玩家
能繼續擲骰,則令 a=0(玩家可擲骰),並使用 while 迴圈將玩家擲骰至判斷是
否進行下一輪遊戲的部分包起來。
#### 一般類別
而一般類別中的程式碼大多為本學期中老師所教的小遊戲,所以這邊主要
介紹一下我們是如何將其輸贏結果與主程式連結,首先我們在主程式中建立一
個方法(smallgm)並宣告 int c,接下來就回到一般類別中,先建立主程式物件
mc,並在遊戲決定輸贏時呼叫 smallgm,且指定 c 為 0 或 1,因為在 smallgm 中
已經使用 if-else 設定如果 c=0 則 win=false,若 c=1 則 win=true。當一般類
別物件呼叫結束後,只要在主程式呼叫 smgm 方法來進行小遊戲輸了的懲罰就成
功了。
