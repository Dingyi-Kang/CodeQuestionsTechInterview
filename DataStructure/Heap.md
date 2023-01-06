great link: https://medium.com/devslopes-blog/swift-data-structures-heap-e3fbbdaa3129
<img width="704" alt="image" src="https://user-images.githubusercontent.com/81428296/210898849-39f2c85a-f595-4fe2-855b-bea3e094876c.png">

<img width="712" alt="image" src="https://user-images.githubusercontent.com/81428296/210898537-fc842d05-ed6f-4a61-a8dc-f6f536704714.png">


    struct MinHeap {
    var items: [Int] = []
    
    //Get Index
    private func getLeftChildIndex(_ parentIndex: Int) -> Int {
        return 2 * parentIndex + 1
    }
    private func getRightChildIndex(_ parentIndex: Int) -> Int {
        return 2 * parentIndex + 2
    }
    private func getParentIndex(_ childIndex: Int) -> Int {
        return (childIndex - 1) / 2
    }
    
    // Boolean Check
    private func hasLeftChild(_ index: Int) -> Bool {
        return getLeftChildIndex(index) < items.count
    }
    private func hasRightChild(_ index: Int) -> Bool {
        return getRightChildIndex(index) < items.count
    }
    private func hasParent(_ index: Int) -> Bool {
        return getParentIndex(index) >= 0
    }
    
    // Return Item From Heap
    private func leftChild(_ index: Int) -> Int {
        return items[getLeftChildIndex(index)]
    }
    private func rightChild(_ index: Int) -> Int {
        return items[getRightChildIndex(index)]
    }
    private func parent(_ index: Int) -> Int {
        return items[getParentIndex(index)]
    }
    
    mutating private func swap(indexOne: Int, indexTwo: Int) {
        let placeholder = items[indexOne]
        items[indexOne] = items[indexTwo]
        items[indexTwo] = placeholder
    }
    
    mutating private func heapifyDown() {
        var index = 0
        while hasLeftChild(index) {
              var smallerChildIndex = getLeftChildIndex(index)
              if hasRightChild(index) && rightChild(index) < leftChild(index) {
                  smallerChildIndex = getRightChildIndex(index)
              }

              if items[index] < items[smallerChildIndex] {
                  break
              } else {
                  swap(indexOne: index, indexTwo: smallerChildIndex)
              }
              index = smallerChildIndex
        }
    }
    
    mutating private func heapifyUp() {
        var index = items.count - 1
        while hasParent(index) && parent(index) > items[index] {
              swap(indexOne: getParentIndex(index), indexTwo: index)
              index = getParentIndex(index)
        }
    }
    
    mutating public func poll() -> Int {
      if items.count != 0 {
          let item = items[0]
          items[0] = items[items.count - 1]
          heapifyDown()
          items.removeLast()
          return item
      } else {
          fatalError()
      }
    }
    
    mutating public func add(_ item: Int) {
        items.append(item)
        heapifyUp()
    }
    
    }
    
## my first attemp which is worse than above
## but the comment are good
## 1. why left/right/parent node is i*2 + 1, i*2+2, (i-1)%2 -- which is explained in the comment embedded in the code below
## 2. has extra functions to check if hasParent/Left/Right is more convenient since boolean is convenient than unwrapping nil
## 3. has extra functions to get node based on the index is also good
## 4. Swap function is very helpful
## 5. heapifyDown is most difficult for you
## !6. mutating prefix for all method which will change ???
## 7. don't forget poll and add method, and heapifyUp and heapifyDown are private
    struct MinHeap{

    private var items = [ListNode]()

    //note: we just need to get index instead of the node. We can get node easily once we get the index
    private func getLeftChild(_ parentIndex: Int) -> Int? {
        //the number of nodes in the tree/array till the left child of parent node is exactly double of the total nodes till the parent node
        //hence, number = 2 * (parentIndex + 1) and the index = 2 * (parentIndex + 1) - 1 = 2 * parentIndex + 1
        let i = 2 * parentIndex + 1
        return i < items.count ? items[i] :  nil
    }

    private func getRightChild(_ parentIndex: Int) -> Int? {
        let i = 2 * parentIndex + 2
        return i < items.count ? items[i] :  nil
    }

    private func getParent(_ childIndex: Int) -> Int?{
        //?????????
        //the number of Nodes till parent is the reminder of the number of nodes till any their child node divided by 2
        // for example -- 4, 5 --> 2 ; hence, the index = (i+1)%2 - 1 = (i-1) % 2 ==> 3, 4 --> 1
        if childIndex == 0 {return nil}
        else {return (childIndex-1)%2} 
    }

    private func heapifyUp(){

    }

    //this assume the child/children is/are heapified
    private func heapifyDown(){

        let left = getLeftChild(0)
        let right = getRightChild(0)

        if ..........

    }

    private func swap(_ firstIndex:Int, _ secondIndex:Int){
        let m = items[firstIndex]
        items[firstIndex] = items[secondIndex]
        items[secondIndex] = m
    }

    //some version of heap implementation may have peek()

    func poll() -> ListNode{
        if items.count > 0{
            let item = items[0]
    //???? cannot direclty remove top root. or the whole tree will be messy. put the last leave in the root, at least the tree is partial heap, need less work. Or, need to rebuild the heap
            items[0] = items[items.count-1]
            items.removeLast()
            heapifyDown()
            return item
        }
        else{
            fataError()
        }
    }

    func add(_ node: ListNode){
        items.append(node)
        heapifyUp()
    }

    }


## My second try succeeded and is customized for the problem
    struct MinHeap{
        private var items = [ListNode]()

        private func getLeftChildIndex(_ i:Int) -> Int{
            return 2*i+1
        }
        private func getRightChildIndex(_ i:Int) -> Int{
            return 2*i+2
        }
        private func getParentIndex(_ i:Int) -> Int{
            return (i-1)%2
        }
        private func hasLeftChild(_ i: Int) -> Bool{
            return 2*i+1 < items.count
        }
        private func hasRightChild(_ i: Int) -> Bool{
            return 2*i+2 < items.count
        }
        private func hasParent(_ i: Int) -> Bool{
            return (i-1)%2 >= 0
        }
        private func getLeftChildValue(_ i: Int) -> Int{
            return items[2*i+1].val
        }
        private func getRightChildValue(_ i: Int) -> Int{
            return items[2*i+2].val
        }
        private func getParentValue(_ i: Int) -> Int{
            return items[(i-1)%2].val
        }
        mutating private func swap(_ i:Int, _ j:Int){
            let m = items[i]
            items[j] = items[i]
            items[i] = m
        }
        mutating private func heapifyDown(){
            var currIndex = 0
            while hasLeftChild(currIndex){
                var smallerNodeIndex = getLeftChildIndex(currIndex)
                if hasRightChild(currIndex) && getRightChildValue(currIndex) < items[smallerNodeIndex].val {
                    smallerNodeIndex = getRightChildIndex(currIndex)
                }

                if items[currIndex].val < items[smallerNodeIndex].val{
                    break
                }else{
                    swap(currIndex, smallerNodeIndex)
                    currIndex = smallerNodeIndex
                }
            }
        }

        mutating private func heapifyUp(){
            var currIndex = items.count - 1
            while hasParent(currIndex) && items[currIndex].val < getParentValue(currIndex){
                    swap(currIndex, getParentIndex(currIndex))
                    currIndex = getParentIndex(currIndex)
            }
        }

        public mutating func poll(_ n: ListNode) -> ListNode?{
            if items.count > 0 {
                let n = items[0]
                //do nothign, if items.count == 1
                swap(0, items.count-1)
                items.removeLast()
                heapifyDown()
                return n
            }else{
                return nil
            }
        }

        public mutating func add(_ n: ListNode){
            items.append(n)
            heapifyUp()
        }
    }
