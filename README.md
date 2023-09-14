# Intuition
To solve this problem, we can use a simple iterative approach. We will iterate over the string character by character, following the given algorithm. At each step, we will check if the character requires any special action and update our result accordingly.
# Approach
1. Initialize variables i (index), sign (sign of the integer), and result (the integer value) to 0.
2. Ignore any leading whitespace by incrementing i until we reach a non-whitespace character.
3. Check for a sign character (+ or -). If a sign is present, update the sign variable accordingly and increment i.
4. Convert the remaining digits to an integer by iterating through the string. We will iterate until i is less than the length of the string and the current character is a digit.
5. Inside the loop, convert the current digit character to an actual digit value using the appropriate conversion operation (digit = s[i].to_i in Ruby and int digit = s[i] - '0' in C and Java).
6. Check for overflow: If the result is greater than the maximum 32-bit signed integer value divided by 10, or if it is equal to the maximum value divided by 10 and the current digit is greater than 7, we have an overflow condition. Return the maximum or minimum value accordingly based on the sign.
7. If there is no overflow, update the result by multiplying it by 10 and adding the current digit.
8. Increment i to move to the next character.
9. After the loop ends, multiply the result by the sign to get the final result.
10. Return the final result.

# Complexity
- Time complexity: O(n), where n is the length of the input string. We iterate over the string once.
- Space complexity: O(1), as we only use a constant amount of additional space for the variables.

# Code
```С []
#include <stdio.h>

int myAtoi(char * s){
    int i = 0;
    int sign = 1;
    int result = 0;
    
    // Ignore leading whitespace
    while (s[i] == ' ') {
        i++;
    }
    
    // Check for sign
    if (s[i] == '+' || s[i] == '-') {
        sign = (s[i] == '+') ? 1 : -1;
        i++;
    }
    
    // Convert digits to integer
    while (s[i] >= '0' && s[i] <= '9') {
        int digit = s[i] - '0';
        
        // Check for overflow
        if (result > (INT_MAX / 10) || (result == (INT_MAX / 10) && digit > 7)) {
            return (sign == 1) ? INT_MAX : INT_MIN;
        }
        
        result = result * 10 + digit;
        i++;
    }
    
    return sign * result;
}
```
```С++ []
class Solution {
public:
    int myAtoi(string s) {
        int i = 0;
        int sign = 1;
        int result = 0;
        
        // Ignore leading whitespace
        while (s[i] == ' ') {
            i++;
        }
        
        // Check for sign
        if (s[i] == '+' || s[i] == '-') {
            sign = (s[i] == '+') ? 1 : -1;
            i++;
        }
        
        // Convert digits to integer
        while (s[i] >= '0' && s[i] <= '9') {
            int digit = s[i] - '0';
            
            // Check for overflow
            if (result > (INT_MAX / 10) || (result == (INT_MAX / 10) && digit > 7)) {
                return (sign == 1) ? INT_MAX : INT_MIN;
            }
            
            result = result * 10 + digit;
            i++;
        }
        
        return sign * result;
    }
};
```
```Java []
class Solution {
    public int myAtoi(String s) {
        int i = 0;
        int sign = 1;
        int result = 0;
    
        // Ignore leading whitespace
        while (i < s.length() && s.charAt(i) == ' ') {
            i++;
        }
    
        // Check for sign
        if (i < s.length() && (s.charAt(i) == '+' || s.charAt(i) == '-')) {
            sign = (s.charAt(i) == '+') ? 1 : -1;
            i++;
        }
    
        // Convert digits to integer
        while (i < s.length() && Character.isDigit(s.charAt(i))) {
            int digit = s.charAt(i) - '0';
            
            // Check for overflow
            if (result > (Integer.MAX_VALUE / 10) || (result == (Integer.MAX_VALUE / 10) && digit >7)) {
            return (sign == 1) ? Integer.MAX_VALUE : Integer.MIN_VALUE;
            }
        
            result = result * 10 + digit;
            i++;
        }

        return sign * result;
    }
}
```
```python2 []
class Solution(object):
    def myAtoi(self, s):
        """
        :type s: str
        :rtype: int
        """
        i = 0
        sign = 1
        result = 0
        
        # Ignore leading whitespace
        while i < len(s) and s[i] == ' ':
            i += 1
        
        # Check for sign
        if i < len(s) and (s[i] == '+' or s[i] == '-'):
            sign = 1 if s[i] == '+' else -1
            i += 1
        
        # Convert digits to integer
        while i < len(s) and s[i].isdigit():
            digit = int(s[i])
            
            # Check for overflow
            if result > (2**31 - 1) // 10 or (result == (2**31 - 1) // 10 and digit > 7):
                return 2**31 - 1 if sign == 1 else -2**31
            
            result = result * 10 + digit
            i += 1
        
        return sign * result

```
```python3 []
class Solution:
    def myAtoi(self, s: str) -> int:
        i = 0
        sign = 1
        result = 0
        
        # Ignore leading whitespace
        while i < len(s) and s[i] == ' ':
            i += 1
        
        # Check for sign
        if i < len(s) and (s[i] == '+' or s[i] == '-'):
            sign = 1 if s[i] == '+' else -1
            i += 1
        
        # Convert digits to integer
        while i < len(s) and s[i].isdigit():
            digit = int(s[i])
            
            # Check for overflow
            if result > (2**31 - 1) // 10 or (result == (2**31 - 1) // 10 and digit > 7):
                return 2**31 - 1 if sign == 1 else -2**31
            
            result = result * 10 + digit
            i += 1
        
        return sign * result
```
```C# []
public class Solution {
    public int MyAtoi(string s) {
        int i = 0, sign = 1, result = 0;
        // Ignore leading whitespace
        while (i < s.Length && s[i] == ' ') {
            i++;
        }
        // Check for sign
        if (i < s.Length && (s[i] == '+' || s[i] == '-')) {
            sign = s[i++] == '+' ? 1 : -1;
        }
        // Convert digits to integer
        while (i < s.Length && s[i] >= '0' && s[i] <= '9') {
            int digit = s[i++] - '0';
            // Check for overflow
            if (result > int.MaxValue / 10 || (result == int.MaxValue / 10 && digit > 7)) {
                return sign == 1 ? int.MaxValue : int.MinValue;
            }
            result = result * 10 + digit;
        }
        return sign * result;
    }
}
```
```ruby []
# @param {String} s
# @return {Integer}
def my_atoi(s)
    i = 0
    sign = 1
    result = 0
    
    # Ignore leading whitespace
    while i < s.length && s[i] == ' '
        i += 1
    end
    
    # Check for sign
    if i < s.length && (s[i] == '+' || s[i] == '-')
        sign = -1 if s[i] == '-'
        i += 1
    end
    
    # Convert digits to integer
    while i < s.length && s[i].match?(/\d/)
        digit = s[i].to_i
        
        # Check for overflow
        if result > (2**31 - 1) / 10 || (result == (2**31 - 1) / 10 && digit > 7)
            return sign == 1 ? 2**31 - 1 : -2**31
        end
        
        result = result * 10 + digit
        i += 1
    end
    
    return sign * result
end
```
