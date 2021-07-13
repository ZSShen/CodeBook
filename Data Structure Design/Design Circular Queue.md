
# Problem
### LeetCode 622. Design Circular Queue
https://leetcode.com/problems/design-circular-queue

# Solution
```c++
class MyCircularQueue {
public:
    MyCircularQueue(int k)
        : records(k), capacity(k), size(0), front(0), rear(0)
    {
        /**
         *  front: Point to the first element.
         *  rear : Point to the empty space after the last element.
         *
         *  f
         *  a b c _
         *        r
         */
    }

    bool enQueue(int value) {

        if (size == capacity) {
            return false;
        }

        records[rear++] = value;
        rear %= capacity;
        ++size;

        return true;
    }

    bool deQueue() {

        if (size == 0) {
            return false;
        }

        records[front++];
        front %= capacity;
        --size;

        return true;
    }

    int Front() {

        if (size == 0) {
            return -1;
        }

        return records[front];
    }

    int Rear() {

        if (size == 0) {
            return -1;
        }

        int idx = (rear - 1 >= 0) ? rear - 1 : capacity - 1;
        return records[idx];
    }

    bool isEmpty() {
        return size == 0;
    }

    bool isFull() {
        return size == capacity;
    }

private:
    vector<int> records;
    int capacity, size;
    int front, rear;
};

/**
 * Your MyCircularQueue object will be instantiated and called as such:
 * MyCircularQueue* obj = new MyCircularQueue(k);
 * bool param_1 = obj->enQueue(value);
 * bool param_2 = obj->deQueue();
 * int param_3 = obj->Front();
 * int param_4 = obj->Rear();
 * bool param_5 = obj->isEmpty();
 * bool param_6 = obj->isFull();
 */
```