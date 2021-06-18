## Queue
### 특징
### 직접 구현해본 queue
인터페이스
```java
public interface MyQueue<T> {
    public T poll();
    public T peek();
    public void add(T data);
}

```

구현부
```java
public class MyQueueImpl<T> implements MyQueue<T> {

    Node<T> first;
    Node<T> last;
    
    @Override
    public T poll() {
        if(first == null)
            return null;
        T data = first.getData();
        first = first.getNext();
        return data;

    }

    @Override
    public T peek() {
        if(first == null)
            return null;

        T data = first.getData();
        return data;
    }

    @Override
    public void add(T data) {
        if(first == null){
            first = new Node<>(data);
            last = first;
        }else{
            Node<T> newNode = new Node<>(data);
            last.setNext(newNode);
            last = newNode;
        }
    }
}

```