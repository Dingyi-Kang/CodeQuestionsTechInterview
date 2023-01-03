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
          
 
 
 ## two pointers
 
    //Runtime: 47 ms, faster than 35.83% of Java online submissions for 3Sum.
    //Memory Usage: 60.1 MB, less than 32.20% of Java online submissions for 3Sum.
    //Two pointers
    //Time: O(N * LogN + N * N); Space : O(N + LogN)
    public List<List<Integer>> threeSum(int[] nums) {
        Set<List<Integer>> resultSet = new HashSet();
        Arrays.sort(nums);

        for(int i = 0; i <= nums.length - 3 && nums[i] <= 0;){
            int left = i + 1, right = nums.length - 1;
            if (0 - nums[i] - nums[left] < 0) break;

            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];
                if (sum > 0) {
                    right--;
                    while (left < right && nums[right] == nums[right + 1]) right--; //skip duplicated number
                } else {
                    if (sum == 0) {
                        resultSet.add(Arrays.asList(nums[i], nums[left], nums[right]));
                        right--;
                        while (left < right && nums[right] == nums[right + 1]) right--;
                    }
                    left++;
                    while (left < right && nums[left] == nums[left - 1]) left++;
                }
            }
            i++;
            while(i < nums.length - 2 && nums[i] == nums[i - 1]) i++;
        }
        return new ArrayList<>(resultSet);
    }
