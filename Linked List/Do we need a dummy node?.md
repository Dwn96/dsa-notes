## **A simple mental checklist**

Whenever you encounter a linked list problem, ask yourself:

**Question 1: Could the original head change?**

For example:
- Removing the first node.    
- Reversing the entire list.    
- Merging two lists where either list could provide the first node.    

A dummy node is often useful.

**Question 2: Am I building a new list?**

For example:

- Add Two Numbers.    
- Merge Two Sorted Lists.    
- Partition List.    

A dummy node makes appending nodes much easier because you don't need separate logic for the first node.

**Question 3: Am I just traversing or rearranging existing nodes while keeping the head?**

For example:

- Reorder List.    
- Find Middle.    
- Linked List Cycle.
You probably don't need one.