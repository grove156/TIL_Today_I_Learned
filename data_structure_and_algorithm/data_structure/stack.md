## Stack
### 특징
* LIFO(Last in First out)로 가장 마지막에 들어간 데이터가 먼저 나오는 형삭
* 가장 기본적인 자료구조의 형태
* 컴퓨터 내부에 callstack(호출스택)이 이와같은 구조로 되어 있기 때문에 마지막에 불려진 함수가 제일 먼저 실해 되게 됨
* 자바에서는 push(), pop(), peek(), empty(),search()등의 API를 제공함
    * push() - 데이터를 넣음
    * pop() - 데이터를 return (꺼내고 스택에서는 제거돰)
    * peek() - 데이터를 return하지만 제거하진 않음 
    * empty() - 스택이 비어있는지 확인 비어있으면 true
    * search() - 마지막에 들어간 데이터의 인덱스르 반환(없을 경우 -1 라톤)
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