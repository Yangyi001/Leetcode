**难度：简单**   
用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )

 

示例 1：
```
输入：
["CQueue","appendTail","deleteHead","deleteHead"]
[[],[3],[],[]]
输出：[null,null,3,-1]
```
示例 2：
```
输入：
["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
[[],[],[5],[2],[],[]]
输出：[null,-1,null,null,5,2]
```
提示：

- 1 <= values <= 10000
- 最多会对 appendTail、deleteHead 进行 10000 次调用

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。     

**解题思路**    

该题目要求用两个栈实现，所以我们定义两个栈：主栈 和 辅助栈。    

当需要appendTail时，直接在 主栈后面添加元素即可，而当需要deleteHead时，我们应该取出主栈的栈底元素，此时若 辅助栈 为空，我们可以把 主栈 元素逐个弹出后加入 辅助栈 中， 辅助栈 的栈顶元素即为队头元素。     

**Python实现**   
```
class CQueue:

    def __init__(self):
        self.__stackone__ = []
        self.__stacktwo__ = []


    def appendTail(self, value: int) -> None:
        self.__stackone__.append(value)

    def deleteHead(self) -> int:
        if self.__stacktwo__ == []:
            while self.__stackone__:
                self.__stacktwo__.append(self.__stackone__.pop())
        return self.__stacktwo__.pop() if self.__stacktwo__ else -1
```