# 7. Reverse Integer

Given a signed 32-bit integer x, return x with its digits reversed. If reversing x causes the value to go outside the signed 32-bit integer range \[-231, 231 - 1\], then return 0.

Assume the environment does not allow you to store 64-bit integers \(signed or unsigned\).

Example 1:

Input: x = 123

Output: 321

Example 2:

Input: x = -123

Output: -321

Example 3:

Input: x = 120

 Output: 21

Example 4:

Input: x = 0

Output: 0

```text
class Solution{
    public int reverse(int x){
        int ans = 0;
        while(x != 0){
            int pop = x % 10;
            if (ans > Integer.MAX_VALUE / 10 ||(ans == Integer.MAX_VALUE / 10 && pop > 7))
            return 0;
            if (ans < Integer.MIN_VALUE / 10 ||(ans == Integer.MAX_VALUE /10 && pop <-8 ))
            return 0;
            ans = ans * 10 + pop;
            x /= 10;
        }
        return ans;
    }
}
```

這個只要把整數判斷對就行,

有的數是超出範圍的,我們將它排除.

反轉的算法就是

比如 123456789 除以 10 就得到餘數 9 那麼之後再把 9 \*10 循環下來 9就到了 1的位置

每次過後把這個數整除10.

最最最最重要的!!!!! 2^31-1=2147483647,-2^31=-2147483648

