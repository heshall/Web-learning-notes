### 二分查找

**前置条件**

- 必须采用顺序存储结构。
- 必须按关键字大小有序排列

**时间复杂度**：O(logn)

```j
    // 二分查找法
    // 与中间值对比，判断查找值所在方向
    init (arr, l, r, target) {
      console.log(l, r)
      const mid = Math.floor((l + r) / 2)
      console.log('mid:', mid)
      if (l > r) {
        console.log('失败')
        return -1
      }
      if (target > arr[mid]) {
        console.log('取右')
        return this.init(arr, mid + 1, r, target)
      } else if (target < arr[mid]) {
        console.log('取左')
        return this.init(arr, l, mid - 1, target)
      } else if (target === arr[mid]) {
        console.log('找到元素' + arr[mid])
        return target
      }
    }
```

