# ToDoItem.vue 的 prompt


### 新增一個 ToDoItem.vue
- template
有 DIV 包括 checkbox input 跟 文字 Label， input id 跟 checked 與 Data 做單向綁定
Label for 跟 ID 做單向綁定， label 用於顯示 label 參數

### 新增了「編輯」和「刪除」按鈕
- 當點擊「編輯」按鈕時，會切換顯示 ToDoItemEditForm 元件，讓我們可以用它來編輯待辦事項。此處理函式會將 isEditing 標記設為 true。
- 當點擊「刪除」按鈕時，會透過事件處理函式刪除該待辦事項。在此處理函式中，發出一個 文件刪除 事件，以便更新列表。


### 使用 ToDoItemEditForm form
- 如果 isEditing 為真，就顯示 ToDoItemEditForm


### script 
- 會有三個輸入的 props 參數， Label ， Label 必填的， done 是 boolean ，id 文字必填
- Data 包括 isDone 跟 props 的 done 一樣
- 當 checkbox 有改變，會送出 資料改變 的事件，還有元件的 id 字串


### 在現有的 isDone 資料點下方新增 isEditing
- methods 中新增一個 完成編輯清單 方法。送出 清單完成編輯 事件，並將 isEditing 設為 false 。 
- 新增 編輯取消的方法