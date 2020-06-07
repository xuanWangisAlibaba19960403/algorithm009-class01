**递归**

1. 节点的定义
2. 重复性（自相似性）

## 树的示例代码

```
def preorder(self, root):
    if root:
         self.traverse_path.append(root.val)
         self.preorder(root.left)
         self.preorder(root.right)

def inorder(self, root):
    if root:
        self.inorder(root.left)
        self.traverse_path.append(root.val)
        self.inorder(root.right)
            
def postorder(self, root):

    if root:
         self.postorder(root.left)
         self.postorder(root.right)
         self.traverse_path.append(root.val) 
```

# 递归

递归 - 循环

通过函数体来进行的循环

## 递归思想：有去有回

- 递：拆分成若干个相同解法的小问题

- 归：找到终止条件 返回相应的结果

  ## 代码模板

  ```
  public void recur(int level, int param) {
       // terminator递归终结条件
       if (level > MAX_LEVEL) {
           // process result
           return;
       }
       // process current logic 处理当层逻辑
       process(level, param);
       // drill down 下探到下一层
       recur( level: level + 1, newParam);
       // restore current status 清理当前层
  
  }
  ```

## 递归的三要素

- 明确递归终止条件(Terminator)
- 给出递归终止时的处理办法(Process)
- 提取逻辑，通过递归语句来找到子问题(Drill Down)