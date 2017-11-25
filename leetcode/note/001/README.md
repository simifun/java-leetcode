# [Two Sum](https://leetcode.com/problems/two-sum/description/)

Given an array of integers, return indices of the two numbers such that they add up to a specific target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.
Example:
Given nums = [2, 7, 11, 15], target = 9,
Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
</br>简单来说就是给出两数的和target和一个int数组，求数组中是否有满足两数和等于target的，返回其下标。
题目很简单，解出来很容易，比如Brute Force解法，直接两个for循环嵌套就ok了。参考：

<pre><code class="java">public int[] twoSum(int[] nums, int target) {
    for (int i = 0; i &lt; nums.length; i++) {
        for (int j = i + 1; j &lt; nums.length; j++) {
            if (nums[j] == target - nums[i]) {
                return new int[] { i, j };
            }
        }
    }/Users/sss/Coding/git/java-leetcode/leetcode/README.md
    throw new IllegalArgumentException("No two sum solution");
}
</code></pre>

空间复杂度O(1)，很好！时间复杂度O(n<sup>2</sup>)，好吧，这不是我们想看到的。有没有更高效的解法？
<br>如果我们经常使用hsah表的话，我们不难知道凡事是涉及到key值查找的话，考虑以下hash总是好的。这里给出一种思路：将数据元素遍历存入HashMap，存储方式为&lt;nums[i],i>，将值作为HashMap的key值传入（这样才能利用hash的方法快速找到该值）之后就是类似的遍历查找了。
<br>
代码如下:

<pre><code class="java">public int[] twoSum(int[] nums, int target) {
    Map&lt;Integer, Integer&gt; map = new HashMap&lt;&gt;();
    for (int i = 0; i &lt; nums.length; i++) {
        map.put(nums[i], i);
    }
    for (int i = 0; i &lt; nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement) &amp;&amp; map.get(complement) != i) {
            return new int[] { i, map.get(complement) };
        }
    }
    throw new IllegalArgumentException("No two sum solution");
}
</code></pre>

时间复杂度O(n)，nice！空间复杂度O(n)，涨了，没办法，拿空间换时间是常见的，但也是令人欣然接受的。那么这是最优解吗？有没有更优雅的方案？
<br>答案是有，只需要将上述第二种方法做一下改进，边插入边比较:<br>

<pre><code class="java">public int[] twoSum(int[] nums, int target) {
    Map&lt;Integer, Integer&gt; map = new HashMap&lt;&gt;();
    for (int i = 0; i &lt; nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement)) {
            return new int[] { map.get(complement), i };
        }
        map.put(nums[i], i);
    }
    throw new IllegalArgumentException("No two sum solution");
}
</code></pre>

时间复杂度O(n)，空间复杂度O(1)好了，不愧是最优解，很巧妙，值得琢磨。
</br>类似利用hash table降低时间复杂度的例子还有很多，比如：
2017-涂鸦工厂：<a href="http://https://github.com/simifun/java-leetcode/tree/master/leetcode/note/002">找最长不重复字串</a>
