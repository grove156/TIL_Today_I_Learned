##  Hash Map
### 특징

### 직접 구현해본 Hash Map

**Map 컨테이너?!**
```java
public class MapContainer<K,V> {
    private K key;
    private V value;
    private MapContainer<K,V> next;

    public MapContainer() {
    }

    public MapContainer(K key, V value) {
        this.key = key;
        this.value = value;
    }

    public K getKey() {
        return key;
    }

    public void setKey(K key) {
        this.key = key;
    }

    public V getValue() {
        return value;
    }

    public void setValue(V value) {
        this.value = value;
    }

    public MapContainer<K, V> getNext() {
        return next;
    }

    public void setNext(MapContainer<K, V> next) {
        this.next = next;
    }
}

```
**인터페이스**
```java
public interface MyMap<K,V> {
    public void put(K key, V value);
    public V get(K key);
    public boolean containsKey(K key);

}

```
**구현체**
```java
import dataStructures.MapContainer;
import dataStructures.myInterfaces.MyMap;

import java.util.ArrayList;
import java.util.List;

public class MyHashMap<K,V> implements MyMap<K,V> {
    private int size;
    List<MapContainer<K,V>> containers;

    public MyHashMap(){
        this(1000);
    }

    public MyHashMap(int size){
        this.size = size;
        containers = new ArrayList<>(size);
    }

    @Override
    public void put(K key, V value) {
        int index = getKey(hashing(key));
        if(!containers.contains(index)){
            containers.add(index, new MapContainer<>(key,value));
        }else{
            MapContainer<K,V> currentNode = containers.get(index).getNext();
            while(currentNode.getNext() != null){
                currentNode = currentNode.getNext();
            }
            currentNode.setNext(new MapContainer(key, value));
        }
    }

    @Override
    public V get(K key) {
        try{
            int index = getKey(hashing(key));
            MapContainer<K,V> currentNode = containers.get(index);
            while(currentNode != null){
                if(currentNode.getKey() == key)
                    return currentNode.getValue();
                currentNode = currentNode.getNext();
            }
            return null;

        }catch (Exception e){
            return null;
        }
    }

    @Override
    public boolean containsKey(K key) {
        if(containers.size() == 0){
            return false;
        }

        int index = getKey(hashing(key));
        if(containers.get(index)==null){
            return false;
        }else{
            MapContainer<K,V> currentNode = containers.get(index);
            while(currentNode !=null){
                if(currentNode.getKey()==key){
                    return true;
                }
                currentNode = currentNode.getNext();
            }
        }
        return false;
    }

    private int hashing(K key){
        return key.hashCode();
    }

    private int getKey(int hashed){
        return hashed % size;
    }
}

```