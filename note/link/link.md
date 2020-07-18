#### 单链表反转

#### 链表中环的检测

#### 两个有序的链表合并

#### 删除链表倒数第 n 个结点

#### 求链表的中间结点



#### 实现

```python
# -*- coding: utf-8 -*-


class LinkNode(object):
    """
    单链表节点
    """

    def __init__(self, value):
        self.value = value  # 存储的值

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
    def create_link(num):
        """
        创建单链表
        :param num:
        :return:
        """
        link_node = LinkNode(1)
        temp = link_node
        next = None
        for i in range(2, num + 1):
            next = LinkNode(i)
            temp.next = next
            temp = next
        next.next = None
        return link_node

    @staticmethod
    def print_link(link_node):
        """
        打印单链表
        :param link_node:
        :return:
        """
        while link_node.next:
            print(link_node.value)
            link_node = link_node.next


class LinkHandle(object):
    """
    单链表处理
    """

    def reverse(self, link_node):
        while link_node.next:
            pass



if __name__ == '__main__':
    link_handle = LinkHandle()
    link_handle.reverse(Link.create_link(20))
```

