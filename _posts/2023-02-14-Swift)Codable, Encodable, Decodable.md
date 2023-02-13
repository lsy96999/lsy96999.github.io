---
layout: post
title:  "Swift) Cotable, Encodable, Decodable"
date:   2023-02-14 00:02:18 +0900
categories: swift
---
Codable, Encodable, Decodable은 JSON과 같은 외부표현식으로 변환하는 프로토콜이다.

JSON으로 예들들어서  
Encode란  
Swift Object -> JSON String 로 변환하는 작업이며  
Decode란  
JSON String -> Swift Object 로 변환하는 작업이다.  

특정 Swift Object에  
Encodable만 채택하면 encode만 할수 있고,  
Decodable만 책택하면 decode만 할수 있다.  

Codable은 Encodable과 Decodable을 합친 프로토콜이다.

JSON의 Key명과 struct의 프로퍼티명이 다른경우 CodingKey라는 프로토콜을 통해 맞춰줄수 있다.
ex) 카멜케이스와 스네이크 케이스의 네이밍룰 불일치

example
{% highlight swift %}

//Codable = Encodable + Decodable
struct Card: Encodable, Decodable{
    let name: String
    let level: Int
    let subName: String
    enum CodingKeys:String, CodingKey{
        case name
        case level
        case subName = "sub_name" //key 명을 맞춰준다.
    }
}
let card = Card(name: "star", level: 2, subName: "sub")
let encoder = JSONEncoder();
let data = try! encoder.encode(card);
print("\(String(data: data, encoding: .utf8))")
//Optional("{\"name\":\"star\",\"level\":2,\"sub_name\":\"sub\"}")

let decoder = JSONDecoder();
let data2 = try! decoder.decode(Card.self, from: data)
print(data2.name)//star
print(data2.level)//2
print(data2.subName)//sub


{% endhighlight %}