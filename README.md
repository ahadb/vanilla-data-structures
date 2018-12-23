# vanilla-data-structures
Data structures created with plain ole vanilla JavaScript

## Linked List
In computer science, a Linked list is a linear collection of data elements, whose order is not given by their physical placement in
memory. Instead, each element points to the next. It is a data structure consisting of a collection of nodes which together represent 
a sequence. In its most basic form, each node contains: data, and a reference (in other words, a link) to the next node in the sequence.
This structure allows for efficient insertion or removal of elements from any position in the sequence during iteration. More complex 
variants add additional links, allowing more efficient insertion or removal of nodes at arbitrary positions. A drawback of linked lists
is that access time is linear (and difficult to pipeline). Faster access, such as random access, is not feasible. Arrays have better 
cache locality compared to linked lists.

Linked lists are among the simplest and most common data structures. They can be used to implement several other common abstract data 
types, including lists, stacks, queues, associative arrays, and S-expressions, though it is not uncommon to implement those data 
structures directly without using a linked list as the basis.

```javascript
function LinkedList() {
  this.head = null
  this.tail = null
 }
 
function Node(value, next, prev) {
  this.value = value
  this.next = next
  this.prev = prev
}
 
LinkedList.prototype.addToHead = function(value) {
  var newNode = new Node(value, this.head, null)
  if (this.head) {
    this.head.prev = newNode
  } else {
    this.tail = newNode
  }
  this.head = newNode
}
 
LinkedList.prototype.addToTail = function(value) {
  var newNode = new Node(value, null, this.tail)
  if (this.tail) {
    this.tail.next = newNode
  } else {
    this.head = newNode
  }
  this.tail = newNode
}

LinkedList.prototype.removeHead = function() {
  if (!this.head) {
    return null
  }
  var value = this.head.value
  this.head = this.head.next

  if (this.head) {
    this.head.prev = null
  }
  else this.tail = null

  return value

}

LinkedList.prototype.removeTail = function () {
  if (!this.tail) {
    return null
  }
  let value = this.tail.value
  this.tail = this.tail.prev

  if (this.tail) {
    this.tail.next = null
  } 
  else this.head = null

  return value
}

LinkedList.prototype.search = function (searchValue) {
  let currentNode = this.head

  while (currentNode) {
    if (currentNode.value === searchValue) {
      return currentNode
    }
    currentNode = currentNode.next
  }
  return null
}

const list = new LinkedList()

list.addToHead(10)
list.addToTail(20)

list.search(10)
// => Object { value: 10, next: {…}, prev: null }

list.search(20)
// => Object { value: 20, next: null, prev: {…} }

list.search(3000)
// => null
``` 
