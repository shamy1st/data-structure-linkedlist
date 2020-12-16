# Linked List

![](https://github.com/shamy1st/data-structure/blob/main/images/linkedlist.png)

--                 | indexing | search | add    | remove(index or value)
-------------------|----------|--------|--------|-----------------------
Singly Linked List | O(n)     | O(n)   | O(1)   | O(n)
Doubly Linked List | O(n)     | O(n)   | O(1)   | O(n)

--                 | addFirst | addMiddle | addLast | removeFirst | removeMiddle | removeLast
-------------------|----------|-----------|---------|-------------|--------------|-----------
Singly Linked List | O(1)     | O(n)      | O(1)    | O(1)        | O(n)         | O(n)
Doubly Linked List | O(1)     | O(n)      | O(1)    | O(1)        | O(n)         | O(1)

![](https://github.com/shamy1st/data-structure/blob/main/images/singly-doubly-linkedlist.png)

        public class Main {
            public static void main(String[] args) {
                LinkedList<Integer> list = new LinkedList<>();
                list.addLast(10);
                list.addLast(20);
                list.addLast(30);
                list.removeLast();
                System.out.println(list.size());
            }
        }

        //Singly Linked List
        public class LinkedList<T> {
            private class Node<T> {
                private T value;
                private Node<T> next;

                public Node(T value) {
                    this.value = value;
                }
            }

            private Node<T> head;
            private Node<T> tail;
            private int size;

            private boolean isEmpty() {
                return head == null;
            }

            //O(1)
            public void addFirst(T item) {
                Node node = new Node(item);
                if(isEmpty())
                    head = tail = node;
                else {
                    node.next = head;
                    head = node;
                }

                size++;
            }

            //O(1)
            public void addLast(T item) {
                Node node = new Node(item);
                if(isEmpty())
                    head = tail = node;
                else {
                    tail.next = node;
                    tail = node;
                }

                size++;
            }

            //O(n)
            public int indexOf(T item) {
                Node current = head;
                int index = 0;
                while(current != null) {
                    if(current.value == item)
                        return index;

                    current = current.next;
                    index++;
                }
                return -1;
            }

            //O(n)
            public boolean contains(T item) {
                return indexOf(item) != -1;
            }

            //O(1)
            public void removeFirst() {
                if(isEmpty())
                    throw new NoSuchElementException(); //like java implementation

                if(head == tail) {
                    head = tail = null;
                    size = 0;
                    return;
                }

                Node second = head.next;
                head.next = null;
                head = second;
                size--;
            }

            //O(n)
            public void removeLast() {
                if(isEmpty())
                    throw new NoSuchElementException(); //like java implementation

                if(head == tail) {
                    head = tail = null;
                    size = 0;
                    return;
                }

                Node current = head;
                while(current != null) {
                    if(current.next == tail) {
                        current.next = null;
                        tail = current;
                    }
                    current = current.next;
                }
                size--;
            }

            public int size() {
                return size;
            }
        }
