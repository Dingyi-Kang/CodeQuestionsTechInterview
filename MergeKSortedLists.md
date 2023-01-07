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
   
         class Solution {
          func mergeKLists(_ lists: [ListNode?]) -> ListNode? { 

              if lists.isEmpty {return nil}

              var pQue = Heap()

              for list in lists{
                  var l = list
                  while(l != nil){
                      pQue.add(l!.val)
                      l = l!.next
                  }
              }

              var headValue = pQue.poll()
              if headValue == nil {return nil}

              var headNode = ListNode(headValue!)
              var currNode = headNode
              var currNodeVal = pQue.poll()

              while(currNodeVal != nil){

                  let nextNode = ListNode(currNodeVal!)
                  currNode.next = nextNode
                  currNode = nextNode
                  currNodeVal = pQue.poll()
              }
              return headNode


          }
      }


      struct Heap {

          var items = [Int]()

          private func getLeftChildIndex(_ i :Int) -> Int{
              return 2*i+1
          }

          private func getRightChildIndex(_ i :Int) -> Int{
              return 2*i+2
          }

          private func getParentIndex(_ i :Int) -> Int{
              return (i-1)/2
          }

          private func hasLeftChild(_ i : Int) -> Bool{
              return 2*i+1 < items.count
          }

          private func hasRightChild(_ i : Int) -> Bool{
              return 2*i+2 < items.count
          }

          private func hasParent(_ i : Int) -> Bool{
              return (i-1)/2 >= 0
          }

          private func getLeftChild(_ i :Int) -> Int{
              return items[2*i+1]
          }

          private func getRightChild(_ i :Int) -> Int{
              return items[2*i+2]
          }

          private func getParent(_ i :Int) -> Int{
              return items[(i-1)/2]
          }

          mutating private func swap(_ i:Int, _ j:Int){
              let m = items[i]
              items[i] = items[j]
              items[j] = m
          }

          mutating private func heapifyDown(){
              if items.count == 0 {return}

              var currIndex = 0

              while hasLeftChild(currIndex){
                  var smallerIndex = getLeftChildIndex(currIndex)

                  if hasRightChild(currIndex) && getRightChild(currIndex) < items[smallerIndex]{
                      smallerIndex = getRightChildIndex(currIndex)
                  }

                  if items[smallerIndex] < items[currIndex]{
                      swap(smallerIndex, currIndex)
                      currIndex = smallerIndex
                  }else{ break }

              }

          }

          mutating private func heapifyUp(){
              var currIndex = items.count - 1 
              while hasParent(currIndex), items[currIndex] < getParent(currIndex) {
                  swap(currIndex, getParentIndex(currIndex))
                  currIndex = getParentIndex(currIndex)
              }
          }

          mutating public func poll()->Int?{
              if items.count == 0 {return nil}

              let head = items[0]
              swap(0, items.count-1)
              items.removeLast()
              heapifyDown()
              return head
          }

          mutating public func add(_ n:Int){
              items.append(n)
              heapifyUp()
          }

      }
   
   ## my solution 3 -- using QuickSort -- partition -- beat over 97% in time
         class Solution {
          func mergeKLists(_ lists: [ListNode?]) -> ListNode? { 

              if lists.isEmpty {return nil}

              var arr = [Int]()

              for list in lists{
                  if let list = list{
                      var l = list
                      arr.append(l.val)
                      while(l.next != nil){
                          l = l.next!
                          arr.append(l.val)
                      }
                  }
              }

              if arr.isEmpty {return nil}

              quickSort(0, arr.count-1, &arr)

              var head = ListNode(arr[0])

              if arr.count == 1 {return head}

              var curr = ListNode(arr[1])
              head.next = curr
              for i in 2..<arr.count{
                  let newNode = ListNode(arr[i])
                  curr.next = newNode
                  curr = newNode
              }

              return head
          }
   
   ## my solution 4 -- using divide and conquer -- most consie and efficient solution
   class Solution {
    func mergeKLists(_ lists: [ListNode?]) -> ListNode? { 
        
        if lists.isEmpty {return nil}

        return divide(0, lists.count-1, lists)
    }


    func divide(_ l:Int, _ r:Int, _ lists:[ListNode?])->ListNode?{
        if l > r {return nil}
        if l == r {return lists[l]}

        let med = (l+r)/2

        let h1 = divide(l, med, lists)
        let h2 = divide(med+1, r, lists)

        return merge(h1, h2)

    }

    func merge(_ l:ListNode?, _ r:ListNode?) -> ListNode?{

        if l == nil{return r}
        else if r == nil {return l}

        if l!.val < r!.val{
            l!.next = merge(l!.next, r)
            return l
        }else{
            r!.next = merge(l, r!.next)
            return r
        }

    }

   }
   
