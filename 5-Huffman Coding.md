### An Application of Binary Trees and Priority Queues  

scan文章或句子，紀錄每個element出現的頻率  
排出priority queue  

如果queue有兩個以上(包含兩個)的元素，進行以下步驟:
1. 產生新的 node1  
2. delete 最小的 node2 成為 node1 的左子樹  
3. delete 次小的 node3 成為 node1 的右子樹  
4. 將 node1 的值等於 node2 + node3  
5. 再依 node1 的大小 insert queue  
6. 重複以上，直到元素少於兩個  

---

是否有可能overhead ?  
有可能 
除了密文本身還要儲存 Huffman tree
