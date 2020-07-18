#### 单链表反转

#### 链表中环的检测

#### 两个有序的链表合并

#### 删除链表倒数第 n 个结点

#### 求链表的中间结点



#### 实现

```python
# -*- coding: utf-8 -*-

# 单链表反转
# 链表中环的检测
# 将两个升序链表合并为一个新的 升序 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。示例：输入：1->2->4, 1->3->4 输出：1->1->2->3->4->4
# 给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头结点。
# 求链表的中间结点


class LinkNode(object):
    """
    单链表节点
    """

    def __init__(self, value):
        self.value = value  # 存储的值
        self._next = None

    @property
    def next(self):
        return self._next

    @next.setter
    def next(self, link_node):
        if link_node is None:
            self._next = None
        elif not isinstance(link_node, LinkNode):
            raise Exception("必须是LinkNode节点对象")
        else:
            self._next = link_node


class Link(object):
    """
    单链表
    """
    @staticmethod
    def create_link(num, is_cycle=False):
        """
        创建单链表
        :param num:
        :return:
        """

        head = LinkNode(1)
        if num == 1:
            return head
        elif num <= 0:
            raise Exception("num 必须大于等于1")
        else:
            temp = head
            next = None
            for i in range(2, num + 1):
                next = LinkNode(i)
                temp.next = next
                temp = next
            next.next = None if not is_cycle else head
            return head

    @staticmethod
    def print_link(head):
        """
        打印单链表
        :param link_node:
        :return:
        """
        while head:
            print(head.value, end=" ")
            head = head.next
        print("")


class LinkHandle(object):
    """
    链表处理
    """

    def reverse(self, head):
        """
        单链表反转
        :param link_node: 头结点
        :return: 反转后的头结点
        """
        prev = None
        while head:
            next = head.next
            head.next = prev
            prev = head
            head = next
        return prev

    def has_cycle(self, head):
        """
        中环检测
        :param link_node: 头节点
        :return: 是否是中环
        """
        fast, slow = head, head
        while fast and fast.next:
            fast = fast.next.next
            slow = slow.next
            if fast == slow:
                return True
        return False

    def find_middle_node(self, head):
        """
        求链表的中间节点
        :param head:
        :return:
        """
        fast, slow = head, head
        fast = fast.next if fast else None
        while fast and fast.next:
            fast = fast.next.next
            slow = slow.next
        return slow

    def merge_order_link(self, head1, head2):
        """
        将两个升序链表合并为一个新的 升序 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的
        :param head1:
        :param head2:
        :return:
        """
        head = LinkNode(0)
        temp = head
        while head1 or head2:
            if head1 and head2 and head1.value <= head2.value or not head2:
                temp.next = head1
                head1 = head1.next
            else:
                temp.next = head2
                head2 = head2.next
            temp = temp.next
        return head.next

    def remove_nth_from_end(self, head, n):
        """
        给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头结点。
        :param head:
        :param n:
        :return:
        """
        Node = LinkNode(None)
        Node.next = head
        fast, slow = Node, Node
        num = 0
        while fast.next:
            fast = fast.next
            if num == n:
                slow = slow.next
            else:
                num += 1
        slow.next = slow.next.next
        return Node.next



if __name__ == '__main__':
    link_handle = LinkHandle()
    head = Link.create_link(30)
    Link.print_link(head)
    head = link_handle.reverse(head)
    print("*" * 50)

    Link.print_link(head)
    print("*" * 50)

    head = Link.create_link(30, is_cycle=True)
    print(link_handle.has_cycle(head))
    print("*" * 50)

    head1 = LinkNode(1)
    head1_1 = LinkNode(2)
    head1_2 = LinkNode(4)
    head1.next = head1_1
    head1_1.next = head1_2
    head1_2.next = None
    head2 = LinkNode(1)
    head2_1 = LinkNode(3)
    head2_2 = LinkNode(4)
    head2.next = head2_1
    head2_1.next = head2_2
    head2_2.next = None
    head = link_handle.merge_order_link(head1, head2)
    Link.print_link(head)
    print("*" * 50)

    head = Link.create_link(2)
    Link.print_link(head)
    head = link_handle.remove_nth_from_end(head,2)
    Link.print_link(head)
```

