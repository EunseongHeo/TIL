
# 2.2. Linked List 구현
###### 2_1_Concept_LinkedList(0813).md 파일에서 설명한 LInked List의  개념을 토대로 Java로 LInked List 구현해 보기


## 구현
#### 구현 순서
1. Node 클래스 정의 (chk)
2. LinkedList 클래스의 객체 정의 
3. LinkedList 클래스에 필요한 클래스 및 메서드 정의
    - 추가
      - addFirst(Object value)
      - addLast(Object value)
      - add(int index, Object value)
    - 삭제
      - removeFirst()
      - removeLast()
      - remove(int index)
    - 탐색
       - indexOf(Object data)
    - 리스트 크기
      - size()
    - 노드 값 얻기
       - get(int index)
    - 출력
       - toString()
    - 반복
      - Iterator
        - next()
        - hasNext()
        - add(Object data)
        - remove()

```java
package LInkedListTest;

import java.util.ListIterator;

public class LinkedListTest {
    private Node head;  //첫번째 노드를 가리키는 필드
    private Node tail;  //마지막 노드를 가리키는 필드
    private int size = 0;   //리스트의 크기값을 저장하는 필드

    private class Node {
        Object data ;
        Node next;
        public Node(){}
        public Node(Object data){
            this.data = data;
        }
        public Node(Object data, Node next){
            this.data = data;
            this.next = next;
        }
        public String toString(){
            return String.valueOf(this.data);
        }
    }

    //To add the element into the list
    public void addFirst(Object data){
        Node newNode = new Node(data);
        newNode.next = head;
        head = newNode;
        size++;
        if(head.next == null) tail = head;
    }

    public  void addLast(Object data){
        Node newNode = new Node(data);
        if(size==0) {
            addFirst(data);
        } else {
            tail.next = newNode;
            tail = newNode;
            size ++;
        }
    }

    Node node(int index){
        Node x = head;
        for (int i = 0; i < index; i++)x = x.next;
        return x;
    }

    public void add(int index, Object data){
        if(index == 0) addFirst(data);
        else{
            Node temp1 = node(index-1);
            Node temp2 = temp1.next;
            Node newNode = new Node(data);
            temp1.next = newNode;
            newNode.next = temp2;
            size++;
            if(newNode.next == null) tail = newNode;
        }
    }

    //To remove the element from the list
    public Object removeFirst(){
        Node target = head;
        head = head.next;
        Object dataDeleted = target.data;
        target = null;
        size--;
        return dataDeleted;
    }

    public Object remove(int index) {
        if(index==0) return removeFirst();
        Node temp = node(index-1);
        Node target = node(index);
        temp.next = target.next;

        Object dataDeleted = target.data;
        if(target == tail) tail = temp;

        target = null;
        size--;

        return dataDeleted;
    }

    //To search the index which has 'data' value
    public int indexOf(Object data){
//        탐색 대상 => target
        Node target = head;
        int index = 0;
        while (target.data != data){
            target = target.next;
            index++;
            if(target ==  null) return -1;
        }
//        탐색 대상을 찾았다면 대상의 인덱스 값을 리턴합니다.
        return index;
    }

    //To get the size of the list
    public int size(){
        return size;
    }

    //To get the value of the node which was indexed. 
    public Object get(int index){
        Node temp = node(index);
        return temp.data;
    }

    public String toString(){
        if(head == null) return "[]";

        Node temp = head;
        String str = "[";
        while (temp.next != null){
            str += temp.data + ", ";
            temp = temp.next;
        }
        str += temp.data;
        return str + "]";
    }
    
    //Iterate
//    반복자를 생성하여 리턴한다.
    public ListIterator listIterator(){
        return new ListIterator();
    }

    class ListIterator{
        private Node lastReturned;
        private Node next;
        private int nextIndex;

        ListIterator(){
            next = head;
            nextIndex = 0;
        }

        public Object next(){
            lastReturned = next;
            next = next.next;
            nextIndex++;
            return lastReturned.data;
        }

        public boolean hasNext(){
            return nextIndex < size();
        }

        public void add(Object data){
            Node newNode = new Node(data);
            if(lastReturned == null){
                head = newNode;
                newNode.next = next;
            } else {
                lastReturned.next = newNode;
                newNode.next = next;
            }
            lastReturned = newNode;
            nextIndex++;
            size++;
        }

        public void remove(){
            if(nextIndex == 0){
                throw new IllegalStateException();
            }
            LinkedListTest.this.remove(nextIndex-1);
            nextIndex--;
        }
    }
}

```

linked list 개념 참고 -
[Opentutorials.org LInked list](https://opentutorials.org/module/1335/8821)

linked list 구현 참고 -
[Opentutorials.org LInked list - Java 구현](https://opentutorials.org/module/1335/8857)
