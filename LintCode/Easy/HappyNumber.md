# HappyNumber
Source： [http://www.lintcode.com/en/problem/happy-number](http://www.lintcode.com/en/problem/happy-number/#)

```cpp
class Solution {
public:
    /**
     * @param n an integer
     * @return true if this is a happy number or false
     */
    bool isHappy(int n) {
        // Write your code here

        int origin = n;
        int old = -1;
        int sum = n;
        vector<int> vec;
        vec.push_back(sum);

        while (true) {
            int tmp = sum;
            int numOfDigit = 0;
            do {
                numOfDigit += 1;
                tmp /= 10;
            } while (tmp);

            n = sum;
            sum = 0;

            for (int i = 0; i < numOfDigit; i++) {
                int t = n % 10;
                n /= 10;
                sum += t * t;
            }
            if (sum == 1) {
                return true;
            }

            for(int val : vec){
                if(sum == val){
                    return false;
                }
            }

            vec.push_back(sum);

        }
    }
};

```

test case:
```
19
2
88777897
```
