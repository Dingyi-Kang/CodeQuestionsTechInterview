This is my naive solution which didn't work due to the huge memory space

      /**
       * Definition for singly-linked list.
       * public class ListNode {
       *     public var val: Int
       *     public var next: ListNode?
       *     public init() { self.val = 0; self.next = nil; }
       *     public init(_ val: Int) { self.val = val; self.next = nil; }
       *     public init(_ val: Int, _ next: ListNode?) { self.val = val; self.next = next; }
       * }
       */
      class Solution {
          func removeNthFromEnd(_ head: ListNode?, _ n: Int) -> ListNode? {

              var dict:[Int:ListNode] = [:]

              guard let head = head else{return nil}

              var currNode = head
              var i = 0
              dict[i] = currNode
              while(currNode.next != nil){
                  currNode = currNode.next!
                  i += 1
                  dict[i] = currNode
              }

              if i == 0{
                  return nil
              }

              let removedNodeIndex = i - n + 1

              let prevNode = dict[removedNodeIndex-1]!
              prevNode.next = dict[removedNodeIndex]!.next

              return dict[0]
          }
      }
      
      
  
