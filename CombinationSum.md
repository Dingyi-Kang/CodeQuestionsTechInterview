## my solution which works -- only beat 17% in running time
### dynamic programming, binaryInsert
### But the bottleNeck of this solution is too many duplicates (it is just a improved version of brute force)
    class Solution {
        func combinationSum(_ candidates: [Int], _ target: Int) -> [[Int]] {

            var newSet = Set<[Int]>()

            for i in candidates{
                let newTarget = target - i

                if newTarget == 0{
                    newSet.insert([i])
                }

                else if newTarget < 2 {
                    continue
                }
                // >= 2
                else{
                    var arrs = combinationSum(candidates, newTarget)
                    //insert i into each arr of arrs
                    for k in 0..<arrs.count {
                        let j = binaryInsertIndex(0, arrs[k].count-1, arrs[k], i)
                        arrs[k].insert(i, at: j)
                        newSet.insert(arrs[k])
                    }
                }
            }
            return Array(newSet)
        }


        func binaryInsertIndex(_ l:Int, _ r:Int, _ arr:[Int], _ val: Int)->Int{

            if l > r {
                return l 
            } 

            let m = (l + r)/2

            if arr[m] == val {return m}
            else if arr[m] < val {
                return binaryInsertIndex(m+1, r, arr, val)
            }else{
                return binaryInsertIndex(l, m-1, arr, val)
            }

        }
    }
    
    
## quicker solution which I should learn something from it -- way of brancing recursive tree -- efficiently avoid duplicates
### BackTracking is fit for recursion
### Below is my solution based on the idea
#### At each recursion, branch into two cases -- using the first element of the candidates at least once in the combination(s) vs not using even once the first element of the candidates in the combination(s)

      class Solution {
          func combinationSum(_ candidates: [Int], _ target: Int) -> [[Int]] {

              if candidates.count == 0 {return []}

              var arrs = [[Int]]()

              let i = candidates[0]

              //the cases of using at least one i
              if i == target{
                  arrs.append([i])
              }
              else if target - i > 1 {
                  var lists = combinationSum(candidates, target - i)
                  for k in 0..<lists.count {
                      lists[k].insert(i, at: 0)
                      arrs.append(lists[k])
                  }
              }

              //the case of using not even one i
              var newC = candidates
              newC.removeFirst()
              arrs.append(contentsOf: combinationSum(newC, target))

              return arrs
          }
      }
