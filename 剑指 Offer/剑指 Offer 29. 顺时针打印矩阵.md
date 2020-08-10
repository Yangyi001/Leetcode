**难度：简单**   

输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。

 

示例 1：
```
输入：matrix = [[1,2,3],[4,5,6],[7,8,9]]
输出：[1,2,3,6,9,8,7,4,5]
```
示例 2：
```
输入：matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
输出：[1,2,3,4,8,12,11,10,9,5,6,7]
```

限制：

- 0 <= matrix.length <= 100
- 0 <= matrix[i].length <= 100

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/shun-shi-zhen-da-yin-ju-zhen-lcof
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。    

**解题思路**    
本题实际上不难，注意转向和边界条件即可。    

**Python实现**    
```
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        if matrix == []:
            return []
        illegal = 'illegal'
        tern_dict = {'R':(0, 1), 'L':(0, -1), 'U':(-1, 0), 'D':(1, 0)}
        tern_tran = {'R':'D', 'L':'U', 'U':'R', 'D':'L'}
        mlong = len(matrix[0]) - 1
        mwide = len(matrix) - 1
        direction = 'R'
        res = [matrix[0][0]]
        matrix[0][0] = illegal
        location = [0, 0]
        while True:
            last_locate = location[:]
            go = tern_dict[direction]
            location = [location[0]+go[0], location[1]+go[1]]
            if location[0] < 0 or location[0] > mwide or location[1] < 0 or location[1] > mlong or matrix[location[0]][location[1]] == illegal:
                direction = tern_tran[direction]
                go = tern_dict[direction]
                location = [last_locate[0]+go[0], last_locate[1]+go[1]]
                if location[0] < 0 or location[0] > mwide or location[1] < 0 or location[1] > mlong or matrix[location[0]][location[1]] == illegal: break
            res.append(matrix[location[0]][location[1]])
            matrix[location[0]][location[1]] = illegal
        return res
```