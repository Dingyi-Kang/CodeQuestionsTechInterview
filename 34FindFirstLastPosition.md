## my solution which works
    class Solution {
        func searchRange(_ nums: [Int], _ target: Int) -> [Int] {
            if nums.count == 1 && nums[0] == target { return [0, 0]}

            let (f, s) = binarySearch(0, nums.count-1, nums, target)
            return [f, s]
        }


        func binarySearch(_ l:Int, _ r:Int, _ nums:[Int], _ target: Int) -> (Int, Int){

            if l > r {return (-1, -1)}

            let m = (l + r)/2

            if nums[m] == target{
                var st = m
                var ed = m

                while (st - 1 >= 0 && nums[st - 1] == target) {
                        st = st - 1
                }

                while (ed + 1 < nums.count && nums[ed + 1] == target){
                        ed = ed + 1
                }
                return (st, ed)
            }
            else if nums[m] > target{
                return binarySearch(l, m-1, nums, target)
            }
            else{
                return binarySearch(m+1, r, nums, target)
            }

        }
    }
