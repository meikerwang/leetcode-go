### 剑指 Offer 03. 数组中重复的数字


找出数组中重复的数字。


在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

示例 1：

输入：
[2, 3, 1, 0, 2, 5, 3]
输出：2 或 3 
 

限制：

2 <= n <= 100000

### 分析

1. 先排序,再看相邻元素是否相同,比较慢, O(nlog n), 空间O(1)
2. 哈希表, 时间O(n), 空间O(1)
3. 原地hash: 因为nums元素范围有限,可以使用原地排序,把位置为i的位置放置元素i



```go
func findRepeatNumber(nums []int) int {
    return find(nums)
}

// 原地交换
func find(nums []int) int {
    for i, _ := range nums {
        for nums[i] != i {
            if nums[i] == nums[nums[i]] {
                return nums[i]
            }
            nums[i], nums[nums[i]] = nums[nums[i]], nums[i]
        }
    }
    return -1
}

// hash存储
func find2(nums []int) int {
    numMap := make(map[int] bool)
    for _, val := range nums {
        if numMap[val] {
            return val
        } else {
            numMap[val] = true
        }
    }
    return -1
}

func find3(nums []int) int {
    numMap := make(map[int] int)
    for _, val := range nums {
        if _, exist := numMap[val]; exist {
            return val
        }
        numMap[val] = val
    }
    return -1
}
```