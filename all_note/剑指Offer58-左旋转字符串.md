### 剑指Offer58-左旋转字符串

字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。

``` markdown
输入: s = "abcdefg", k = 2
输出: "cdefgab"

输入: s = "lrloseumgh", k = 6
输出: "umghlrlose"
```

**限制：**

- `1 <= k < s.length <= 10000`



**思路1：** 尾部添加

将前面的字符串添加到尾部，返回对应的结果。

``` java
class Solution {
    public String reverseLeftWords(String s, int n) {
        if (s == null || n <= 0) {
            return null;
        }

        StringBuilder str = new StringBuilder();
        int length = s.length();
        for (int i = n; i < n + length; i++) {
            str.append(s.charAt(i % length));
        }

        return str.toString();
    }
}
```



**思路2** ： 三次旋转

分三次旋转字符串：

- 旋转前 k 个字符
- 旋转后 n-k 个字符
- 旋转整个字符串

``` cpp
class Solution {
public:
    string reverseLeftWords(string s, int n) {
        reverse(s.begin(),s.begin()+n);
        reverse(s.begin()+n,s.begin()+s.size());
        reverse(s.begin(),s.end());
        return s;
    }
};

```

