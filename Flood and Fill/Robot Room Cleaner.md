
# Problem
### LeetCode 489. Robot Room Cleaner
https://leetcode.com/problems/robot-room-cleaner

# Solution
```c++
/**
 * // This is the robot's control interface.
 * // You should not implement it, or speculate about its implementation
 * class Robot {
 *   public:
 *     // Returns true if the cell in front is open and robot moves into the cell.
 *     // Returns false if the cell in front is blocked and robot stays in the current cell.
 *     bool move();
 *
 *     // Robot will stay in the same cell after calling turnLeft/turnRight.
 *     // Each turn will be 90 degrees.
 *     void turnLeft();
 *     void turnRight();
 *
 *     // Clean the current cell.
 *     void clean();
 * };
 */
class Solution {
public:
    void cleanRoom(Robot& robot) {

        /**
         *  TC: O(N), where
         *      N is the number of cells
         *
         *  SC: O(N), where
         *      N is the number of cells
         *
         */

        unordered_set<string> set;
        backTrack(robot, set, 0, 0, UP);
    }

private:
    enum {
        UP = 0,
        RIGHT = 90,
        DOWN = 180,
        LEFT = 270
    };

    void backTrack(
        Robot& robot, unordered_set<string>& set, int x, int y, int direct) {

        string code = to_string(x) + ',' + to_string(y);
        if (set.count(code) == 1) {
            return;
        }

        robot.clean();
        set.emplace(move(code));

        for (int i = 0 ; i < 4 ; ++i) {
            if (robot.move()) {
                switch (direct) {
                    case UP:
                        backTrack(robot, set, x, y + 1, direct);
                        break;
                    case RIGHT:
                        backTrack(robot, set, x + 1, y, direct);
                        break;
                    case DOWN:
                        backTrack(robot, set, x, y - 1, direct);
                        break;
                    case LEFT:
                        backTrack(robot, set, x - 1, y, direct);
                        break;
                }

                // Since we've adopted move() to move the robot one step
                // forward, we now need to make it move back by one
                // step.
                robot.turnLeft();
                robot.turnLeft();
                robot.move();
                robot.turnRight();
                robot.turnRight();
            }

            direct += 90;
            direct %= 360;
            robot.turnRight();
        }
    }
};
```
