# The reason why the string subscribt and other APIs are so complicated:
<img width="692" alt="image" src="https://user-images.githubusercontent.com/81428296/212445695-88d16ba9-81dc-4239-a750-8c66da254304.png">

## 0. link of offical document of string
https://docs.swift.org/swift-book/LanguageGuide/StringsAndCharacters.html

## 1. get the character at the certain index of string
<img width="792" alt="image" src="https://user-images.githubusercontent.com/81428296/210304139-b6a71c49-72e8-4e60-a2c2-8a40ccefdbf5.png">
<img width="748" alt="image" src="https://user-images.githubusercontent.com/81428296/210304204-7ef9f47d-bb4f-41c4-be60-a29bb2d33c29.png">

link: https://www.simpleswiftguide.com/get-character-from-string-using-its-index-in-swift/


## 2. if a string is defined as let, no matter what mutant operations you do on it (dropFirst, remove), it wont change. and there is no compile error!!

## 3. remove a character at certain index of the string
<img width="948" alt="image" src="https://user-images.githubusercontent.com/81428296/210304410-e06cf650-f24e-4448-b625-2819ce4e66f5.png">


## 4. there is no single quote in Swift
<img width="708" alt="image" src="https://user-images.githubusercontent.com/81428296/210304481-74fabd86-6913-425f-ac0b-e71097898809.png">
post link: https://stackoverflow.com/questions/31415242/single-quotes-with-characters-in-swift

<img width="684" alt="image" src="https://user-images.githubusercontent.com/81428296/210304521-a87837ac-5453-441b-9fe6-08cdbf1aaa93.png">

<img width="305" alt="image" src="https://user-images.githubusercontent.com/81428296/210305093-a49325af-870c-4aa9-99bf-2bd5b7b5705b.png">

## 5. replace a character or subString
### 5.1 if just replace a character at certain index, you use remove and then insert
    str.remove(at: index)
    str.insert(newC, at: index)
### 5.2 if you want to replace a subString
<img width="763" alt="image" src="https://user-images.githubusercontent.com/81428296/212445456-9c181062-d91f-4a56-a33f-98aa762cf4e0.png">
    
    let rs = str.index(str.startIndex, offsetBy: 3) // See how 3 is an Int
    let re = str.index(str.startIndex, offsetBy: 4) // See how 4 is an Int
    str.replaceSubrange(rs..<re, with: "B")
    
## 6. the syntax of split -- str.split(separator: "@")

## 7. the syntax of join -- str.joined(separator: "@")

## 8. need to cast the UInt8 to Int. They are in different types
<img width="781" alt="image" src="https://user-images.githubusercontent.com/81428296/212446655-00691e47-aada-4ec8-aa54-ade13c141d7a.png">
<img width="743" alt="image" src="https://user-images.githubusercontent.com/81428296/212446703-693e3f71-48e5-4e86-8729-b6c81fe5c60a.png">
<img width="763" alt="image" src="https://user-images.githubusercontent.com/81428296/212446758-2c1a36c0-47e1-48bf-bb33-b10af63e2c97.png">


