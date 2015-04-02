---
layout: post
title: "链表操作"
date: 2015-04-02 10:48:06 +0800
comments: true
categories: 
---
  链表本身很灵活，很考察编程功底，所以我将复习过程中比较好的链表问题整理了一下。本文用到的节点结构如下：  
  
	public class Node {
       public Node next;  
       public int value;
    }
1.在O(1)时间删除链表节点  
-----
**题目描述：**从无头单链表中删除节点，在O(1)时间删除该节点.  
  
**分析：**用下一个节点数据覆盖要删除的节点，然后删除下一个节点，删除的节点不能是尾节点.  
  
**代码如下：**　　
	  
      public void deleteRandomNode(Node cur) {
		if(cur == null)
			return;
		Node pNext = cur.next;
		if(pNext != null) {//其实这步判断是多余的，这个方法能用的前提就是删除的节点不能是尾节点
			cur.value = pNext.value;
			cur.next = pNext.next;
		}
	　　
２.单链表的转置  
----- 
**题目描述：**输入一个单向链表，输出逆序反转后的链表  
  
**分析：**用两个临时指针 n,newHead 在链表上循环一遍即可.  
  
**代码如下：**  
  
	public Node reverse(Node head) {
		if(head == null)
			return;
		Node n = null, newHead = null;
		while(head != null) {
			n = newHead;
			newHead = head;
			head = head.next;
			newHead.next = n;
		} 
		return newHead;
	}　　
3.求链表的中间节点  
-----
**题目描述：**求链表的中间节点，如果链表的长度为偶数，返回中间两个节点的任意一个，若为奇数，则返回中间节点。  
  
**分析：**用两个指针从链表头节点开始，一个指针每次向后移动两步，一个指针每次移动一步，直到快指针移到到尾节点，那么慢指针正好位于链表中间位置。  
  
**代码如下：**  
	
	public Node searchMiddle(Node head) {
		if(head == null || head.next == null)
			return head;
		Node p1, p2;
		p1 = p2 = head;
		while(p2.next != null && p2.next.next != null) {
			p1 = p1.next;
			p2 = p2.next.next;
		}
		return p1;
	}  
4.求链表倒数第k个节点  
----- 
**题目描述：**输入一个单向链表，输出该链表中倒数第k个节点，链表的倒数第0个节点为链表的尾指针。  
  
**分析：**设置两个指针 p1、p2，首先 p1 和 p2 都指向 head，然后 p2 向前走 k 步，这样 p1 和 p2 之间就间隔 k 个节点，最后 p1 和 p2 同时向前移动，直至 p2 走到链表末尾,p1就是所求的节点。  
  
**代码如下：**  
	
	public Node getKNode(Node head,int k) {
		if(k < 0)
			return null;
		Node p1 = head, p2 = head;
		while(k-- > 0 && p2 != null) {
			p2 = p2.next;
		}
		//大于链表的长度
		if(k > 0) 
			return null;
		while(p2 != null) {
			p1 = p1.next;
			p2 = p2.next;
		}
		return p1;
	}  
5.判断单链表是否存在环  
----- 
**题目描述：**输入一个单向链表，判断链表是否有环。  
  
**分析：**通过两个指针，分别从链表的头节点出发，一个每次向后移动一步，另一个移动两步，两个指针移动速度不一样，如果存在环，那么两个指针一定会在环里相遇。  
  
**代码如下：**  
	
	public boolean hasCircle(Node head) {
		if(head == null)
			return false;
		Node p1 = head,p2 = head;
		while(p2 != null && p2.next != null) {
			p1 = p1.next;
			p2 = p2.next.next;
			if(p1 == p2)
				return true;
		}
		return false;
	}  
6.找到环的入口点  
-----  
**题目描述：**输入一个单向链表，判断链表是否有环。如果链表存在环，如何找到环的入口点。  
  
**分析：**由上题可知，按照 p2 每次两步，p1 每次一步的方式走，发现 p2 和 p1 重合，确定了单向链表有环路了。接下来，让p2回到链表的头部，重新走，每次步长不是走2了，而是走1，那么当 p1 和 p2 再次相遇的时候，就是环路的入口了。  
  
**为什么？**  
假定起点到环入口点的距离为 a，p1 和 p2 的相交点M与环入口点的距离为b，环路的周长为L，当 p1 和 p2 第一次相遇的时候，假定 p1 走了 n 步。那么有：  
　　p1走的路径： `a+b ＝ n；`  
　　p2走的路径： `a+b+k*L = 2*n；` p2 比 p1 多走了k圈环路，总路程是p1的2倍  
　　根据上述公式可以得到 `k*L=a+b=n`显然，如果从相遇点M开始，p1 再走 n 步的话，还可以再回到相遇点，同时p2从头开始走的话，经过n步，也会达到相遇点M。  
　　显然在这个步骤当中 p1 和 p2 只有前 a 步走的路径不同，所以当 p1 和 p2 再次重合的时候，必然是在链表的环路入口点上。  
    
**代码如下：**  
	
	public Node findLoopPort(Node head) {
		if(head == null)
			return head;
		Node p1 = head,p2 = head;
		while(p2 != null && p2.next != null) {
			p1 = p1.next;
			p2 = p2.next.next;
			if(p1 == p2)
				break;
		}
		//不存在环
		if(p1 != p2) 
			return null;
		p2 = head;
		while(p1 != p2) {
			p1 = p1.next;
			p2 = p2.next;
		}
		return p2;
	}  
7.判断两个链表是否相交  
-----  
**题目描述：**给出两个单向链表的头指针（如下图所示），
!['题目'](/home/nanyang/Downloads/title.jpg)
比如h1、h2，判断这两个链表是否相交。这里为了简化问题，我们假设两个链表均不带环。  
  
**分析：**如果两个没有环的链表相交于某一节点,则最后一个节点一定是共有的,我们只要判断两个链表的尾指针是否相等。相等，则链表相交,不相等，则链表不相交。  
  
**代码如下：**  
	
	public boolean isIntersect(Node h1, Node h2) {
		if(h1 == null || h2 == null)
			return false;
		Node p1 = h1;
		while(p1.next != null) {
			p1 = p1.next;
		}
		Node p2 = h2;
		while(p2.next != null) {
			p2 = p2.next;
		}
		//判断尾节点是否相等
		return p1 == p2;
	}  
８.扩展：链表有环，如何判断相交  
-----
**题目描述：**上面的问题都是针对链表无环的，那么如果现在，链表是有环的呢?上面的方法还同样有效么？  
  
**分析：**如果有环且两个链表相交，则两个链表都有共同一个环，即环上的任意一个节点都存在于两个链表上。因此，就可以判断一链表上俩指针相遇的那个节点，在不在另一条链表上 .  
  
**代码如下：**  
	
	public boolean isIntersectWithLoop(Node h1, Node h2) {
		if(h1 == null || h2 == null)
			return false;
		Node p1 = findCircleNode(h1), p2 = findCircleNode(h2);
		//判断链表带不带环，并保存环内节点
		if(p1 == null)
			return false;//不带环，异常退出
		if(p2 == null)
			return false;//不带环，异常退出
		Node n = p2.next;
		//走了一圈
		while(n != p2) {
			if(n == p1)
				return true;
			n = n.next;
		}
		return false;
	}  
９.扩展：两链表相交的第一个公共节点  
-----
**题目描述：**如果两个无环单链表相交，怎么求出他们相交的第一个节点呢？  
  
**分析：**采用对齐的思想。计算两个链表的长度 L1 , L2，分别用两个指针 p1 , p2 指向两个链表的头，然后将较长链表的 p1（假设为 p1）向后移动`L2 - L1`个节点，然后再同时向后移动p1 , p2，直到 `p1 = p2`。相遇的点就是相交的第一个节点.  
  
**代码如下：**  
	
	public Node findIntersectNode(Node h1, Node h2) {
		int len1 = listLength(h1);
		int len2 = listLength(h2);
		if(len1 > len2) {
			for(int i=0; i<len1 - len2; ++i) {
				h1 = h1.next;
			}
		} else {
			for(int i=0; i<len2 - len1; ++i) {
				h2 = h2.next;
			}
		}
		while(h1 != null) {
			if(h1 == h2)
				return h1;
			h1 = h1.next;
			h2 = h2.next;
		}
		return null;
	}  