### 剑指offer 41.数据流中的中位数

如何得到一个数据流中的中位数？如果从数据流中读出奇数个数值，那么中位数就是所有数值排序之后位于中间的数值。如果从数据流中读出偶数个数值，那么中位数就是所有数值排序之后中间两个数的平均值。

例如，

[2,3,4] 的中位数是 3

[2,3] 的中位数是 (2 + 3) / 2 = 2.5

设计一个支持以下两种操作的数据结构：

- void addNum(int num) - 从数据流中添加一个整数到数据结构中。
- double findMedian() - 返回目前所有元素的中位数。

``` markdown
输入：
["MedianFinder","addNum","addNum","findMedian","addNum","findMedian"]
[[],[1],[2],[],[3],[]]
输出：[null,null,null,1.50000,null,2.00000]

输入：
["MedianFinder","addNum","findMedian","addNum","findMedian"]
[[],[2],[],[3],[]]
输出：[null,null,2.00000,null,2.50000]
```



**思路：** 双堆

维护一个小根堆和大根堆，分别保存目前数据流更大和更小的一半，中位数要么是一个堆的堆顶，要么是两个堆顶的平均数。具体的添加和返回操作根据数据流的个数奇偶性决定。

``` java
class MedianFinder {
    PriorityQueue<Integer> big; // 存储较大的一半
    PriorityQueue<Integer> small; // 存储较小的一半
    /** initialize your data structure here. */
    public MedianFinder() {
        big = new PriorityQueue<>();
        small = new PriorityQueue<>((Integer x, Integer y) -> {
            return y - x;
        });
    }
    
    public void addNum(int num) {
        if (small.size() == big.size()) {
            big.offer(num);
            small.offer(big.poll());
        } else {
            small.offer(num);
            big.offer(small.poll());
        }
    }
    
    public double findMedian() {
        if (big.size() == small.size()) {
            return (big.peek() + small.peek()) * 1.0 / 2; 
        } else {
            return small.peek();
        }
    }
}

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder obj = new MedianFinder();
 * obj.addNum(num);
 * double param_2 = obj.findMedian();
 */
```

