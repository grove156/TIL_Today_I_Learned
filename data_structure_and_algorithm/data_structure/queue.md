## Queue
### 특징
* FIFO(First in First Out)로 처음 들어간 데이터가 먼저나오는 자료구조
* LIFO 자료구조인 스택과는 반대되는 개념
* 톰캣 서버의 요청을 쌓아두는 큐(요청이 들어오면 들어오는 순서대로 처리)와 같이 순차처리 해야하는 곳에 쓰이는 자료구조
* 자바에서의 큐는 랑크드리스트로 구현됨
* 큐에서 제공하는 API로는
    * add() - 데이터를 저장하고 성공하면 true를 리턴, 저장 실패시 IlligalStateException예외발생
    * offer() - 데이터를 저장하지만 add와는 다르게 저장실패시 예외대신 false를 리턴
    * poll() - 제일 앞에 데이터를 꺼내고 삭제시킴 (없을시 null리턴)
    * remove() - 제일 앞에 데이터를 꺼내고 삭제시킴(없을시 NoSuchElementException))
    * peek() - poll처럼 데이터를 반환하지만 삭제하지는 않음(없을시 null리턴)
    * element() - peek처럼 데이터를 반환하고 삭제하지 않음(없을시 NoSuchException 발생)
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