## my first attempt -- naive method
### recursive -- compare O(k*n) time
      class Solution {
          func mergeKLists(_ lists: [ListNode?]) -> ListNode? { 

              var newLists = lists.filter{ $0 != nil}

              return getNextHead(&newLists)

          }

          func getNextHead(_ lists: inout [ListNode?]) -> ListNode?{
              if lists.isEmpty{
                  return nil
              }

              var head = lists[0]!
              var index = 0
              for i in 1..<lists.count {

                  if lists[i]!.val < head.val{
                      head = lists[i]!
                      index = i
                  }

              }

              lists.remove(at: index)
              if head.next != nil{
                  lists.append(head.next!)
              }

              head.next = getNextHead(&lists)
              return head
          }
      }
      
   
   ## soultion 2 -- using priority queue
   
   
   
   ## solution 3 -- using divide and conquer
   
   
