## Binary Tree
### 특징

### 직접 구현해본 Binary Tree
**트리 노드**
```java
public class TreeNode {
    int value;
    TreeNode leftChild;
    TreeNode rightChild;

    public TreeNode(){};

    public TreeNode(int value){
        this.value = value;
    }

    public int getValue() {
        return value;
    }

    public TreeNode getLeftChild() {
        return leftChild;
    }

    public void setLeftChild(TreeNode leftChild) {
        this.leftChild = leftChild;
    }

    public TreeNode getRightChild() {
        return rightChild;
    }

    public void setRightChild(TreeNode rightChild) {
        this.rightChild = rightChild;
    }

    public boolean hasLeft(){
        if(this.leftChild==null)
            return false;
        return true;
    }

    public boolean hasRight(){
        if(this.rightChild==null)
            return false;
        return true;
    }

    public boolean isLeap(){
        if(!(hasLeft() || hasRight()))
            return true;
        return false;
    }
}

```

**구현**
```java
public class MyTree {

    TreeNode root;

    public void add(int value){
        if(root == null){
            root = new TreeNode(value);
        }
        else{
            insertSearch(root,value);
        }

    }

    public Integer poll(int value){
        return pollSearch(null,root,value);
    }

    public boolean contains(int value){
        return search(root, value);
    }

    private void insertSearch(TreeNode parent, int value){
        if(parent.getValue() == value)
            return;
        if(value < parent.getValue()){
            if(parent.getLeftChild() == null){
                parent.setLeftChild(new TreeNode(value));
            }else{
                insertSearch(parent.getLeftChild(),value);
            }
        }else if(value > parent.getValue()){
            if(parent.getRightChild() == null){
                parent.setRightChild(new TreeNode(value));
            }else{
                insertSearch(parent.getRightChild(),value);
            }
        }
    }

    private boolean search(TreeNode parent, int value){
        if(parent.getValue() == value)
            return true;
        if(value < parent.getValue()){
            if(parent.getLeftChild() == null)
                return false;
            else
                return search(parent.getLeftChild(),value);
        }else if(value > parent.getValue()){
            if(parent.getRightChild() == null)
                return false;
            else
                return search(parent.getRightChild(),value);
        }
        return false;
    }

    private Integer pollSearch(TreeNode parent, TreeNode target, int value){
        if(target == null)
            return null;
        if(target == parent && target.getValue() == value){
            TreeNode last = target;
            TreeNode lastParent = parent;
            while(last.hasLeft()){
                lastParent = last;
                last = last.getLeftChild();
            }

            if(last.isLeap()){
                if(parent.getLeftChild() == target){
                    parent.setLeftChild(last);
                }else{
                    parent.setRightChild(last);
                }
                lastParent.setLeftChild(null);
            }else{
                if(parent.getLeftChild() == target){
                    parent.setLeftChild(last);
                }else{
                    parent.setRightChild(last);
                }
                lastParent.setLeftChild(last.getRightChild());
            }
        }

        if(target.getValue() == value){
            if(target.isLeap()){
                if(parent.getLeftChild() == target){
                    parent.setLeftChild(null);
                }else{
                    parent.setRightChild(null);
                }
            }

            if(target.hasRight() && !target.hasLeft()){
                if(parent.getLeftChild() == target)
                    parent.setLeftChild(target.getRightChild());
                else
                    parent.setRightChild(target.getRightChild());
            }

            TreeNode last = target;
            TreeNode lastParent = parent;
            while(last.hasLeft()){
                lastParent = last;
                last = last.getLeftChild();
            }

            if(last.isLeap()){
                if(parent.getLeftChild() == target){
                    parent.setLeftChild(last);
                }else{
                    parent.setRightChild(last);
                }
                lastParent.setLeftChild(null);
            }else{
                if(parent.getLeftChild() == target){
                    parent.setLeftChild(last);
                }else{
                    parent.setRightChild(last);
                }
                lastParent.setLeftChild(last.getRightChild());
            }
            return target.getValue();
        }else if(target.getValue() < value){
            pollSearch(target,target.getLeftChild(),value);
        }else{
            pollSearch(target,target.getRightChild(),value);
        }
        return null;
    }
}

```