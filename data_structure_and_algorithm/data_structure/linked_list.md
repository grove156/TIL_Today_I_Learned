## Linked List
### 특징
* 연결된 노드들이 집합이 배열처럼 되어있는 구조
* 독적으로 크기를 변경할 수 있음 
* 배열과 다른점은 배열은 크기변경이 힘들지만 빠르고 링크드리스트는 배열 크기를 변경할 수 있지만 노드를 연결해야 함으로 상대적으로 배열보다 느림
* 자바에서는 큐(인터페이스)를 링크드리스트로 구현 ex - ``` Queue<Integer> = new LinkedList<>();``` 
### 직접 구현해본 Linked List
**노드**
```java
public class Node<T> {

    private T data;
    private Node prev;
    private Node next;

    public Node(){};

    public Node(T data){
        this.data = data;
    }

    public T getData() {
        return data;
    }

    public void setData(T data) {
        this.data = data;
    }

    public Node getPrev() {
        return prev;
    }

    public void setPrev(Node prev) {
        this.prev = prev;
    }

    public Node getNext() {
        return next;
    }

    public void setNext(Node next) {
        this.next = next;
    }

    public boolean hasNext(){
        return next != null;
    }
}
```

**인터페이스**
```java
import java.util.List;

public interface MyDoubleLinkedList<T> {
    public void add(T data);
    public void put(T data);
    public T get();
    public T poll();
    public int size();
    public boolean hasData(T data);
    public List<T> getAll();

}
```

**구현체**
```java
public class MyLinkedList<T> implements MyDoubleLinkedList<T> {
    Node<T> first;
    Node<T> last;
    @Override //add front
    public void add(T data) {
        if(first == null){
            first = new Node<>(data);
            last = first;
        }else{
            Node<T> newNode = new Node<>(data);
            newNode.setNext(first);
            first.setPrev(newNode);
            first = newNode;
        }
    }

    @Override //put last
    public void put(T data) {
        if(last == null){
            first = new Node<>(data);
            last = first;
        }else{
            Node<T> newNode = new Node<>(data);
            newNode.setPrev(last);
            last.setNext(newNode);
            last = newNode;
        }

    }

    @Override // get first
    public T get() {
        if(first == null)
            return null;
        if(first == last){
            T data = first.getData();
            first = null;
            last = null;
            return data;
        }
        T data = first.getData();
        first = first.getNext();

        return data;
    }

    @Override // poll last
    public T poll() {
        if(last == null)
            return null;

        if(last == first){
            T data = last.getData();
            last = null;
            first = null;
            return data;
        }

        T data = last.getData();
        last = last.getPrev();
        last.setNext(null);
        return data;
    }

    @Override
    public int size() {
        if(first == null)
            return 0;
        if(first == last)
            return 1;
        Node<T> node = first;
        int count = 0;
        while(node != null){
            count++;
            node = node.getNext();
        }
        return count;
    }

    @Override
    public boolean hasData(T data) {
        if(first == null)
            return false;
        Node<T> node = first;
        while(node != null){
            if(node.getData() == data)
                return true;
            node = node.getNext();
        }
        return false;
    }

    public List<T> getAll(){
        if(first==null)
            return null;
        List<T> list = new ArrayList<>();
        Node<T> node = first;
        while(node != null){
            list.add(node.getData());
            node = node.getNext();
        }
        return list;
    }
}
```