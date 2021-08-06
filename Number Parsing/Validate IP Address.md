
# Problem
### LeetCode 468. Validate IP Address
https://leetcode.com/problems/validate-ip-address

# Solution
```c++
class Solution {
public:
    string validIPAddress(string s) {

        auto index = s.find('.');
        if (index != string::npos) {
            return isV4(s) ? "IPv4" : "Neither";
        }

        index = s.find(":");
        if (index != string::npos) {
            return isV6(s) ? "IPv6" : "Neither";
        }

        return "Neither";
    }

private:
    bool validV4Token(const string& s) {

        int n = s.length();
        if (n == 0 || n >= 4) {
            return false;
        }

        if (n >= 2 && s[0] == '0') {
            return false;
        }

        for (char ch : s) {
            if (!isdigit(ch)) {
                return false;
            }
        }

        return true;
    }

    bool validV6Token(const string& s) {

        int n = s.length();
        if (n == 0 || n >= 5) {
            return false;
        }

        for (char ch : s) {
            if (!(isdigit(ch) ||
                  'a' <= ch && ch <= 'f' ||
                  'A' <= ch && ch <= 'F')) {
                return false;
            }
        }

        return true;
    }

    bool isV4(const string& s) {

        stringstream input(s);
        string token;

        int count = 0;

        while (getline(input, token, '.')) {
            if (!validV4Token(token)) {
                return false;
            }

            int val = stoi(token);
            if (val > 255) {
                return false;
            }

            ++count;
        }

        return count == 4 && s.back() != '.';
    }

    bool isV6(const string& s) {

        stringstream input(s);
        string token;

        int count = 0;

        while (getline(input, token, ':')) {
            if (!validV6Token(token)) {
                return false;
            }

            int val = stoi(token, 0, 16);
            if (val > 65535) {
                return false;
            }

            ++count;
        }

        return count == 8 && s.back() != ':';
    }
};
```