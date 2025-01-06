
## 登入帳號管理  
* 未來會介接到高榮自己的權限管理機制，以及其他合作機構 
* 機構能 CRUD  
* 帳號能 CRUD  
* table 欄位  
    1. 機構名稱  
    2. account name  
    3. uid (unique)  
    4. role (admin, general)  
* role 的權限  
    * 唯一能編輯 ICD-10 table 的人  
    * 能看到所有人的文章  
* 機構刪除時底下 user 是否要跟著刪除？  

## 文章保存與恢復  
* 讓使用者儲存/載入已存之檔案  
* 每一筆能 CRUD  
* table 欄位  
    1. uid (unique)  
    2. doc_id  
    3. content  
    4. created_date  
    5. saved_date  
    6. is_draft  
    7. status (submit/draft)  
        + 文章預設 draft，submit 後才不再是 draft  
        + 但文章仍能修改  

## ICD-10 Code table  
* offline 讓 ICD-10 Code extractor 自動爬梳解析病碼  
* 病碼能 CRUD  
* table 欄位  
    1. icd_id (unique)  
    2. ICD-9-CM代碼   
    3. ICD-9-CM英文名稱  
    4. ICD-9-CM中文名稱  
    5. ICD-10-CM  
    6. ICD-10-CM英文名稱  
    7. ICD-10-CM中文名稱  
    8. 對應情形  
    9. freeze: True/False  
        + 已 freeze 的禁止刪除  
* 新增病碼直接由 admin 操作，不用自動從 paper 抓出病毒碼  
* 查詢病碼是否已存在  
    + 已存在: 不動作  
    + 不存在: 新增，且 verified 設為 `False`  
* verified == `False` 的 row 需要等醫師驗證並填入缺值，劃押後才能併入 verified 部分  
* 若 verified == `False` 的病碼被 parse 到多次，並且有些欄位值相異，衝突如何管理？  

## paper offline 處理  
* 從 chunk 內找出病名 + 病碼  
* chunk 要對應到 page  
* paper 要對應到所有的 ICD-10 病碼  
* table 欄位  
    1. paper id  
    2. paper file path  
    3. paper icd_ids  
        + icd9  
        + icd10  
    5. chunks   
        + page number  
        + text  
        + ICD-10 code  
        
## 後臺檢視  
## 輸出 word 檔  
一般 user 不能碰譯碼簿跟 500 篇  

只有 admin 可以新增譯碼簿 prority 較低  
 
* 某個病碼 能夠跟 某些 paper 產生關聯  
* 輸入疾病名稱 -> 找到 ICD 10 code -> 找到有ICD 10 code相關的 papers  
* 輸錯字能否模糊比對（鬆一點） 

一份 word 檔  

