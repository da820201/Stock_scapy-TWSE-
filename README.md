# Stock_scrapy 
### 程式目的:爬取證交所每五秒委託簿交易
### 程式流程: 
![image](https://i.imgur.com/yfgHt8Q.jpg)
### 程式解釋:
        1.由於爬取證交所資料時會被阻擋IP，因此程式會先使用多進程去爬取多個IP，並放進程式的IP Pool
        
        2.傳統的Requests或是selenium套件都會產生程式必須等待請求回應完成，才會執行後面程式碼的狀況；
          因此程是在發送請求的部分是採用多進程+多線程來進行，同時每個發送的請求都盡力避免用同樣的IP；
          
        3.證交所在交易的伺服器在面對大量請求時，會出現拒絕回應的情況，但為求訓練資料的完整，程是在這
          部分會將原先被儲存於IP Pool的備用IP提取，並包裝成新的請求，快速並密集的向證交所發送請求；
          
        4.將每五秒所取得的資料，推送到SQL內
        
        5.當離開設定的時間，將負責發送請求的進程及相關佇列物件進行回收，並等待下次設定的程式設定的開始時間
