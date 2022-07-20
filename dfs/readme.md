说个有帮助的技巧：永远只想当前层的逻辑，不要把思路钻进下一层。写代码的时候就假设dfs函数内部已经写好了，进去下一层一定会产生正确的结果；你只管把当前层的逻辑写好，整个dfs函数就都是正确的



给定一棵二叉树的根节点 root ，请找出该二叉树中每一层的最大值。

 

示例1：
输入: root = [1,3,2,5,3,null,9]
输出: [1,3,9]
示例2：

输入: root = [1,2,3]
输出: [1,3]

提示：

二叉树的节点个数的范围是 [0,104]
-231 <= Node.val <= 231 - 1


/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */

func largestValues(root *TreeNode) []int {
    if root == nil {
        return nil
    }
    var que = []*TreeNode {root}
    var res []int
    for len(que) > 0 {
        var tmp []*TreeNode
        var curMax = math.MinInt32
        for _, t := range que {
            if t.Val > curMax {
                curMax = t.Val
            }
            if t.Left != nil {
                tmp = append(tmp, t.Left)
            }
            if t.Right != nil {
                tmp = append(tmp, t.Right)
            }
        }
        res = append(res, curMax)
        que = tmp
    }
    return res
}