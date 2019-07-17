```
import Foundation

/// Linked List Structure with recursive enumeration implimentation which conforms to sequence protocol.
indirect enum LinkedListNode<T> {
    case value(element: T, next: LinkedListNode<T>)
    case end
}

extension LinkedListNode: Sequence {
    func makeIterator() -> LinkedListIterator<T> {
        return LinkedListIterator(current: self)
    }
}

struct LinkedListIterator<T>: IteratorProtocol {
    var current: LinkedListNode<T>
    
    mutating func next() -> T? {
        switch current {
        case let .value(element, next):
            current = next
            return element
        case .end:
            return nil
        }
    }
}

/// Usage:
let list = LinkedListNode.value(element: "five", next: .value(element: "seven", next: .end))

/// Since we are conforming to Sequence, we now get  map(), filter(), forEach() etc.
list.forEach {
    print($0)
}
let fives = list.filter { $0 == "five" }
print(fives)

```