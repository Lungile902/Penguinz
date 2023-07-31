# Penguinz
SchoolHomeWork
public class MyLinkedList<E>  {
    private Node<E> head, tail;

    public MyLinkedList() {
        head = null;
        tail = null;
    }

    /** Return the head element in the list */
    public E getFirst() {
        if (head == null) {
            return null;
        }
        else {
            return head.element;
        }
    }

    /** Return the last element in the list */
    public E getLast() {
        if (head==null) {
            return null;
        }
        else {
            return tail.element;
        }
    }

    /** Add an element to the beginning of the list */
    public void prepend(E e) {
        Node<E> newNode = new Node<>(e); // Create a new node
        newNode.next = head; // link the new node with the head
        head = newNode; // head points to the new node

        if (tail == null) // the new node is the only node in list
            tail = head;
    }

    /** Add an element to the end of the list */
    public void append(E item) {

        Node<E> newNode = new Node<>(item); // Create a new for element e

        if (head == null) {
            head = tail = newNode; // The new node is the only node in list
        }
        else {
            tail.next = newNode; // Link the new with the last node
            tail = newNode; // tail now points to the last node
        }
    }

    /** Remove the head node and
     *  return the object that is contained in the removed node. */
    public E removeFirst() {
        if (head == null) {
            return null;
        }
        else {
            E temp = head.element;
            head = head.next;
            if (head == null) {
                tail = null;
            }
            return temp;
        }
    }

    public MyLinkedList merge(MyLinkedList plist) //merge first semester marks and second seester marks
    {
        Node<E> ptrThis, ptrParam;
        ptrThis = head;
        ptrParam = plist.head;
        MyLinkedList returnlist = new MyLinkedList();

        if(head==null)// caling list is empty - set this list to param list
        {
            while(ptrParam != null)
            {
                returnlist.append(ptrParam.element);
                ptrParam = ptrParam.next;
            }
            return returnlist;

        }

        if(plist.head == null)// param list is empty - make no changes
        {
            while(ptrThis != null)
            {
                returnlist.append(ptrThis.element);
                ptrThis = ptrThis.next;
            }
            return returnlist; 
        }

        while((ptrThis != null) && (ptrParam != null))// continue up to end of one list
        {
            if (((Comparable)ptrThis.element).compareTo(ptrParam.element)==0)
            {
                returnlist.append(ptrThis.element);
                ptrThis = ptrThis.next;
            }
            else
            {
                ptrParam = ptrParam.next;
            }
        }

        if(ptrThis == null)// copy rest of param list
        {
            while(ptrParam != null)
            {
                returnlist.append(ptrParam.element);
                ptrParam = ptrParam.next;
            }
        }
        if(ptrParam == null) // copy rest of calling list
        {
            while(ptrThis != null)
            {
                returnlist.append(ptrThis.element);
                ptrThis = ptrThis.next;
            }
        }

        return returnlist;
    }

    public void swap(int pos) throws Exception
    {
        int i =1;
        Node<E> p = this.head;
        if(head == null)
        {
            throw new Exception("There are no elements in the list");
        }
        while(i<pos-1)
        {
            p=p.next;
            i++;
        }
        Node<E> q = p.next;
        Node<E> r = q.next;
        //storing the swaped elements 
        q.next = r.next;
        r.next = q;
        p.next = r;
    }

    public boolean delete(E item)
    {
        Node<E> ptr = head;
        Node<E> prvPtr = null;
        while (ptr!= null&& ((Comparable)ptr.element).compareTo(item)!= 0)
        {
            prvPtr=ptr;
            ptr=ptr.next;
        }
        if (ptr == null)//item not found
            return false;
        if (ptr==head) // item is first element
            head= head.next;
        else // general case
            prvPtr.next=ptr.next;
        if (ptr==tail)// last element
            tail=prvPtr;
        return true;
    }

    public String toString() {
        String result = "[";

        Node<E> ptr = head;
        for (ptr= head;ptr!=null; ptr=ptr.next) 
        {
            result = result +  ptr.element.toString();     
            if (ptr.next != null)
                result = result + ","; // add commas but not to the final 1   
        }
        result += "]"; // Insert the closing ] in the string
        return result;
    }

    public void clear() {
        head = tail = null;
    }

    private static class Node<E> {
        E element;
        Node<E> next;

        public Node(E element) {
            this.element = element;
            next = null;
        }
    }

} // end myLinkedList class


/**
 * Write a description of class StackAsMyLinkeList here.
 *
 * @author (your name)
 * @version (a version number or a date)
 */
public class StackAsMyLinkedList<E>
{
    MyLinkedList<E> theStack;
    public StackAsMyLinkedList()
    {  theStack = new MyLinkedList<E>();       
    }

    public void push(E newElement) //insert at head
    {  
        theStack.prepend(newElement);
    }

    public E pop() //remove from head
    {  
        E temp = null;
        boolean isDone = false;

        temp = theStack.getFirst();
        if (temp != null)
        {
            isDone=theStack.delete(temp);
        }
        if (isDone)
            return temp;
        else
            return null;
    }

    public String toString()
    {
        return theStack.toString();
    }

}


/**
 * Write a description of class TestMyLinkedList here.
 *
 * @author (your name)
 * @version (a version number or a date)
 */
import java.util.Scanner;
public class TestMyLinkedList
{
    public static void main(String []args) throws Exception
    {
        Scanner input = new Scanner(System.in);
        Integer top = null;
        MyLinkedList<Integer> list = new MyLinkedList<Integer>(); 
        MyLinkedList<Integer> list2 = new MyLinkedList<Integer>();
        StackAsMyLinkedList<Integer> myStack = new StackAsMyLinkedList<Integer>();

        //print empty list
        System.out.println("The list of students, empty list");
        System.out.println(list);

        //fill the list
        list.append(new Integer(04));
        list.append(new Integer(80));
        list.append(new Integer(45));
        list.append(new Integer(69));
        list.append(new Integer(78));
        list.append(new Integer(35));
        System.out.println("\nThe list of students");
        System.out.println(list);
        
        //if parameter list is empty
        System.out.println("\nShow marks that are similar to the second semester marks, parameter list empty");
        System.out.println(list.merge(list2));

        //swap list adjacent list from second position
        System.out.println("\nMarks swaped adjacent to position 2");
        list.swap(2);
        System.out.println(list);

        //fill second list (second semester marks)
        list2.append(new Integer(45));
        list2.append(new Integer(69));
        list2.append(new Integer(50));
        list2.append(new Integer(71));
        list2.append(new Integer(66));
        
        //show marks swaped
        System.out.println("\nShow marks that are similar to the second semester marks");
        System.out.println(list.merge(list2));

        //clear list
        list.clear();
        list2.clear();
        
        //if list is empty
        System.out.println("\nShow marks that are similar to the second semester marks, empty ist");
        System.out.println(list.merge(list2));
        
        //add new elements to the Stack
        System.out.println("\nNew Students addedd on the stack");
        myStack.push(new Integer(27));
        myStack.push(new Integer(94));
        myStack.push(new Integer(55));
        System.out.println(myStack +" ");

        System.out.println("\nDo you want to undo the previos action? ");
        char answer = input.next().charAt(0);
        if(Character.toUpperCase(answer)=='Y')
        {
            top = (Integer) myStack.pop();
            if (top != null)
                System.out.println("Top is: " + top.intValue() +"\n");
            else
                System.out.println("Empty Stack");
            System.out.println(myStack +" ");
        }
    }
}


This code features data structures that you can use to append, prepend, getlast, swap, and removefirst node to the linked list.
There is also a stack data structure that you can use to add or reomove items from your list.
