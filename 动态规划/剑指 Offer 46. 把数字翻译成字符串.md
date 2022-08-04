给定一个数字，我们按照如下规则把它翻译为字符串：0 翻译成 “a” ，1 翻译成 “b”，……，11 翻译成 “l”，……，25 翻译成 “z”。一个数字可能有多个翻译。请编程实现一个函数，用来计算一个数字有多少种不同的翻译方法。

 

示例 1:

输入: 12258
输出: 5
解释: 12258有5种不同的翻译，分别是"bccfi", "bwfi", "bczi", "mcfi"和"mzi"
 

提示：

0 <= num < 231


```go
func translateNum(num int) int {
    func translateNum(num int) int {
    var arr []int

    for num > 0 {
        y := num % 10
        arr = append(arr, y)
        num = num / 10
    }
    if len(arr) < 2 {
        return 1
    }
    i, j := 0, len(arr)-1
    for i < j {
        arr[i], arr[j] = arr[j], arr[i]
        i++
        j--
    }
    //fmt.Println(arr)
    dp := make([]int, len(arr)+1)
    dp[0] = 1
    dp[1] = 1
    for i = 2; i <= len(arr); i++ {
        t := (arr[i-2] * 10 + arr[i-1])
        if (arr[i-2] * 10 + arr[i-1]) < 26  && t >= 10 {
            dp[i] = dp[i-1] + dp[i-2]
        } else {
            dp[i] = dp[i-1]
        }
    }
    return dp[len(arr)]
}


//     1 2 2 5 8
//   0 0 0 
// 1 0 1 1
// 2 0 
// 2
// 5
// 8

// dp[i] = dp[i-1] + dp[i-2]

//   1 2 2 5 8

// 1 1 2 3 5 5


func translateNum(num int) int {
    var arr []int

    for num > 0 {
        y := num % 10
        arr = append(arr, y)
        num = num / 10
    }
    if len(arr) < 2 {
        return 1
    }
    i, j := 0, len(arr)-1
    for i < j {
        arr[i], arr[j] = arr[j], arr[i]
        i++
        j--
    }
    // fmt.Println(arr)
    a, b := 1, 1
    for i = 2; i <= len(arr); i++ {
        t := (arr[i-2] * 10 + arr[i-1])
        if t < 26  && t >= 10 {
            // x := a
            // b = a + b
            // a = x
            a, b = b, a+b
        } else {
            a, b = b, b
        }
    }
    return b
}


}
```