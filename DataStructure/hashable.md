    extension ListNode:Hashable{
         public var hashValue:Int{
             return ObjectIdentifier(self).hashValue
         }
         public static func == (lhs:ListNode, rhs:ListNode)->Bool{
             return lhs == rhs
         }
         public func hash(into hasher:inout Hasher){
             hasher.combine(ObjectIdentifier(self))
         }
    }
