# Java Collections
> :calendar: *August 19, 2017*

A collection is simply an object that groups multiple elements into a single unit. Collections are
used to store, retrieve, manipulate, and communicate aggregate data.

The Java Collections Framework is a unified architecture for representing and manipulating
collections.

## Interfaces

### [`Collection<E>`](https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html)
The root interface in the collection hierarchy. A collection represents a group of objects known as
elements.

### [`List<E>`](https://docs.oracle.com/javase/8/docs/api/java/util/List.html)
An ordered collection. The user of this interface has precise control over where in the list each
element is inserted. Elements can be accessed by their index integer.

### [`Set<E>`](https://docs.oracle.com/javase/8/docs/api/java/util/Set.html)
A collection that contains no duplicate elements.

### [`Map<K, V>`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html)
An object that maps keys to values. A map cannot contain duplicate keys and each key can map to only
one value.

### [`Queue<E>`](https://docs.oracle.com/javase/8/docs/api/java/util/Queue.html)
A collection designed for holding elements prior to processing. Queues typically (but not always)
order elements in a FIFO (first-in-first-out) manner.

Queues also provide additional insertion, extraction, and inspection operations that exist in two
forms: one throws an exception if the operation failed; the other returns a special value (either
`null` or `false` depending on the operation).

### [`Deque<E>`](https://docs.oracle.com/javase/8/docs/api/java/util/Deque.html)
A collection that supports insertion and removal at both ends (the "head" and "tail"). The name
deque is short for "double ended queue" and is pronounced "deck".

Similarly to the Queue interface, the Deque interface provides additional operations that either
throw an exception or return a special value.

## Classes

### [`ArrayList<E>`](https://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html)
ArrayList is a built-in Java class that stores a list of data of the specified type.

```java
// import the ArrayList class
import java.util.ArrayList;

// create a new programmingLanguages object
ArrayList<String> programmingLanguages = new ArrayList<String>();

// add a String to programming languages
programmingLanguages.add("JavaScript");

// insert a new value at index 0
programmingLanguages.add(0, "Java");

// access the value at index 0
programmingLanguages.get(0);

// get the size of the list
programmingLanguages.size();

// iterate over the list and print each value using a for each loop
for (String language : programmingLanguages) {
  System.out.println(language);
}
```

### [`LinkedList<E>`](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedList.html)
LinkedLists implement both the List and Deque interfaces, which gives them additional functionality
over an ArrayList.

If you are going to be inserting items to the end of the array, an ArrayList will be a better
choice. However, if you are going to be inserting or removing items into arbitrary indexes, a
LinkedList will be faster. This is because an ArrayList will need to reindex every item; but a
LinkedList does not.

### [`Vector<E>`](https://docs.oracle.com/javase/8/docs/api/java/util/Vector.html)
The Vector class implements a growable array of objects. Like the ArrayList, it implements the List
interface. Unlike ArrayLists, Vectors are synchronized and thread-safe.

When in doubt, use ArrayList.

### [`Stack<E>`](https://docs.oracle.com/javase/8/docs/api/java/util/Stack.html)
Stacks extend the Vector class and represent a LIFO (last-in-first-out) stack of objects.

It is recommended to implement the Deque interface (i.e., LinkedList, ArrayDeque) instead of
instantiating a stack.

### [`HashSet<E>`](https://docs.oracle.com/javase/8/docs/api/java/util/HashSet.html)
The HashSet implements the Set interface backed by a hash table (an instance of HashMap).

Note that the order of a HashSet is not guaranteed.

### [`LinkedHashSet<E>`](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedHashSet.html)
LinkedHashSet extends HashSet, except with predictable iteration order. The LinkedHashSet is backed
by a LinkedList to defines the iteration order (the order in which elements were inserted).

### [`TreeSet<E>`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeSet.html)
TreeSet implements the NavigableSet interface and orders elements using either natural ordering or
a comparator provided at creation time.

### [`HashMap<K, V>`](https://docs.oracle.com/javase/8/docs/api/java/util/HashMap.html)
HashMap is a built-in Java class containing a set of key-value pairs.

```java
import java.util.HashMap;

HashMap<String, String> react = new HashMap<String, String>();

react.put("currentVersion", "15.6.1");
react.put("githubStars", "73,000");

// HashMap's keySet method returns a list of keys that can be iterated over
for (String key : react.keySet()) {
  System.out.println(key + ": " react.get(key));
}
```

### [`LinkedHashMap<K, V>`](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedHashMap.html)
LinkedHashMap extends HashMap and is backed by a LinkedList to provide predictable iteration order.

### [`TreeMap<K, V>`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)
TreeMap implements the NavigableMap interface and orders elements using either natural ordering or
a comparator provided at creation time.

### [`PriorityQueue<E>`](https://docs.oracle.com/javase/8/docs/api/java/util/PriorityQueue.html)
An implementation of the Queue interface. Elements are ordered according to natural ordering or by
a comparator. A PriorityQueue relying on natural ordering does not permit insertion of
non-comparable objects.

### [`ArrayDeque<E>`](https://docs.oracle.com/javase/8/docs/api/java/util/ArrayDeque.html)
An implementation of the Deque interface. Faster than Stack when used as a stack, and LinkedList
when used as a queue.
