## Stack
### 특징
### 직접 구현해본 stack
**인터페이스**
```java
public interface MyStack<T> {

    public T pop();
    public void push(T data);
    public T peek();
}

```
**구현체**
```java
public class MyStackImpl<T> implements MyStack<T> {

    Node<T> last;

    @Override
    public T pop() {
        if(last == null)
            return null;
        T retVal = last.getData();
        last = last.getPrev();
        return retVal;
    }

    @Override
    public void push(T data) {
        if(last == null){
            last = new Node<>(data);
        }else{
            Node newNode = new Node<>(data);

            last.setNext(newNode);
            newNode.setPrev(last);
            last = newNode;
        }
    }

    @Override
    public T peek() {
        return last.getData();
    }
}
```