
# Problem
### LeetCode 251. Flatten 2D Vector
https://leetcode.com/problems/flatten-2d-vector

# Solution
```c++
class Vector2D {
public:
    Vector2D(vector<vector<int>>& vec) {

        row = vec.begin();
        row_end = vec.end();

        if (row != row_end) {
            col = row->begin();
            findNext();
        }
    }

    int next() {
        int elem = cache;
        findNext();
        return elem;
    }

    bool hasNext() {
        return row != row_end;
    }

private:
    int cache;
    vector<vector<int>>::iterator row, row_end;
    vector<int>::iterator col;

    void findNext() {

        if (row == row_end) {
            return;
        }

        if (col != row->end()) {
            cache = *col++;
            return;
        }

        ++row;
        while (row != row_end) {
            if (!row->empty()) {
                col = row->begin();
                cache = *col++;
                break;
            }

            ++row;
        }
    }
};

/**
 * Your Vector2D object will be instantiated and called as such:
 * Vector2D* obj = new Vector2D(vec);
 * int param_1 = obj->next();
 * bool param_2 = obj->hasNext();
 */
```