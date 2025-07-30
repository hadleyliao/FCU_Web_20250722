# ToDoItem.vue 的 prompt


### 新增一個 ToDoItem.vue
- template
有 DIV 包括 checkbox input 跟 文字 Label， input id 跟 checked 與 Data 做單向綁定
Label for 跟 ID 做單向綁定， label 用於顯示 label 參數

### 新增了「編輯」和「刪除」按鈕
- 當點擊「編輯」按鈕時，會切換顯示 ToDoItemEditForm 元件。
- 當點擊「刪除」按鈕時。發出一個 清單刪除 事件，以便更新列表。


### 使用 ToDoItemEditForm form
- 如果 isEditing 為真，就顯示 ToDoItemEditForm


### script 
- 會有三個輸入的 props 參數， Label ， Label 必填的， done 是 boolean ，id 文字必填
  Data 包括 isDone 跟 props 的 done 一樣
- 當 checkbox 有改變，會送出 checkbox變更 的事件，還有元件的 id 字串
- ToDoItemEditForm 元件 會聽事件 清單編輯 事件，送出 清單編輯 事件，同時傳遞新的代辦事項名稱，不顯示 ToDoItemEditForm
- ToDoItemEditForm 元件 會聽事件 取消編輯 事件，不顯示 ToDoItemEditForm 