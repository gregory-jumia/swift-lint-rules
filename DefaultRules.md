# Enabled by Default

## Block Based KVO

Prefer the new block based KVO API with keypaths when using Swift 3.2 or later.

### Examples

Non Triggering Examples

```swift
let observer = foo.observe(\.value, options: [.new]) { (foo, change) in
   print(change.newValue)
}
```

Triggering Examples

```swift
class Foo: NSObject {
  override func observeValue(forKeyPath keyPath: String?, of object: Any?,
                             change: [NSKeyValueChangeKey : Any]?,
                             context: UnsafeMutableRawPointer?) {}
}
```
```swift
class Foo: NSObject {
  override func observeValue(forKeyPath keyPath: String?, of object: Any?,
                             change: Dictionary<NSKeyValueChangeKey, Any>?,
                             context: UnsafeMutableRawPointer?) {}
}
```

## Class Delegate Protocol

Delegate protocols should be class-only so they can be weakly referenced.

### Examples

Non Triggering Examples

```swift
protocol FooDelegate: class {}
```
```swift
protocol FooDelegate: AnyObject {}
```
```swift
protocol FooDelegate: NSObjectProtocol {}
```

Triggering Examples

```swift
protocol FooDelegate {}
```

## Closing Brace Spacing

Closing brace with closing parenthesis should not have any whitespaces in the middle.

### Examples

Non Triggering Examples

```swift
[].map({ })
```
```swift
[].map(
  { }
)
```

Triggering Examples

```swift
[].map({ } )
```
```swift
[].map({ }    )
```

## Closure Parameter Position

Closure parameters should be on the same line as opening brace.

### Examples

Non Triggering Examples

```swift
[1, 2].map { number in
 number + 1 
}
```
```swift
[1, 2].map { number -> Int in
 number + 1 
}
```
```swift
[1, 2].map { (number: Int) -> Int in
 number + 1 
}
```
```swift
[1, 2].map { [weak self] number in
 number + 1 
}
```
```swift
[1, 2].something(closure: { number in
 number + 1 
})
```

Triggering Examples

```swift
[1, 2].map {
 ↓number -> Int in
 number + 1 
}
```
```swift
[1, 2].map {
 (↓number: Int) -> Int in
 number + 1 
}
```
```swift
[1, 2].map {
 [weak self] ↓number in
 number + 1 
}
```

## Colon

Colons should be next to the identifier when specifying a type and next to the key in dictionary literals.

### Examples

Non Triggering Examples

```swift
let abc: Void
```
```swift
let abc: [Void: Void]
```
```swift
let abc = ["string:string": "string"]
```

Triggering Examples

```swift
let abc0:Void

let abc1:  Void

let abc2 :Void

let abc3 : Void
```
```swift
let abc0 = [Void:Void]()

let abc1 = [Void : Void]()

let abc2 = [Void:  Void]()
```

## Comma Spacing

There should be no space before and one after any comma.

### Examples

Non Triggering Examples

```swift
func abc(a: String, b: String) { }
```
```swift
enum a { case a, b, c }
```
```swift
func abc(
  a: String,
  bcd: String
) {
}
```

Triggering Examples

## Compiler Protocol Init

### Examples

Non Triggering Examples

Triggering Examples

## Control Statement

`if`, `for`, `guard`, `switch`, `while`, and `catch` statements shouldn't unnecessarily wrap their conditionals or arguments in parentheses.

### Examples

Non Triggering Examples

```swift
if condition { }

if (a, b) == (0, 1) { }

if (a || b) && (c || d) { }
```
```swift
for item in collection { }

for (key, value) in dictionary { }

for (index, value) in enumerate(array) { }
```

Triggering Examples

```swift
if(condition) { }

if (condition == endIndex) { }

if ((a || b) && (c || d)) { }
```
```swift
for (item in collection) { }

for (var index = 0; index < 42; index++) { }
```
```swift
guard (condition) else { return }
```

## Custom Rules

Create custom rules by providing a regex string. Optionally specify what syntax kinds to match against, the severity level, and what message to display.

## Cyclomatic Complexity

Complexity of function bodies should be limited.

### Examples

Non Triggering Examples

```swift
func f1() {
if true {
for _ in 1..5 { } }
if false { }
}
```
```swift
func f(code: Int) -> Int {switch code {
 case 0: fallthrough
case 0: return 1
case 0: return 1
case 0: return 1
case 0: return 1
case 0: return 1
case 0: return 1
case 0: return 1
case 0: return 1
default: return 1}}
```
```swift
func f1() {if true {}; if true {}; if true {}; if true {}; if true {}; if true {}
func f2() {
if true {}; if true {}; if true {}; if true {}; if true {}
}}
```

Triggering Examples

```swift
func f1() {
  if true {
    if true {
      if false {}
    }
  }
  if false {}
  let i = 0
  switch i {
  case 1: break
  case 2: break
  case 3: break
  case 4: break
 default: break
  }
  for _ in 1...5 {
    guard true else {
      return
    }
  }
}
```

## Deployment Target

Availability checks or attributes shouldn't be using older versions that are satisfied by the deployment target.

## Discarded Notification Center Observer

When registering for a notification using a block, the opaque observer that is returned should be stored so it can be removed later.

### Examples

Non Triggering Examples

```swift
let foo = nc.addObserver(forName: .NSSystemTimeZoneDidChange, object: nil, queue: nil) { }
```
```swift
func foo() -> Any {
   return nc.addObserver(forName: .NSSystemTimeZoneDidChange, object: nil, queue: nil, using: { })
}
```
```swift
var obs: [Any?] = []
obs.append(nc.addObserver(forName: .NSSystemTimeZoneDidChange, object: nil, queue: nil, using: { }))
```
```swift
var obs: [String: Any?] = []
obs["foo"] = nc.addObserver(forName: .NSSystemTimeZoneDidChange, object: nil, queue: nil, using: { })
```

Triggering Examples

```swift
nc.addObserver(forName: .NSSystemTimeZoneDidChange, object: nil, queue: nil) { }
```
```swift
@discardableResult func foo() -> Any {
  return nc.addObserver(forName: .NSSystemTimeZoneDidChange, object: nil, queue: nil, using: { })
}
```

## Discouraged Direct Initialization

Discouraged direct initialization of types that can be harmful.

### Examples

Non Triggering Examples

```swift
let foo = UIDevice.current
let bar = Bundle.main
```
```swift
let foo = Bundle(path: "bar")
let bar = Bundle(identifier: "bar")
```

Triggering Examples

```swift
UIDevice()
UIDevice.init()

Bundle()
Bundle.init()
```
```swift
let foo = UIDevice()
let bar = UIDevice.init()

let foo = Bundle()
let bar = Bundle.init()
```
```swift
let foo = bar(bundle: Bundle(), device: UIDevice())

let foo = bar(bundle: Bundle.init(), device: UIDevice.init())
```

## Duplicate Enum Cases

Enum can't contain multiple cases with the same name.

### Examples

Non Triggering Examples

```swift
enum PictureImport {
  case addImage(image: UIImage)
  case addData(data: Data)
}
```
```swift
enum A {
  case add(image: UIImage)
}
enum B {
  case add(image: UIImage)
}
```

Triggering Examples

```swift
enum PictureImport {
  case ↓add(image: UIImage)
  case addURL(url: URL)
  case ↓add(data: Data)
}
```

## Duplicate Imports

Imports should be unique.

## Dynamic Inline

Avoid using `dynamic` and `@inline(__always)` together.

## Empty Enum Arguments

Arguments can be omitted when matching enums with associated types if they are not used.

### Examples

Non Triggering Examples

```swift
switch foo {
  case .bar: break
}
```
```swift
switch foo {
  case .bar(let x): break
}
```
```swift
switch foo {
  case let .bar(x): break
}
```
```swift
switch (foo, bar) {
  case (_, _): break
}
```

Triggering Examples

```swift
switch foo {
    case .bar(): break
}
```
```swift
switch foo {
    case .bar(_), .bar2(_): break
}
```

## Empty Parameters

Prefer `() -> ` over `Void -> `.

### Examples

Non Triggering Examples

```swift
let abc: () -> Void = {}
```
```swift
func foo(completion: () -> Void)
```
```swift
func foo(completion: () thows -> Void)
```

Triggering Examples

```swift
let abc: (Void) -> Void = {}
```
```swift
func foo(completion: (Void) -> Void)
```
```swift
func foo(completion: (Void) throws -> Void)
```

## Empty Parentheses with Trailing Closure

### Examples

Non Triggering Examples

```swift
[1, 2].map { $0 + 1 }
```
```swift
[1, 2].map({ $0 + 1 })
```
```swift
[1, 2].reduce(0) { $0 + $1 }
```

Triggering Examples

```swift
[1, 2].map() { $0 + 1 }
```
```swift
[1, 2].map( ) { $0 + 1 }
```
```swift
[1, 2].map() { number in
 number + 1 
}
```

## File Line Length

Files should not span too many lines.

## For Where

`where` clauses are preferred over a single `if` inside a `for`.

### Examples

Non Triggering Examples

```swift
for user in users where user.id == 1 { }
```
```swift
for user in users {
  if let id = user.id { }
}
```
```swift
for user in users {
  if var id = user.id { }
}
```
```swift
for user in users {
  if user.id == 1 { } else { }
}
```
```swift
for user in users {
  if user.id == 1 {
  } else if user.id == 2 { }
}
```

Triggering Examples

```swift
for user in users {
  ↓if user.id == 1 { return true }
}
```

## Force Cast

Force casts should be avoided.

### Examples

Non Triggering Examples

```swift
NSNumber() as? Int
```

Triggering Examples

```swift
NSNumber() as! Int
```

## Force Try

Force tries should be avoided.

### Examples

Non Triggering Examples

```swift
func a() throws {}

do {
  try a()
} catch {}
```

Triggering Examples

```swift
func a() throws {}

try! a()
```

## Function Body Length

Functions bodies should not span too many lines.

## Function Parameter Count

Number of function parameters should be low. Default is maximum of 5.

## Generic Type Name

Generic type name should only contain alphanumeric characters, start with an uppercase character and span between 1 and 20 characters in length.

### Examples

Non Triggering Examples

```swift
func run(_ options: NoOptions<CommandantError<()>>) {}
```
```swift
func configureWith(data: Either<MessageThread, (project: Project, backing: Backing)>)
```

Triggering Examples

```swift
func foo<↓T_Foo>() {}
```
```swift
func foo<↓TTTTTTTTTTTTTTTTTTTTT>() {}
```
```swift
func foo<↓type>() {}
```
```swift
typealias StringDictionary<↓T_Foo> = Dictionary<String, T_Foo>
```

## Identifier Name

Identifier names should only contain alphanumeric characters and start with a lowercase character or should only contain capital letters. In an exception to the above, variable names may start with a capital letter when they are declared static and immutable. Variable names should not be too long or too short.

### Examples

Non Triggering Examples

```swift
let myLet = 0
```
```swift
var myVar = 0
```
```swift
private let _myLet = 0
```
```swift
class Abc { static let MyLet = 0 }
```
```swift
let XMLString: String? = nil
```

Triggering Examples

```swift
let MyLet = 0
```
```swift
let _myLet = 0
```
```swift
private let myLet_ = 0
```
```swift
let myExtremelyVeryVeryVeryVeryVeryVeryLongLet = 0
```
```swift
var myExtremelyVeryVeryVeryVeryVeryVeryLongVar = 0
```
```swift
private let _myExtremelyVeryVeryVeryVeryVeryVeryLongLet = 0
```
```swift
let i = 0
```

## Implicit Getter

Computed read-only properties and subscripts should avoid using the get keyword.

### Examples

Non Triggering Examples

```swift
class Foo {
    subscript(i: Int) -> Int {
        get { return 3 }
        set { _abc = newValue }
    }
}
```
```swift
protocol Foo {
    subscript(i: Int) -> Int { get }
}
```

Triggering Examples

```swift
class Foo {
    var foo: Int {
        get{ return 20 }
    }
}
```
```swift
class Foo {
    static var foo: Int {
        get {
            return 20
        }
    }
}
```

## Inert Defer

If defer is at the end of its parent scope, it will be executed right where it is anyway.

### Examples

Non Triggering Examples

```swift
func example3() {
  defer { /* deferred code */ }
  print("other code")
}
```
```swift
func example4() {
  if condition {
    defer { /* deferred code */ }
    print("other code")
  }
}
```

Triggering Examples

```swift
func example3() {
  print("other code")
  defer { /* deferred code */ }
}
```
```swift
func example4() {
  if condition {
    defer { /* deferred code */ }
    // comment
  }
}
```

## Is Disjoint

Prefer using `Set.isDisjoint(with:)` over `Set.intersection(_:).isEmpty`.

### Examples

Non Triggering Examples

```swift
let isObjc = !objcAttributes.isDisjoint(with: dictionary.enclosedSwiftAttributes)
```
```swift
_ = Set(syntaxKinds).intersection(commentAndStringKindsSet)
```

Triggering Examples

```swift
_ = Set(syntaxKinds).↓intersection(commentAndStringKindsSet).isEmpty
```
```swift
let isObjc = !objcAttributes.↓intersection(dictionary.enclosedSwiftAttributes).isEmpty
```

## Large Tuple

Tuples shouldn't have too many members. Create a custom type instead. Default is maximum of 2.

### Examples

Triggering Examples

```swift
↓let foo: (Int, Int, Int)
```
```swift
let foo: (start: Int, end: Int, value: String)
```
```swift
func foo(bar: (Int, Int, Int))
```
```swift
func foo() -> (Int, Int, Int)
```

## Leading Whitespace

Files should not contain leading whitespace.

## Legacy CGGeometry Functions

Struct extension properties and methods are preferred over legacy functions

### Examples

Non Triggering Examples

```swift
rect.width
rect.maxX
rect.isNull
rect1.intersect(rect2)
```

Triggering Examples

```swift
CGRectGetWidth(rect)
CGRectGetMaxX(rect)
CGRectIsNull(rect)
CGRectIntersection(rect1, rect2)
```

## Legacy Constant

Struct-scoped constants are preferred over legacy global constants.

### Examples

Non Triggering Examples

```swift
CGRect.infinite
CGPoint.zero
CGSize.zero
CGRect.null
```
```swift
CGFloat.pi
Float.pi
```

Triggering Examples

```swift
CGRectInfinite
CGPointZero
CGSizeZero
CGRectNull
```
```swift
CGFloat(M_PI)
Float(M_PI)
```

## Legacy Constructor

Swift constructors are preferred over legacy convenience functions.

### Examples

Non Triggering Examples

```swift
CGPoint(x: 10, y: 10)
UIEdgeInsets(top: 0, left: 0, bottom: 10, right: 10)
```

Triggering Examples

```swift
CGPointMake(10, 10)
UIEdgeInsetsMake(0, 0, 10, 10)
```

## Legacy Hashing

Prefer using the `hash(into:)` function instead of overriding `hashValue`. Protocol: `Hashable`.

## Legacy NSGeometry Functions

Struct extension properties and methods are preferred over legacy functions. Similar to [Legacy CGGeometry Functions](#legacy-cggeometry-functions).

## Line Length

Lines should not span too many characters. Default is maximum of 120 characters.

## Mark

MARK comment should be in valid format. e.g. `'// MARK: ...'` or `'// MARK: - ...'`.

### Examples

Non Triggering Examples

```swift
// MARK: good
```
```swift
// MARK: - good
```
```swift
// MARK: -
```

Triggering Examples

```swift
//MARK: bad
```
```swift
// MARK:bad
```
```swift
//MARK:bad
```
```swift
//  MARK: bad
```

## Multiple Closures with Trailing Closure

Trailing closure syntax should not be used when passing more than one closure argument.

### Examples

Non Triggering Examples

```swift
foo.reduce(0) { $0 + $1 }
```
```swift
if let foo = bar.map({ $0 + 1 }) {
}
```
```swift
foo.something(param1: { $0 }, param2: { $0 + 1 })
```

Triggering Examples

```swift
foo.something(param1: { $0 }) { $0 + 1 }
```
```swift
UIView.animate(withDuration: 1.0, animations: {
    someView.alpha = 0.0
}) { _ in
    someView.removeFromSuperview()
}
```

## Nesting

Types should be nested at most 1 level deep, and statements should be nested at most 5 levels deep.

### Examples

Non Triggering Examples

```swift
class Class0 { class Class1 {} }
```
```swift
func func0() {
  func func1() {
    func func2() {
      func func3() {
        func func4() { 
          func func5() {}
        }
      }
    }
  }
}
```

Triggering Examples

```swift
class A { class B { class C {} } }
```
```swift
struct A { struct B { struct C {} } }
```
```swift
enum A { enum B { enum C {} } }
```
```swift
func func0() {
  func func1() {
    func func2() {
      func func3() {
        func func4() { 
          func func5() {
            func func6() {}
          }
        }
      }
    }
  }
}
```

## No Fallthrough Only

Fallthroughs can only be used if the `case` contains at least one other statement.

### Examples

Non Triggering Examples

```swift
switch myvar {
case 1:
  var a = 1
  fallthrough
case 2:
  var a = 2
}
```
```swift
switch myvar {
case "a":
  var one = 1
  var two = 2
  fallthrough
case "b": /* comment */
  var three = 3
}
```

Triggering Examples

```swift
switch myvar {
case 1:
  var a = 2
case 2:
  fallthrough
case 3:
  var a = 3
}
```
```swift
switch myvar {
case 1: // comment
  fallthrough
}
```
```swift
switch myvar {
case 1: /* multi
  line
  comment */
  fallthrough
case 2:
  var a = 2
}
```

## No Space in Method Call

Don't add a space between the method name and the parentheses.

## Notification Center Detachment

An object should only remove itself as an observer in `deinit`.

### Examples

Non Triggering Examples

```swift
class Foo { 
  deinit {
    NotificationCenter.default.removeObserver(self)
  }
}
```
```swift
class Foo { 
  func bar() {
    NotificationCenter.default.removeObserver(otherObject)
  }
}
```

Triggering Examples

```swift
class Foo { 
  func bar() {
    NotificationCenter.default.removeObserver(self)
  }
}
```

## NSObject Prefer isEqual

NSObject subclasses should implement isEqual instead of ==.

### Examples

Non Triggering Examples

```swift
class AClass: NSObject {
}
```
```swift
@objc class AClass: SomeNSObjectSubclass {
}
```
```swift
class AClass: Equatable {
  static func ==(lhs: AClass, rhs: AClass) -> Bool {
    return true
  }
}
```
```swift
class AClass: NSObject {
  override func isEqual(_ object: Any?) -> Bool {
    return true
  }
}
```

Triggering Examples

```swift
class AClass: NSObject {
  static func ==(lhs: AClass, rhs: AClass) -> Bool {
    return false
  }
}
```
```swift
@objc class AClass: SomeOtherNSObjectSubclass {
  static func ==(lhs: AClass, rhs: AClass) -> Bool {
    return true
  }
}
```
```swift
class AClass: NSObject, Equatable {
  static func ==(lhs: AClass, rhs: AClass) -> Bool {
    return false
  }
}
```

## Opening Brace Spacing

Opening braces should be preceded by a single space and on the same line as the declaration.

### Examples

Non Triggering Examples

```swift
func abc() {
}
```
```swift
[].map() { $0 }
```
```swift
[].map({ })
```

Triggering Examples

```swift
func abc(){
}
```
```swift
func abc()
    { }
```
```swift
[].map(){ $0 }
```
```swift
[].map( { } )
```

## Operator Function Whitespace

Operators should be surrounded by a single whitespace when they are being used.

### Examples

Non Triggering Examples

```swift
let foo = 1 + 2
```
```swift
let foo = 1 > 2
```
```swift
let foo = !false
```
```swift
let range = 1...3
```
```swift
let range = 1 ... 3
```
```swift
let range = 1..<3
```

Triggering Examples

```swift
let foo = 1+2
```
```swift
let foo = 1   + 2
```
```swift
let foo = 1   +    2
```
```swift
let foo = 1 +    2
```
```swift
let foo=1 + 2
```

## Private over fileprivate

Prefer `private` over `fileprivate` declarations.

## Private Unit Test

Unit tests marked private are silently skipped.

## Protocol Property Accessors Order

When declaring properties in protocols, the order of accessors should be `get set`.

### Examples

Non Triggering Examples

```swift
protocol Foo {
  var bar: String { get set }
}
```
```swift
protocol Foo {
  var bar: String { get }
}
```
```swift
protocol Foo {
  var bar: String { set }
}
```

Triggering Examples

```swift
protocol Foo {
  var bar: String { set get }
}
```

## Reduce Boolean

Prefer using `.allSatisfy()` or `.contains()` over `reduce(true)` or `reduce(false)`.

## Redundant Discardable Let

Prefer `_ = foo()` over `let _ = foo()` when discarding a result from a function.

## Redundant @objc Attribute

Objective-C attribute (@objc) is redundant in declaration.

### Examples

Non Triggering Examples

```swift
@IBDesignable
extension Foo {
  @objc
  var bar: Int { return 0 }
  var fooBar: Int { return 1 }
}
```
```swift
@objcMembers
class Foo: NSObject {
  @objc
  private var bar: Int {
    return 0
  }
}
```
```swift
@objcMembers
class Foo {
  class Bar: NSObject {
    @objc var foo: Any
  }
}
```

Triggering Examples

```swift
@IBInspectable @objc private var foo: String? {}
```
```swift
@objc @IBAction private func foo(_ sender: Any) {}
```

## Redundant Optional Initialization

Initializing an optional variable with `nil` is redundant.

## Redundant Set Access Control Rule

Property setter access level shouldn't be explicit if it's the same as the variable access level.

### Examples

Non Triggering Examples

```swift
private(set) public var foo: Int
```
```swift
private final class A {
  private(set) var value: Int
}
```

Triggering Examples

```swift
fileprivate(set) fileprivate var foo: Int
```
```swift
class A {
  internal(set) var value: Int
}
```
```swift
fileprivate class A {
  fileprivate(set) var value: Int
}
```

## Redundant String Enum Value

String enum values can be omitted when they are equal to the enumcase name.

### Examples

Triggering Examples

```swift
enum Numbers: String {
  case one = ↓"one"
  case two = ↓"two"
}
```
```swift
enum Numbers: String {
  case one = ↓"one", two = ↓"two"
}
```
```swift
enum Numbers: String {
  case one, two = ↓"two"
}
```

## Redundant Void Return

Returning Void in a function declaration is redundant.

## Returning Whitespace

Return arrow and return type should be separated by a single space or on a separate line.

### Examples

Non Triggering Examples

```swift
func abc() -> Int {}
```
```swift
var abc = {(param: Int) -> Void in }
```
```swift
func abc() ->
    Int {}
```
```swift
func abc()
    -> Int {}
```

Triggering Examples

```swift
func abc()->Int {}
```
```swift
var abc = {(param: Int)->Bool in }
```

## Shorthand Operator

Prefer shorthand operators (+=, -=, *=, /=) over doing the operation and assigning.

## Statement Position

Else and catch should be on the same line, one space after the previous declaration.

### Examples

Non Triggering Examples

```swift
} else if {
```
```swift
} else {
```
```swift
} catch {
```
```swift
"}else{"
```

Triggering Examples

```swift
}else if {
```
```swift
}  else {
```
```swift
}
catch {
```
```swift
}
      catch {
```

## Superfluous Disable Command

SwiftLint 'disable' commands are superfluous when the disabled rule would not have triggered a violation in the disabled region. Use " - " if you wish to document a command.

## Switch and Case Statement Alignment

Case statements should vertically align with their enclosing switch statement, or indented if configured otherwise.

### Examples

Non Triggering Examples

```swift
switch someBool {
case true:
  print("red")
case false:
  print("blue")
}
```

Triggering Examples

```swift
switch someBool {
  case true:
    print("red")
  case false:
    print("blue")
}
```

## Syntactic Sugar

Shorthand syntactic sugar should be used, i.e. `[Int]` instead of `Array<Int>`.

### Examples

Non Triggering Examples

```swift
let x: [Int]
```
```swift
let x: [Int: String]
```
```swift
let x: Int?
```
```swift
let x: Int!
```

Triggering Examples

```swift
let x: Array<String>
```
```swift
let x: Dictionary<Int, String>
```
```swift
let x: Optional<Int>
```
```swift
let x: ImplicitlyUnwrappedOptional<Int>
```


## Todo

TODOs and FIXMEs should be resolved.

## Trailing Comma

Trailing commas in arrays and dictionaries should be avoided/enforced.

## Trailing Newline

Files should have a single trailing newline.

### Examples

Non Triggering Examples

```swift
let a = 0

```

Triggering Examples

```swift
let a = 0
```
```swift
let a = 0


```

## Trailing Semicolon

Lines should not have trailing semicolons.

## Trailing Whitespace

Lines should not have trailing whitespace.

## Type Body Length

Type bodies should not span too many lines.

## Type Name

Type name should only contain alphanumeric characters, start with an uppercase character and span between 3 and 40 characters in length.

## Unneeded Break in Switch

Avoid using unneeded `break` statements.

### Examples

Non Triggering Examples

```swift
switch foo {
default:
  break
}
```
```swift
switch foo {
case .bar:
  for i in [0, 1, 2] { break }
}
```

Triggering Examples

```swift
switch foo {
case .bar:
  something()
  break // comment
}
```

## Unused Capture List

Unused reference in a capture list should be removed.

### Examples

Non Triggering Examples

```swift
[1, 2].map { [weak self] num in
  self?.handle(num)
}
```
```swift
let failure: Failure = { [weak self, unowned delegate = self.delegate!] foo in
  delegate.handle(foo, self)
}
```

Triggering Examples

```swift
[1, 2].map { [weak self] num in
  print(num)
}
```
```swift
let failure: Failure = { [weak self, unowned delegate = self.delegate!] foo in
  self?.handle(foo)
}
```

## Unused Closure Parameter

Unused parameter in a closure should be replaced with `_`.

### Examples

Non Triggering Examples

```swift
[1, 2].map { number in
  number + 1 
}
```
```swift
[1, 2].map { _ in
  3 
}
```
```swift
[1, 2].something { number, idx in
  return number * idx
}
```

Triggering Examples

```swift
[1, 2].map { number in
  return 3 // number
}
```
```swift
[1, 2].something { number, idx in
  return number
}
```

## Unused Control Flow Label

Unused control flow label should be removed.

## Unused Enumerated

When the index or the item is not used, `.enumerated()` can be removed.

## Unused Optional Binding

Prefer `!= nil` over `let _ =`.

### Examples

Non Triggering Examples

```swift
if let bar = Foo.optionalValue {
}
```
```swift
if let (_, second) = getOptionalTuple() {
}
```
```swift
if let (_, asd, _) = getOptionalTuple(), let bar = Foo.optionalValue {
}
```

Triggering Examples

```swift
if let _ = Foo.optionalValue {
}
```
```swift
if let a = Foo.optionalValue, let _ = Foo.optionalValue2 {
}
```

## Unused Setter Value

Setter value is not used.

### Examples

Non Triggering Examples

```swift
var aValue: String {
  get {
    return Persister.shared.aValue
  }
  set {
    Persister.shared.aValue = newValue
  }
}
```
```swift
var aValue: String {
  get {
    return Persister.shared.aValue
  }
  set(value) {
    Persister.shared.aValue = value
  }
}
```

Triggering Examples

```swift
var aValue: String {
  get {
    return Persister.shared.aValue
  }
  set {
    Persister.shared.aValue = aValue
  }
}
```
```swift
var aValue: String {
  get {
    return Persister.shared.aValue
  }
  set(value) {
    Persister.shared.aValue = aValue
  }
}
```

## Valid IBInspectable

`@IBInspectable` should be applied to variables only, have its type explicit and be of a supported type.

### Examples

Non Triggering Examples

```swift
class Foo {
  @IBInspectable private var x: Int
}
```
```swift
class Foo {
  @IBInspectable private var x: String?
}
```
```swift
class Foo {
  @IBInspectable private var x: String!
}
```
```swift
class Foo {
  @IBInspectable private var count: Int = 0
}
```

Triggering Examples

```swift
class Foo {
  @IBInspectable private let count: Int
}
```
```swift
class Foo {
  @IBInspectable private var insets: UIEdgeInsets
}
```
```swift
class Foo {
  @IBInspectable private var count = 0
}
```
```swift
class Foo {
  @IBInspectable private var count: Int?
}
```
```swift
class Foo {
  @IBInspectable private var count: Int!
}
```

## Vertical Parameter Alignment

Function parameters should be aligned vertically if they're in multiple lines in a declaration.

### Examples

Non Triggering Examples

```swift
func foo(bar: Int) { }
```
```swift
func validateFunction(_ file: SwiftLintFile, kind: SwiftDeclarationKind,
                      dictionary: SourceKittenDictionary) -> [StyleViolation] { }
```
```swift
func validateFunction(_ file: SwiftLintFile, kind: SwiftDeclarationKind,
                      dictionary: SourceKittenDictionary)
                      -> [StyleViolation] { }
```

Triggering Examples

```swift
func validateFunction(_ file: SwiftLintFile, kind: SwiftDeclarationKind,
                  dictionary: SourceKittenDictionary) { }
```
```swift
func validateFunction(_ file: SwiftLintFile, kind: SwiftDeclarationKind,
                       dictionary: SourceKittenDictionary) { }
```

## Vertical Whitespace

Limit vertical whitespace to a single empty line.

## Void Return

Prefer `-> Void` over `-> ()`.

### Examples

Non Triggering Examples

```swift
let abc: () -> Void = {}
```
```swift
let foo: (ConfigurationTests) -> () throws -> Void)
```

Triggering Examples

```swift
let abc: () -> ↓() = {}
```
```swift
let abc: () -> ↓(Void) = {}
```

## Weak Delegate

Delegates should be weak to avoid reference cycles.

### Examples

Non Triggering Examples

```swift
class Foo {
  weak var delegate: SomeProtocol?
}
```
```swift
class Foo {
  weak var someDelegate: SomeDelegateProtocol?
}
```
```swift
class Foo {
  weak var delegateScroll: ScrollDelegate?
}
```
```swift
class Foo {
  var scrollHandler: ScrollDelegate?
}
```
```swift
func foo() {
  var delegate: SomeDelegate
}
```
```swift
class Foo {
  var delegateNotified: Bool?
}
```
```swift
protocol P {
  var delegate: AnyObject? { get set }
}
```
```swift
class Foo {
  var computedDelegate: ComputedDelegate {
    return bar() 
  } 
}
```

Triggering Examples

```swift
class Foo {
  var delegate: SomeProtocol?
}
```
```swift
class Foo {
  var scrollDelegate: ScrollDelegate?
}
```

## XCTFail Message

An XCTFail call should include a description of the assertion.

### Examples

Non Triggering Examples

```swift
func testFoo() {
  XCTFail("bar")
}
```
```swift
func testFoo() {
  XCTFail(bar)
}
```

Triggering Examples

```swift
func testFoo() {
  XCTFail()
}
```
```swift
func testFoo() {
  XCTFail("")
}
```
