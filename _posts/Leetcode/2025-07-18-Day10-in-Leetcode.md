---
title: Day10 in Leetcode
date: 2025-07-18
categories: [Leetcode]
tags: [Leetcode, Algorithm]
---

# 232. 用栈实现队列
**一句话思路**：用两个栈，一个负责入队，一个负责出队，需要时将元素在两栈间倒腾
**模板**：
    stack<int> inStack, outStack;

    void in2out() {
        while (!inStack.empty()) {
            outStack.push(inStack.top());
            inStack.pop();
        }
    }

    MyQueue() {
        
    }
    
    void push(int x) {
        inStack.push(x);
    }
    
    int pop() {
        if (outStack.empty()) {
            in2out();
        }
        int x = outStack.top();
        outStack.pop();
        return x;
    }
    
    int peek() {
        if (outStack.empty()) {
            in2out();
        }
        return outStack.top();
    }
    
    bool empty() {
        return inStack.empty() && outStack.empty();
    }
**易错**：只有在输出栈为空时才从输入栈倒元素，避免顺序错乱；倒腾时要一次性全部倒完
**关键理解**：outStack不空时，新push的元素不会立即被pop，必须等outStack清空后才能轮到inStack中的元素
**类似题**：
225.用队列实现栈 - 双队列模拟栈
剑指Offer09.用两个栈实现队列 - 同样的思路

# 225. 用队列实现栈
**一句话思路**：用两个队列，每次pop时将前n-1个元素移到另一个队列，保留最后一个
**模板**：
    queue<int> queue1;
    queue<int> queue2;

    MyStack() {
        
    }
    
    void push(int x) {
        queue2.push(x);
        while (!queue1.empty()) {
            queue2.push(queue1.front());
            queue1.pop();
        }
        swap(queue1, queue2);
    }
    
    int pop() {
        int r = queue1.front();
        queue1.pop();
        return r;
    }
    
    int top() {
        int r = queue1.front();
        return r;
    }
    
    bool empty() {
        return queue1.empty();
    }
**易错**：每次pop后要清空辅助队列，保持只有一个队列有元素
**类似题**：
232.用栈实现队列 - 双栈模拟队列
剑指Offer30.包含min函数的栈 - 栈的变种实现

# 20. 有效的括号
**一句话思路**：用栈匹配，遇到左括号入栈对应右括号，遇到右括号检查是否与栈顶匹配
**模板**：
        stack<char> st;
        for (int i = 0; i < s.size(); i++) {
            if (s[i] == '(') st.push(')');
            else if (s[i] == '{') st.push('}');
            else if (s[i] == '[') st.push(']');
            else if (st.empty() || st.top() != s[i]) return false;
            else st.pop();
        }
        return st.empty();
**易错**：注意栈为空时直接返回false，最后要检查栈是否为空
**类似题**：
1047.删除字符串中的所有相邻重复项 - 也是用栈匹配
22.括号生成 - 括号相关的递归问题

# 1047. 删除字符串中的所有相邻重复项
**一句话思路**：用栈或字符串模拟栈，遇到相同字符就消除，否则加入
**模板**：
        string result;
        for (char s : S) {
            if (result.empty() || result.back() != s) {
                result.push_back(s);
            } else {
                result.pop_back();
            }
        }
        return result;
**易错**：检查栈顶前要先判断栈是否为空
**类似题**：
20.有效的括号 - 同样是栈的匹配消除思想
1209.删除字符串中的所有相邻重复项II - 升级版，删除k个重复 