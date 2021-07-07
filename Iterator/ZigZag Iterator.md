
# Problem
### LeetCode 281. Zigzag Iterator
https://leetcode.com/problems/zigzag-iterator

# Solution
```c++
class ZigzagIterator {
public:
    ZigzagIterator(vector<int>& v1, vector<int>& v2) {

        k = 0;

        if (!v1.empty()) {
            slots.push_back({v1.begin(), v1.end()});
            ++k;
        }
        if (!v2.empty()) {
            slots.push_back({v2.begin(), v2.end()});
            ++k;
        }

        rover = slots.begin();
        end = slots.end();
    }

    int next() {
        int elem;

        auto& vec_bgn = rover->first;
        auto& vec_end = rover->second;

        elem = *vec_bgn++;
        if (vec_bgn == vec_end) {
            rover = slots.erase(rover);
            --k;
        } else {
            ++rover;
        }

        if (rover == end) {
            rover = slots.begin();
        }

        return elem;
    }

    bool hasNext() {
        return k > 0;
    }

private:
    int k;
    list<pair<vector<int>::iterator, vector<int>::iterator>> slots;
    list<pair<vector<int>::iterator, vector<int>::iterator>>::iterator rover, end;
};

/**
 * Your ZigzagIterator object will be instantiated and called as such:
 * ZigzagIterator i(v1, v2);
 * while (i.hasNext()) cout << i.next();
 */
```