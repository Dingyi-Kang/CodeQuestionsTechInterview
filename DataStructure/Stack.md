## this is my initial attempt 
## turned out that not necessary to create a struct of stack which in essence is array used in a certain way
## and there is a smarter way to iterate throught the character in string

      class Solution {
          func isValid(_ s: String) -> Bool {

              guard s.count % 2 == 0 else{return false}

              var stack = Stack()

              for i in 0..<s.count{
                  let c:Character = s[s.index(s.startIndex, offsetBy: i)]

                  if c == "(" || c == "{" || c == "[" {
                      stack.push(c)
                  }
                  else if c == ")" {
                      if let a = stack.pop(), a == "(" {
                          //do nothing
                      }else{ return false }
                  }
                  else if c == "}" {
                      if let a = stack.pop(), a == "{" {
                          //do nothing
                      }else{ return false }
                  }
                  else if c == "]" {
                      if let a = stack.pop(), a == "[" {
                          //do nothing
                      }else{ return false }
                  }
              }
              if stack.pop() == nil {
                  return true
              }else{
                  return false
              }

          }
      }


      struct Stack {

          private var items:[Character] = []

          mutating func push(_ a:Character){
              self.items.append(a)
          } 

          mutating func pop() -> Character?{
              if items.isEmpty {
                  return nil
              } else{
                  return items.removeLast()
              }
          }

      }
 
 
 ## improved version with "stack"
     class Solution {
        func isValid(_ s: String) -> Bool {

            guard s.count % 2 == 0 else{return false}

            var stack = [Character]()

            for c in s{

                if c == "(" || c == "{" || c == "[" {
                    stack.append(c)
                }
                else if c == ")" {
                    if stack.isEmpty{return false}
                    if stack.removeLast() != "(" {return false}
                }
                else if c == "}" {
                    if stack.isEmpty{return false}
                    if stack.removeLast() != "{" {return false}
                }
                else if c == "]" {
                    if stack.isEmpty{return false}
                    if stack.removeLast() != "[" {return false}
                }
            }
            if stack.isEmpty{
                return true
            }else{
                return false
            }

        }
    }

  
  ## Moreover, not necessary to use stack. We can use dict/hashTable instead
    func isValid(_ s: String) -> Bool {
             if s.count % 2 != 0 { return false }

             let dictionary: [Character: Character] = [")": "(","]" :"[","}" :"{"]
             let open: [Character] = ["(", "[", "{"]
             let close: [Character] = [")", "]", "}"]
             var openers: [Character] = [Character]()

             for character in s { 
                 if open.contains(character) { 
                     openers.append(character)
                 } else { 
                     if openers.last == dictionary[character] { 
                         openers.removeLast()
                     } else { 
                         return false
                     }
                 }
             }

             return openers.isEmpty
         }
  
   

