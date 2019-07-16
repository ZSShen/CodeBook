
# Problem
### LintCode 601. Flatten 2D Vector
https://www.lintcode.com/problem/flatten-2d-vector/description

# Solution
```c++
class Vector2D {
public:
    Vector2D(vector<vector<int>>& vec2d)
        : total_row(vec2d.size()), index_row(0), total_col(0), index_col(0),
          vec2d(vec2d) {
        // Initialize your data structure here

        if (index_row < total_row) {
            total_col = vec2d[0].size();
        }
    }

    int next() {
        // Write your code here

        return cache;
    }

    bool hasNext() {
        // Write your code here

        // Adjust the iterators first and please be careful about empty vectors.
        while (index_col == total_col) {
            if (index_col == 0 && index_row == total_row) {
                return false;
            }

            ++index_row;
            index_col = 0;
            total_col = (index_row < total_row) ? vec2d[index_row].size() : 0;
        }

        cache = vec2d[index_row][index_col];
        ++index_col;

        return true;
    }

private:
    int total_row;
    int index_row;

    int total_col;
    int index_col;

    std::vector<std::vector<int>> vec2d;

    int cache;
};

/**
 * Your Vector2D object will be instantiated and called as such:
 * Vector2D i(vec2d);
 * while (i.hasNext()) cout << i.next();
 */
```