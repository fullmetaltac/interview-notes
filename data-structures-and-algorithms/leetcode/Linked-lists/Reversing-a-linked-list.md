## Reversing a linked list

While reversing a linked list is a common interview problem in itself, it is also a technique that can be a step in solving different problems. Elegantly performing the reversal requires a good understanding of how to move pointers around, which we will aim to achieve in this article.

Imagine that we have a linked list `1 -> 2 -> 3 -> 4`, and we want to return `4 -> 3 -> 2 -> 1`. Let's say we keep a pointer `curr` that represents the current node we are at. Starting with `curr` at the `1`, we need to get the `2` to point to `curr`. The problem is, once we iterate (`curr = curr.next`) to get to the `2`, we no longer have a pointer to the `1` because it is a singly linked list. To get around this, we can use another pointer `prev` that tracks the previous node.

At any given node `curr`, we can set `curr.next = prev` to switch the direction of the arrow. Then, we can update `prev` to be `curr` in preparation for the next node. However, if we change `curr.next`, we will lose that next node. To fix this, we can use a temporary variable `nextNode` to point to the next node before changing any of the other pointers.

```python
def reverse_list(head):
    prev = None
    curr = head
    while curr:
        next_node = curr.next # first, make sure we don't lose the next node
        curr.next = prev      # reverse the direction of the pointer
        prev = curr           # set the current node to prev for the next node
        curr = next_node      # move on
        
    return prev
```

The time complexity of this algorithm is $O(n)$ where $n$ is the number of nodes in the linked list. The while loop runs $n$ times, and the work done at each iteration is $O(1)$. The space complexity is $O(1)$ as we are only using a few pointers.

This exercise is a great one to practice operations on a linked list because it demonstrates the thought process needed. Solutions to linked list problems are usually simple and elegant - to get to them, think about what you need, and solve the problem one step at a time. In this example, we had the following thought process:

- When we are at a node `curr`, we need to set its `next` pointer to the node we were at previously.
  - Use a `prev` pointer to track the previous node.
- The prev pointer needs to also update every iteration.
  - After updating `curr.next`, set `prev = curr` in preparation for the next node.
- If we set `curr.next = prev`, then we lose the reference to the original `curr.next`.
  - Use `nextNode` to keep a reference to the original `curr.next`.


> Example: 24. [Swap Nodes in Pairs](https://leetcode.com/problems/swap-nodes-in-pairs/description/)

> Given the head of a linked list, swap every pair of nodes. For example, given a linked list `1 -> 2 -> 3 -> 4 -> 5 -> 6`, return a linked list `2 -> 1 -> 4 -> 3 -> 6 -> 5`.

Again, let's break down what we need to do step by step, and how we can accomplish it. Consider the first pair of nodes as `A -> B`.

- Starting with head at node A, we need node B to point here.
  - We can accomplish this by doing `head.next.next = head`
- However, if we change `B.next`, we will lose access to the rest of the list.
  - Before applying the change in step 1, save a pointer `nextNode = head.next.next`.
- We now have `B` pointing at `A`. We need to move on to the next pair `C, D`. However, `A` is still pointing at `B`, which isn't what we want. If we move on to the next pair immediately, we will lose a reference to `A`, and won't be able to change `A.next`.
    - Save `A` in another pointer with `prev = head` (we haven't changed `head` yet so it's still pointing at `A`).
    - To move to the next pair, do `head = nextNode`.
- Once we move on to the next pair `C -> D`, we need `A` to point to `D`.
  - Now that head is at `C`, and prev is at `A`, we can do `prev.next = head.next`.
- The first pair `A, B` is fully completed. `B` points to `A` and `A` points to `D`. When we started, we had `head` pointing to `A`. After going through steps 1 - 4, we completed `A, B`. Right now, we have `head` pointing to `C`. If we go through the steps again, we will have complete `C, D`, and be ready for the next pair. We can just repeat steps 1 - 4 until all pairs are swapped. But what do we return at the end?
  - Once all the pairs are finished, we need to return `B`. Unfortunately, we lost the reference to `B` a long time ago.
  - We can fix this by saving `B` in a `dummy` node before starting the algorithm.
- What if there is an odd number of nodes? In step 4, we set `A.next` to `C.next`. What if there were only 3 nodes, so `C.next` was null?
  - Before moving on to the next pair, set `head.next = nextNode`. This is setting `A.next` to `C`.
  - Note that this effect will be overridden by step 4 in the next swap if there is still a pair of nodes remaining.
  - Since in step 2 we do `head.next.next`, we need our while loop condition to check for both `head` and `head.next`. That means if there is only one node left in the list, the while loop will end after the current iteration. As such, this effect wouldn't be overridden.
  - For example, consider the list `A -> B -> C -> D`. At some point, we have `B <-> A C -> D`. Here, we perform step 6, and we get `B -> A -> C -> D`. When we start swapping the pair `C, D`, step 4 will set `A.next` to `D`, which overrides what we just did with step 6. But if `D` didn't exist, then the iteration would have just ended. In that scenario, we would have `B -> A -> C`, which is what we want.
  
To summarize the steps:

- Performs an edge swap from `A -> B -> C -> ...` to `A <-> B C -> ...`.
- Make sure we can still access the rest of the list beyond the current pair (saves `C`).
- Now that `A <-> B` is isolated from the rest of the list, save a pointer to `A` to connect it with the rest of the list later. Move to the next pair.
- Connect the previous pair to the rest of the list. In this case connecting `A -> D`.
- Use a dummy pointer to keep a reference to what we want to return.
- Handle the case when there's an odd number of nodes.

```python
class Solution:
    def swapPairs(self, head: ListNode) -> ListNode:
        # Check edge case: linked list has 0 or 1 nodes, just return
        if not head or not head.next:
            return head

        dummy = head.next               # Step 5
        prev = None                     # Initialize for step 3
        while head and head.next:
            if prev:
                prev.next = head.next   # Step 4
            prev = head                 # Step 3

            next_node = head.next.next  # Step 2
            head.next.next = head       # Step 1

            head.next = next_node       # Step 6
            head = next_node            # Move to next pair (Step 3)

        return dummy
```

The time complexity of this algorithm is $O(n)$ where $n$ is the number of nodes in the linked list. The while loop runs $n$ times, and the work done at each iteration is $O(1)$. The space complexity is $O(1)$ as we are only using a few pointers.

## Reversal as only part of an algorithm

We mentioned that reversing a linked list is "also a technique that can be a step in solving different problems". Before we move on, let's quickly see an example of this.

[2130. Maximum Twin Sum of a Linked List](https://leetcode.com/problems/maximum-twin-sum-of-a-linked-list/) asks for the maximum pair sum. The pairs are the first and last node, second and second last node, third and third last node, etc.

The trivial solution would be to convert the linked list into an array, that way you can access the pairs easily by indexing. The more elegant $O(1)$ space solution is as follows:

- Find the middle of the linked list using the fast and slow pointer technique from the previous article.
- Once at the middle of the linked list, perform a reversal. Basically, reverse only the second half of the list.
- After reversing the second half, every node is spaced `n / 2` apart from its pair node, where `n` is the number of nodes in the list which we can find from step 1.
- With that in mind, create another fast pointer `n / 2` ahead of `slow`. Now, just iterate `n / 2` times from `head` to find every pair sum `slow.val + fast.val`.