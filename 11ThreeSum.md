### old solution which works but exceeds the time
          class Solution {
              func threeSum(_ nums: [Int]) -> [[Int]] {
                  guard nums.count >= 3 else {return [[]]}

                  var numsNew = nums
                  quickSort(&numsNew, low:0, high:nums.count-1)
                  //print(numsNew)

                  var results = [[Int]]()
                  var prevI:Int? = nil
                  for i in 0..<numsNew.count{

                      if let prevI = prevI, numsNew[i] == prevI{
                          continue
                      }

                      var prevJ:Int? = nil
                      for j in (i+1)..<numsNew.count{
                          if let prevJ = prevJ, numsNew[j] == prevJ{
                              continue
                          }

                          var prevK:Int? = nil
                          for k in (j+1)..<numsNew.count{
                              if let prevK = prevK, numsNew[k] == prevK{
                                  continue
                              }
                              if numsNew[i] + numsNew[j] + numsNew[k] == 0 {
                                  results.append([numsNew[i], numsNew[j], numsNew[k]])
                              }
                              prevK = numsNew[k]
                          }

                          prevJ = numsNew[j]

                      }
                      prevI = numsNew[i]
                  }

                  return results
              }


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
          }
          
  
