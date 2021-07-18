
# Problem
### LeetCode 641. Design Circular Deque
https://leetcode.com/problems/design-circular-deque

# Solution
```c++
class MyCircularDeque {
public:
    /** Initialize your data structure here. Set the size of the deque to be k. */
    MyCircularDeque(int k)
        : q(k), size(0), capacity(k), front(0), rear(0)
    { }

    /** Adds an item at the front of Deque. Return true if the operation is successful. */
    bool insertFront(int value) {

        if (size == capacity) {
            return false;
        }

        front = (front - 1 + capacity) % capacity;
        q[front] = value;

        if (size == 0) {
            rear = front;
        }
        ++size;

        return true;
    }

    /** Adds an item at the rear of Deque. Return true if the operation is successful. */
    bool insertLast(int value) {

        if (size == capacity) {
            return false;
        }

        rear = (rear + 1) % capacity;
        q[rear] = value;

        if (size == 0) {
            front = rear;
        }
        ++size;

        return true;
    }

    /** Deletes an item from the front of Deque. Return true if the operation is successful. */
    bool deleteFront() {

        if (size == 0) {
            return false;
        }

        front = (front + 1) % capacity;

        --size;
        return true;
    }

    /** Deletes an item from the rear of Deque. Return true if the operation is successful. */
    bool deleteLast() {

        if (size == 0) {
            return false;
        }

        rear = (rear - 1 + capacity) % capacity;

        --size;
        return true;
    }

    /** Get the front item from the deque. */
    int getFront() {
        if (size == 0) {
            return -1;
        }
        return q[front];
    }

    /** Get the last item from the deque. */
    int getRear() {
        if (size == 0) {
            return -1;
        }
        return q[rear];
    }

    /** Checks whether the circular deque is empty or not. */
    bool isEmpty() {
        return size == 0;
    }

    /** Checks whether the circular deque is full or not. */
    bool isFull() {
        return size == capacity;
    }

private:
    vector<int> q;
    int size, capacity;
    int front, rear;
};

/**
 * Your MyCircularDeque object will be instantiated and called as such:
 * MyCircularDeque* obj = new MyCircularDeque(k);
 * bool param_1 = obj->insertFront(value);
 * bool param_2 = obj->insertLast(value);
 * bool param_3 = obj->deleteFront();
 * bool param_4 = obj->deleteLast();
 * int param_5 = obj->getFront();
 * int param_6 = obj->getRear();
 * bool param_7 = obj->isEmpty();
 * bool param_8 = obj->isFull();
 */
```