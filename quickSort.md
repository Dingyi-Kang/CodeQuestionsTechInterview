### quickSort in Swift
### note the inout parameter 
### and return value of partition subprogram is not right edge of the low part but the pivot
    
    func quickSort(_ nums: inout [Int], low:Int, high:Int){

        if high - low <= 0{
            return 
        }

        let p = partition(&nums, l:low, r:high)
        quickSort(&nums, low:low, high:p-1)
        quickSort(&nums, low:p+1, high:high)


    }

    func partition(_ nums: inout [Int], l:Int, r:Int)->Int{

        let pivot = nums[r]
        var left = l-1

        for i in l...r{
            if nums[i] < pivot {
                left += 1
                (nums[left], nums[i]) = (nums[i], nums[left])
            }
        }

       (nums[left+1], nums[r]) = (pivot, nums[left+1])
       //return the positin of pivot instead of the right side of the low
       return left+1

    }
