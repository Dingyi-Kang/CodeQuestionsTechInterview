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
    }
    
