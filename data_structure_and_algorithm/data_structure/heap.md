## Heap

### 특징

### 직접 구현해본 Heap
```java

public class MyHeap {
    List<Integer> container = new ArrayList<>();
    public MyHeap(){ }

    public void add(Integer value){
        if(container.size() <=0)
            container.add(null);
        container.add(value);
        moveUp(container.size()-1);
         
    }

    public Integer poll(){
        Integer retVal = container.get(1);
        Integer last = container.get(container.size()-1);
        container.add(1,last);
        container.remove(container.get(container.size()-1));
        moveDown(1);
        return retVal;
    }

    public void printAll(){
        System.out.println(container.toString());
    }

    private void moveUp(int index){
        if(index < 1){
            return;
        }

        if(container.get(index)>container.get(index/2)){
            return;
        }else{
            swap(index, index/2);
            moveUp(index/2);
        }
    }

    private void moveDown(int index){
        if(index == container.size()-1)
            return;

        if (index >= container.size()-1)
            return;

        int current = container.get(index);
        if(index * 2 > container.size()-1)
            return;
        if(current > container.get(index*2)){
            swap(index, index*2);
            moveDown(index*2);
        }
        if((index * 2)+1 > container.size()-1)
            return;
        if(current > container.get((index*2)+1)){
            swap(index,(index*2)+1);
            moveDown((index*2)+1);
        }
    }

    private void swap(int a, int b){
        int temp = container.get(a);
        container.add(a,container.get(b));
        container.add(b,temp);
    }
}

```