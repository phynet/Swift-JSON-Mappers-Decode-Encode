# Swift-JSON-Mappers-Decode-Encode
This is a collection of resources of different frameworks and libraries used to map (decode-encode-serialize) JSON's in Swift. I'm coping all descriptions from their original source.

## Unbox

From John Sundell as well, **Unbox** is an easy to use Swift JSON decoder (you can find the encoder above). 
Just make your JSON conform to a specific schema or completely change the way you write model code. It can be used on any model with ease.

https://github.com/JohnSundell/Unbox

Example taken from his repo:

A JSON data:

```Swift
    {
        "name": "John",
        "age": 27
    }
```

Which can be represented as:

```Swift
    struct User {
        let name: String
        let age: Int
    }
```

Apply to each property the Unboxable attribute 

```Swift
    extension User: Unboxable {
        init(unboxer: Unboxer) throws {
            self.name = try unboxer.unbox(key: "name")
            self.age = try unboxer.unbox(key: "age")
        }
    }
```

An later (decode) use as:

```Swift
    let user: User = try unbox(dictionary: dictionary)
```

Or 

```Swift
    let user: User = try unbox(data: data)
```



And a extension to use unbox with Alamo Fire: https://github.com/serejahh/UnboxedAlamofire

## Object Mapper


ObjectMapper is a framework written in Swift that makes it easy for you to convert your model objects (classes and structs) to and from JSON.

https://github.com/Hearst-DD/ObjectMapper

## Mapper

Mapper is a simple Swift library to convert JSON to strongly typed objects. One advantage to Mapper over some other libraries is you can have immutable properties

https://github.com/lyft/mapper

## SwiftyJSON

Perhaps the most used parser for Swift, and it's a little more verbose than the above ones.

https://github.com/SwiftyJSON/SwiftyJSON


## Marshal

They say that this library will help you write declarative, performant, error handled code using the power of Protocol Oriented Programming™. I believe them.

https://github.com/utahiosmac/Marshal


## Genome

This library looks promising, uses Node on top of ... it?

> Genome is built on top of Node as opposed to JSON directly. This makes it easy for Genome to work with any data type through little effort.

> All mapping operations are built as sugar on top of Node's core.

https://github.com/LoganWright/Genome



## Decodable

> Simple and strict, yet powerful object mapping made possible by Swift 2's error handling. Greatly inspired by Argo, but without a bizillion functional operators.

https://github.com/Anviking/Decodable

## Wrap

This repo from John Sundell helps you to encode JSON your structs or classes. 

https://github.com/JohnSundell/Wrap


Example copied from the repo:

```Swift
    struct User {
        let name: String
        let age: Int
    }

    let user = User(name: "John", age: 28)
```

Using wrap() you can now encode a User instance with one command:

```Swift
     let dictionary: [String : Any] = try wrap(user)
```

Which will produce the following Dictionary:

```Swift
    {
        "name": "John",
        "age": 28
    }
```


## Serpent

[Serpent](https://engineering.nodesagency.com/articles/iOS/Serpent-more-than-just-another-JSON-mapping-framework/)
 It's a JSON mapper that generates all the parser code from the property models in your app and viceversa.  Seems fast and efficent. But you must download also the [Model Builder](https://github.com/nodes-ios/ModelBoiler)

![Parsing](https://d1gwekl0pol55k.cloudfront.net/image/nstack/translate_values/modelboiler_QFktJAlXOv.gif)


## Freddy 

[Freddy](https://github.com/bignerdranch/Freddy) is yet another Framework to parse JSON created by **Big Nerd Ranch**. It has some benefits like:

- Type Safty: "...provides a type safe solution to parsing JSON in Swift. This means that the compiler helps you work with sending and receiving JSON in a way that helps to prevent runtime crashes."
- Idiomatic Solution: "...Takes advantage of Swift's generics, enumerations, and functional features."
- Error Information: "for mistakes that commonly occur while parsing JSON. If you subscript the JSON object with a key that is not present, you get an informative error. If your desired index is out of bounds, you get an informative error. If you try to convert a JSON value to the wrong type, you get a good error here too."
- [Wiki](https://github.com/bignerdranch/Freddy/wiki): Really important when using a library, or framework because you need information on how to use them. 

```json 
{
    "success": true,
    "people": [
        {
            "name": "Matt Mathias",
            "age": 32,
            "spouse": true
        },
        {
            "name": "Sergeant Pepper",
            "age": 25,
            "spouse": false
        }
    ],
    "jobs": [
        "teacher",
        "judge"
    ],
    "states": {
        "Georgia": [
            30301,
            30302,
            30303
        ],
        "Wisconsin": [
            53000,
            53001
        ]
 }
```

```swift
let data = getSomeData()
do {
    let json = try JSON(data: data)
    let success = try json.getBool(at: "success")
    // do something with `success`
} catch {
    // do something with the error
}
```

```swift
let data = getSomeData()
do {
    let json = try JSON(data: data)
    let georgiaZipCodes = try json.getArray(at: "states","Georgia")
    let firstPersonName = try json.getString(at: "people",0,"name")
} catch {
    // do something with the error
}
```
