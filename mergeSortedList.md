## naive first attempt
### not concise -- it is more imperative way
    class Solution {
        func mergeTwoLists(_ list1: ListNode?, _ list2: ListNode?) -> ListNode? {

                if list1 == nil, list2 == nil{
                    return nil
                }
                else if list1 == nil{
                    return list2
                }else if list2 == nil{
                    return list1
                }

                var p1:ListNode? = list1!
                var p2:ListNode? = list2!
                let head:ListNode
                var currNode:ListNode

                if p1!.val < p2!.val {
                    head = p1!
                    currNode = head
                    p1 = p1!.next
                }else{
                    head = p2!
                    currNode = head
                    p2 = p2!.next
                }

                while(p1 != nil && p2 != nil){
                    if p1!.val <= p2!.val{
                        currNode.next = p1
                        currNode = currNode.next!
                        p1 = p1!.next
                    }else{
                        currNode.next = p2
                        currNode = currNode.next!
                        p2 = p2!.next
                    }
                }

                if p1 == nil{
                    currNode.next = p2
                }else{
                    currNode.next = p1
                }

                return head

        }
    }
    
### recursive solution -- functional programming
    class Solution {
        func mergeTwoLists(_ list1: ListNode?, _ list2: ListNode?) -> ListNode? {

                if list1 == nil{
                    return list2
                }else if list2 == nil{
                    return list1
                }

                let head:ListNode

                if (list1!.val < list2!.val){

                    head = list1!
                    head.next = mergeTwoLists(list1!.next, list2)

                }
                else{
                    head = list2!
                    head.next = mergeTwoLists(list1, list2!.next)
                }

                return head
        }
    }
