## my first attemp -- using two pointer -- not bad
    class Solution {
        func swapPairs(_ head: ListNode?) -> ListNode? {

            if head == nil {return nil}

            var firstP = head
            var secondP = head!.next

            let newHead:ListNode
            if secondP == nil {return firstP}
            else{newHead = secondP!}


            var preFirstP:ListNode? = nil
            while secondP != nil{
                var nextP = secondP!.next

                preFirstP?.next = secondP!
                secondP!.next = firstP!
                preFirstP = firstP!

                firstP = nextP

                if firstP != nil{

                    secondP = firstP!.next
                }else{
                    preFirstP?.next = nil
                    break
                }
            }

            if firstP != nil{
                preFirstP?.next = firstP!
            }


            return newHead

        }
    }
    
## more elegant solution -- recursive
