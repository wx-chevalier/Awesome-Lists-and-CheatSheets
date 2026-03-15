> Rust CheatSheet 是对于 Rust 学习/实践过程中的语法与技巧进行盘点，其属于 [Awesome CheatSheet](https://github.com/wx-chevalier/Awesome-CheatSheets/) 系列，致力于提升学习速度与研发效能，即可以将其当做速查手册，也可以作为轻量级的入门学习资料。本文参考了许多优秀的文章与代码示范，统一声明在了 [Awesome Rust List](https://github.com/wx-chevalier/Awesome-Lists)；如果希望深入了解某方面的内容，可以继续阅读[Rust-Notes](https://github.com/wx-chevalier/Rust-Notes)，或者前往 [rust-examples](https://github.com/wx-chevalier/rust-examples) 查看使用 Rust 解决常见的数据结构与算法、设计模式、业务功能方面的代码实现。

# Rust 语法速览、实践技巧与开源工具清单

Rust 是为工业应用而生，并不拘泥于遵循某个范式（Paradigm），笔者认为其最核心的特性为 Ownership 与 Lifetime；能够在没有 GC 与 Runtime 的情况下，防止近乎所有的段错误，并且保证线程安全(prevents nearly all segfaults, and guarantees thread safety)。Rust 为每个引用与指针设置了 Lifetime，对象则不允许在同一时间有两个和两个以上的可变引用，并且在编译阶段即进行了内存分配(栈或者堆)；Rust 还提供了 Closure 等函数式编程语言的特性、编译时多态(Compile-time Polymorphism)、衍生的错误处理机制、灵活的模块系统等。

对于 Rust 的语法速览可以参考本目录下的 [rust-snippets](./rust-snippets.rs)。

> [Cheats.rs](https://cheats.rs/)

# Hello World

```rs
fn main() {
    println!("Hello, world!");
}
```

| Example    | Explanation                                                                                                                           |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| `//`       | Line comment, use these to document code flow or _internals_.                                                                         |
| `///`      | Outer line **doc comment**, use these on types.                                                                                       |
| `//!`      | Inner line doc comment, mostly used at start of file to document module.                                                              |
| `/*...*/`  | Block comment.                                                                                                                        |
| `/**...*/` | Outer block doc comment.                                                                                                              |
| `/*!...*/` | Inner block doc comment.                                                                                                              |
| `rust ...` | In doc comments, include a [doc test](https://doc.rust-lang.org/rustdoc/documentation-tests.html) (doc code running on `cargo test`). |
| `#`        | In doc tests, hide line from documentation (`# use x::hidden;`).                                                                      |

## Variables

通过关键字定义的数据类型和存储位置。

| Example                       | Explanation                                                                                                                                                      |
| ----------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `struct S {}`                 | Define a **struct** with named fields.                                                                                                                           |
| `struct S { x: T }`           | Define struct with named field `x` of type `T`.                                                                                                                  |
| `struct S` `(T);`             | Define "tupled" struct with numbered field `.0` of type `T`.                                                                                                     |
| `struct S;`                   | Define **zero sized** unit struct. Occupies no space, optimized away.                                                                                            |
| `enum E {}`                   | Define an **enum**, _c_. [algebraic data types](https://en.wikipedia.org/wiki/Algebraic_data_type), [tagged unions](https://en.wikipedia.org/wiki/Tagged_union). |
| ` enum E { A, B``(), C {} } ` | Define variants of enum; can be unit- `A`, tuple- `B` `()` and struct-like `C{}`.                                                                                |
| `enum E { A = 1 }`            | If variants are only unit-like, allow discriminant values, e.g., for FFI.                                                                                        |
| `union U {}`                  | Unsafe C-like **union** for FFI compatibility.                                                                                                                   |
| `static X: T = T();`          | **Global variable** with `'static` lifetime, single memory location.                                                                                             |
| `const X: T = T();`           | Defines **constant** . Copied into a temporary when used.                                                                                                        |
| `let x: T;`                   | Allocate `T` bytes on stack bound as `x`. Assignable once, not mutable.                                                                                          |
| `let mut x: T;`               | Like `let`, but allow for **mutability** and mutable borrow.                                                                                                     |
| `x = y;`                      | Moves `y` to `x`, invalidating `y` if `T` is not **`Copy`**, and copying `y` otherwise.                                                                          |

绑定变量（Bound Variables）存在于堆栈中，用于同步代码。在 `async {}` 代码中，它们成为异步状态机的一部分，可能驻留在堆上。从技术上讲，可变性和不变性是误称。不可变的绑定或共享引用可能仍包含 Cell，从而提供内部可变性。创建和访问数据结构；以及其他一些西语类型。

| Example         | Explanation                                                                                                                                                      |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `S { x: y }`    | Create `struct S {}` or `use`'ed `enum E::S {}` with field `x` set to `y`.                                                                                       |
| `S { x }`       | Same, but use local variable `x` for field `x`.                                                                                                                  |
| `S { ..s }`     | Fill remaining fields from `s`, esp. useful with [Default](https://doc.rust-lang.org/std/default/trait.Default.html).                                            |
| `S { 0: x }`    | Like `S` `(x)` below, but set field `.0` with struct syntax.                                                                                                     |
| `S` `(x)`       | Create `struct S` `(T)` or `use`'ed `enum E::S` `()` with field `.0` set to `x`.                                                                                 |
| `S`             | If `S` is unit `struct S;` or `use`'ed `enum E::S` create value of `S`.                                                                                          |
| `E::C { x: y }` | Create enum variant `C`. Other methods above also work.                                                                                                          |
| `()`            | Empty tuple, both literal and type, aka **unit**.                                                                                                                |
| `(x)`           | Parenthesized expression.                                                                                                                                        |
| `(x,)`          | Single-element **tuple** expression.                                                                                                                             |
| `(S,)`          | Single-element tuple type.                                                                                                                                       |
| `[S]`           | Array type of unspecified length, i.e., **slice**. Can't live on stack.                                                                                          |
| `[S; n]`        | **Array type** of fixed length `n` holding elements of type `S`.                                                                                                 |
| `[x; n]`        | Array instance with `n` copies of `x`.                                                                                                                           |
| `[x, y]`        | Array instance with given elements `x` and `y`.                                                                                                                  |
| `x[0]`          | Collection indexing. Overloadable [Index](https://doc.rust-lang.org/std/ops/trait.Index.html), [IndexMut](https://doc.rust-lang.org/std/ops/trait.IndexMut.html) |
| `x[..]`         | Collection slice-like indexing via [RangeFull](https://doc.rust-lang.org/std/ops/struct.RangeFull.html), _c_. slices.                                            |
| `x[a..]`        | Collection slice-like indexing via [RangeFrom](https://doc.rust-lang.org/std/ops/struct.RangeFrom.html).                                                         |
| `x[..b]`        | Collection slice-like indexing [RangeTo](https://doc.rust-lang.org/std/ops/struct.RangeTo.html).                                                                 |
| `x[a..b]`       | Collection slice-like indexing via [Range](https://doc.rust-lang.org/std/ops/struct.Range.html).                                                                 |
| `a..b`          | Right-exclusive **range** creation, also seen as `..b`.                                                                                                          |
| `a..=b`         | Inclusive range creation, also seen as `..=b`.                                                                                                                   |
| `s.x`           | Named **field access**, might try to [Deref](https://doc.rust-lang.org/std/ops/trait.Deref.html) if `x` not part of type `S`.                                    |
| `s.0`           | Numbered field access, used for tuple types `S` `(T)`.                                                                                                           |

这些签名不适合任何其他类别，但是很高兴知道。

| Example                     | Explanation                                                               |
| --------------------------- | ------------------------------------------------------------------------- | ----- | ---- |
| `!`                         | Always empty **never type**.                                              |
| `_`                         | Unnamed variable binding, e.g., `                                         | x, \_ | {}`. |
| `let _ = x;`                | Unnamed assignment is no-op, does **not** move out `x` or preserve scope! |
| `_x`                        | Variable binding explicitly marked as unused.                             |
| `1_234_567`                 | Numeric separator for visual clarity.                                     |
| `1_u8`                      | Type specifier for **numeric literals** (also `i8`, `u16`, ...).          |
| `0xBEEF`, `0o777`, `0b1001` | Hexadecimal (`0x`), octal (`0o`) and binary (`0b`) integer literals.      |
| `r#foo`                     | A **raw identifier** for edition compatibility.                           |
| `x;`                        | **Statement** terminator, _c_. **expressions**                            |

## References & Pointers

授予对未拥有的内存的访问权限。另请参见“泛型和约束”部分。

| Example                    | Explanation                                                                                                                                                |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `&S`                       | Shared **reference** (space for holding _any_ `&s`).                                                                                                       |
| `&[S]`                     | Special slice reference that contains (`address`, `length`).                                                                                               |
| `&str`                     | Special string reference that contains (`address`, `length`).                                                                                              |
| `&mut S`                   | Exclusive reference to allow mutability (also `&mut [S]`, `&mut dyn S`, ...)                                                                               |
| `&dyn T`                   | Special **trait object** reference that contains (`address`, `vtable`).                                                                                    |
| `*const S`                 | Immutable **raw pointer type** w/o memory safety.                                                                                                          |
| `*mut S`                   | Mutable raw pointer type w/o memory safety.                                                                                                                |
| `&s`                       | Shared **borrow** (e.g., address, len, vtable, ... of _this_ `s`, like `0x1234`).                                                                          |
| `&mut s`                   | Exclusive borrow that allows **mutability**.                                                                                                               |
| `ref s`                    | **Bind by reference**.                                                                                                                                     |
| `let ref r = s;`           | Equivalent to `let r = &s`.                                                                                                                                |
| `let S { ref mut x } = s;` | Mutable ref binding (`let x = &mut s.x`), shorthand destructuring version.                                                                                 |
| `*r`                       | **Dereference** a reference `r` to access what it points to.                                                                                               |
| `*r = s;`                  | If `r` is a mutable reference, move or copy `s` to target memory.                                                                                          |
| `s = *r;`                  | Make `s` a copy of whatever `r` references, if that is `Copy`.                                                                                             |
| `s = *my_box;`             | [Special case](https://www.reddit.com/r/rust/comments/b4so6i/what_is_exactly/ej8xwg8/) for `Box` that can also move out Box'ed content if it isn't `Copy`. |
| `'a`                       | A **lifetime parameter**,, duration of a flow in static analysis.                                                                                          |
| `&'a S`                    | Only accepts a `s` with an address that lives `'a` or longer.                                                                                              |
| `&'a mut S`                | Same, but allow content of address to be changed.                                                                                                          |
| `struct S<'a> {}`          | Signals `S` will contain address with lifetime `'a`. Creator of `S` decides `'a`.                                                                          |
| `trait T<'a> {}`           | Signals a `S` which `impl T for S` might contain address.                                                                                                  |
| `fn f<'a>(t: &'a T)`       | Same, for function. Caller decides `'a`.                                                                                                                   |
| `'static`                  | Special lifetime lasting the entire program execution.                                                                                                     |

## Types

类型的简写名称，以及将一种类型转换为另一种类型的方法。

| Example       | Explanation                                                                                                                                                                      |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `type T = S;` | Create a **type alias**, i.e., another name for `S`.                                                                                                                             |
| `Self`        | Type alias for **implementing type**, e.g. `fn new() -> Self`.                                                                                                                   |
| `self`        | Method subject in `fn f(self) {}`, same as `fn f(self: Self) {}`.                                                                                                                |
| `&self`       | Same, but refers to self as borrowed, same as `f(self: &Self)`                                                                                                                   |
| `&mut self`   | Same, but mutably borrowed, same as `f(self: &mut Self)`                                                                                                                         |
| `self: Box`   | [Arbitrary self type](https://github.com/withoutboats/rfcs/blob/arbitray-receivers/text/0000-century-of-the-self-type.md), add methods to smart pointers (`my_box.f_of_self()`). |
| `S as T`      | **Disambiguate** type `S` as trait `T`, e.g., `::f()`.                                                                                                                           |
| `S as R`      | In `use` of symbol, import `S` as `R`, e.g., `use a::S as R`.                                                                                                                    |
| `x as u32`    | Primitive **cast**, may truncate and be a bit surprising.                                                                                                                        |

## Functions & Behavior

定义代码单元及其抽象。

| Example                | Explanation                                                                          |
| ---------------------- | ------------------------------------------------------------------------------------ | ------ | ------------------------------------------------------------------------ |
| `trait T {}`           | Define a **trait**; common behavior others can implement.                            |
| `trait T : R {}`       | `T` is subtrait of **supertrait** `R`. Any `S` must `impl R` before it can `impl T`. |
| `impl S {}`            | **Implementation** of functionality for a type `S`, e.g., methods.                   |
| `impl T for S {}`      | Implement trait `T` for type `S`.                                                    |
| `impl !T for S {}`     | Disable an automatically derived **auto trait** .                                    |
| `fn f() {}`            | Definition of a **function**; or associated function if inside `impl`.               |
| `fn f() -> S {}`       | Same, returning a value of type S.                                                   |
| `fn f(&self) {}`       | Define a **method**, e.g., within an `impl S {}`.                                    |
| `const fn f() {}`      | Constant `fn` usable at compile time, e.g., `const X: u32 = f(Y)`.                   |
| `async fn f() {}`      | **Async** function transformation, makes `f` return an `impl` **`Future`**.          |
| `async fn f() -> S {}` | Same, but make `f` return an `impl Future`.                                          |
| `async { x }`          | Used within a function, make `{ x }` an `impl Future`.                               |
| `fn() -> S`            | **Function pointers**,, memory holding address of a callable.                        |
| `Fn() -> S`            | **Callable Trait**, (also `FnMut`, `FnOnce`), implemented by closures, fn's ...      |
| `                      |                                                                                      | {}`    | A **closure** that borrows its **captures**.                             |
| `                      | x                                                                                    | {}`    | Closure with a bound parameter `x`.                                      |
| `                      | x                                                                                    | x + x` | Closure without block expression; may only consist of single expression. |
| `move                  | x                                                                                    | x + y` | Closure taking ownership of its captures.                                |
| `return                |                                                                                      | true`  | Closures sometimes look like logical ORs (here: return a closure).       |
| `unsafe`               | If you enjoy debugging segfaults Friday night; **unsafe code**.                      |
| `unsafe f() {}`        | Sort-of means "_can cause UB, **YOU must check** requirements_".                     |
| `unsafe {}`            | Guarantees to compiler "**\*I have checked** requirements, trust me\*".              |

## Control Flow

| Example            | Explanation                                                                                                                                                                                 |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `while x {}`       | **Loop**, run while expression `x` is true.                                                                                                                                                 |
| `loop {}`          | **Loop infinitely** until `break`. Can yield value with `break x`.                                                                                                                          |
| `for x in iter {}` | Syntactic sugar to loop over **iterators**.                                                                                                                                                 |
| `if x {} else {}`  | **Conditional branch** if expression is true.                                                                                                                                               |
| `'label: loop {}`  | **Loop label**, useful for flow control in nested loops.                                                                                                                                    |
| `break`            | **Break expression** to exit a loop.                                                                                                                                                        |
| `break x`          | Same, but make `x` value of the loop expression (only in actual `loop`).                                                                                                                    |
| `break 'label`     | Exit not only this loop, but the enclosing one marked with `'label`.                                                                                                                        |
| `continue`         | **Continue expression** to the next loop iteration of this loop.                                                                                                                            |
| `continue 'label`  | Same, but instead of enclosing loop marked with `'label`.                                                                                                                                   |
| `x?`               | If `x` is [Err](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err) or [None](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None), **return and propagate**. |
| `x.await`          | Only works inside `async`. Yield flow until **`Future`** or Stream `x` ready.                                                                                                               |
| `return x`         | Early return from function. More idiomatic way is to end with expression.                                                                                                                   |
| `f()`              | Invoke callable `f` (e.g., a function, closure, function pointer, `Fn`, ...).                                                                                                               |
| `x.f()`            | Call member function, requires `f` takes `self`, `&self`, ... as first argument.                                                                                                            |
| `X::f(x)`          | Same as `x.f()`. Unless `impl Copy for X {}`, `f` can only be called once.                                                                                                                  |
| `X::f(&x)`         | Same as `x.f()`.                                                                                                                                                                            |
| `X::f(&mut x)`     | Same as `x.f()`.                                                                                                                                                                            |
| `S::f(&x)`         | Same as `x.f()` if `X` [derefs](https://doc.rust-lang.org/std/ops/trait.Deref.html) to `S`, i.e., `x.f()` finds methods of `S`.                                                             |
| `T::f(&x)`         | Same as `x.f()` if `X impl T`, i.e., `x.f()` finds methods of `T` if in scope.                                                                                                              |
| `X::f()`           | Call associated function, e.g., `X::new()`.                                                                                                                                                 |
| `::f()`            | Call trait method `T::f()` implemented for `X`.                                                                                                                                             |

## Pattern Matching

在 match 或 let 表达式或函数参数中找到的构造。

| Example                     | Explanation                                                                     |
| --------------------------- | ------------------------------------------------------------------------------- |
| `match m {}`                | Initiate **pattern matching**, then use match arms, _c_. next table.            |
| `let S(x) = get();`         | Notably, `let` also **destructures** similar to the table below.                |
| `let S { x } = s;`          | Only `x` will be bound to value `s.x`.                                          |
| `let (_, b, _) = abc;`      | Only `b` will be bound to value `abc.1`.                                        |
| `let (a, ..) = abc;`        | Ignoring 'the rest' also works.                                                 |
| `let (.., a, b) = (1, 2);`  | Specific bindings take precedence over 'the rest', here `a` is `1`, `b` is `2`. |
| `let Some(x) = get();`      | **Won't** work if pattern can be **refuted**, use `if let` instead.             |
| `if let Some(x) = get() {}` | Branch if pattern can be assigned (e.g., `enum` variant), syntactic sugar.      |
| `fn f(S { x }: S)`          | Function parameters also work like `let`, here `x` bound to `s.x` of `f(s)`.    |

匹配表达式中的模式匹配臂。这些臂的左侧也可以在 let 表达式中找到。

| Match Arm                 | Explanation                                                                              |
| ------------------------- | ---------------------------------------------------------------------------------------- | ------------------------------------------- |
| `E::A => {}`              | Match enum variant `A`, _c_. **pattern matching**.                                       |
| `E::B ( .. ) => {}`       | Match enum tuple variant `B`, wildcard any index.                                        |
| `E::C { .. } => {}`       | Match enum struct variant `C`, wildcard any field.                                       |
| `S { x: 0, y: 1 } => {}`  | Match struct with specific values (only accepts `s` with `s.x` of `0` and `s.y` of `1`). |
| `S { x: a, y: b } => {}`  | Match struct with _any_(!) values and bind `s.x` to `a` and `s.y` to `b`.                |
| `S { x, y } => {}`        | Same, but shorthand with `s.x` and `s.y` bound as `x` and `y` respectively.              |
| `S { .. } => {}`          | Match struct with any values.                                                            |
| `D => {}`                 | Match enum variant `E::D` if `D` in `use`.                                               |
| `D => {}`                 | Match anything, bind `D`; possibly false friend of `E::D` if `D` not in `use`.           |
| `_ => {}`                 | Proper wildcard that matches anything / "all the rest".                                  |
| `(a, 0) => {}`            | Match tuple with any value for `a` and `0` for second.                                   |
| `[a, 0] => {}`            | **Slice pattern**, match array with any value for `a` and `0` for second.                |
| `[1, ..] => {}`           | Match array starting with `1`, any value for rest; **subslice pattern**.                 |
| `[2, .., 5] => {}`        | Match array starting with `1`, ending with `5`.                                          |
| `[2, x @ .., 5] => {}`    | Same, but also bind `x` to slice representing middle (_c._ next entry).                  |
| `x @ 1..=5 => {}`         | Bind matched to `x`; **pattern binding**, here `x` would be `1`, `2`, ... or `5`.        |
| `0                        | 1 => {}`                                                                                 | Pattern alternatives (or-patterns).         |
| `E::A                     | E::Z`                                                                                    | Same, but on enum variants.                 |
| `E::C {x}                 | E::D {x}`                                                                                | Same, but bind `x` if all variants have it. |
| `S { x } if x > 10 => {}` | Pattern **match guards**, condition must be true as well to match.                       |

## Macros & Attributes

代码生成结构在实际编译发生之前就已扩展。

| Example    | Explanation                                                     |
| ---------- | --------------------------------------------------------------- |
| `m!()`     | **Macro** invocation, also `m!{}`, `m![]` (depending on macro). |
| `#[attr]`  | Outer **attribute**., annotating the following item.            |
| `#![attr]` | Inner attribute, annotating the surrounding item.               |

在声明性宏中的示例 macro_rules！实现这些工作：

| Within Macros | Explanation                                                                             |
| ------------- | --------------------------------------------------------------------------------------- |
| `$x:ty`       | Macro capture, with the `ty` part being:                                                |
| `$x:item`     | An item, like a function, struct, module, etc.                                          |
| `$x:block`    | A block `{}` of statements or expressions, e.g., `{ let x = 5; }`                       |
| `$x:stmt`     | A statement, e.g., `let x = 1 + 1;`, `String::new();` or `vec![];`                      |
| `$x:expr`     | An expression, e.g., `x`, `1 + 1`, `String::new()` or `vec![]`                          |
| `$x:pat`      | A pattern, e.g., `Some(t)`, `(17, 'a')` or `_`.                                         |
| `$x:ty`       | A type, e.g., `String`, `usize` or `Vec`.                                               |
| `$x:ident`    | An identifier, for example in `let x = 0;` the identifier is `x`.                       |
| `$x:path`     | A path (e.g. `foo`, `::std::mem::replace`, `transmute::<_, int>`, …).                   |
| `$x:literal`  | A literal (e.g. `3`, `"foo"`, `b"bar"`, etc.).                                          |
| `$x:lifetime` | A lifetime (e.g. `'a`, `'static`, etc.).                                                |
| `$x:meta`     | A meta item; the things that go inside `#[...]` and `#![...]` attributes.               |
| `$x:vis`      | A visibility modifier; `pub`, `pub(crate)`, etc.                                        |
| `$x:tt`       | A single token tree, [see here](https://stackoverflow.com/a/40303308) for more details. |
| `$x`          | Macro substitution, e.g., use the captured `$x:ty` from above.                          |
| `$(x),*`      | Macro repetition "zero or more times" in macros by example.                             |
| `$(x),?`      | Same, but "zero or one time".                                                           |
| `$(x),+`      | Same, but "one or more times".                                                          |
| `$(x)<<+`     | In fact separators other than `,` are also accepted. Here: `<<`.                        |
| `$crate`      | Special hygiene variable, crate where macros is defined.                                |

## Generics & Constraints

Generics combine with many other constructs such as struct S<T>, fn f<T>(), ...

| Example                     | Explanation                                                                           |
| --------------------------- | ------------------------------------------------------------------------------------- |
| `S`                         | A **generic** type with a type parameter (`T` is placeholder name here).              |
| `S`                         | Type short hand **trait bound** specification (`R` _must_ be actual trait).           |
| `T: R, P: S`                | **Independent trait bounds** (here one for `T` and one for `P`).                      |
| `T: R, S`                   | Compile error, you probably want compound bound `R + S` below.                        |
| `T: R + S`                  | **Compound trait bound**, `T` must fulfill `R` and `S`.                               |
| `T: R + 'a`                 | Same, but w. lifetime. `T` must fulfill `R`, if `T` has lifetimes, must outlive `'a`. |
| `T: ?Sized`                 | Opt out of a pre-defined trait bound, here `Sized`.                                   |
| `T: 'a`                     | Type **lifetime bound** ; if T has references, they must outlive `'a`.                |
| `T: 'static`                | Same; does esp. _not_ mean value `t` _will_ live `'static`, only that it could.       |
| `'b: 'a`                    | Lifetime `'b` must live at least as long as (i.e., _outlive_) `'a` bound.             |
| `S where T: R`              | Same as `S` but more pleasant to read for longer bounds.                              |
| `S`                         | **Default type parameter** for associated type.                                       |
| `S<'_>`                     | Inferred **anonymous lifetime**; asks compiler to _'figure it out'_ if obvious.       |
| `S<_>`                      | Inferred **anonymous type**, e.g., as `let x: Vec<_> = iter.collect()`                |
| `S::`                       | **Turbofish** call site type disambiguation, e.g. `f::()`.                            |
| `trait T {}`                | A trait generic over `X`. Can have multiple `impl T for S` (one per `X`).             |
| `trait T { type X; }`       | Defines **associated type** `X`. Only one `impl T for S` possible.                    |
| `type X = R;`               | Set associated type within `impl T for S { type X = R; }`.                            |
| `impl S {}`                 | Implement functionality for any `T` in `S`.                                           |
| `impl S {}`                 | Implement functionality for exactly `S` (e.g., `S`).                                  |
| `fn f() -> impl T`          | **Existential types**, returns an unknown-to-caller `S` that `impl T`.                |
| `fn f(x: &impl T)`          | Trait bound,"**impl traits**", somewhat similar to `fn f(x: &S)`.                     |
| `fn f(x: &dyn T)`           | Marker for **dynamic dispatch**, `f` will not be monomorphized.                       |
| `fn f() where Self: R;`     | In `trait T {}`, make `f` accessible only on types known to also `impl R`.            |
| `fn f() where Self: R {}`   | Esp. useful w. default methods (non dflt. would need be impl'ed anyway).              |
| `for<'a>`                   | **Higher-ranked trait bounds.**                                                       |
| `trait T: for<'a> R<'a> {}` | Any `S` that `impl T` would also have to fulfill `R` for any lifetime.                |

# Data Structures

# Organizing Code

将项目分割成较小的单元，并最大程度地减少依赖性。

| Example                | Explanation                                                                 |
| ---------------------- | --------------------------------------------------------------------------- |
| `mod m {}`             | Define a **module**, get definition from inside `{}`.                       |
| `mod m;`               | Define a module, get definition from `m.rs` or `m/mod.rs`.                  |
| `a::b`                 | Namespace **path** to element `b` within `a` (`mod`, `enum`, ...).          |
| `::b`                  | Search `b` relative to crate root.                                          |
| `crate::b`             | Search `b` relative to crate root.                                          |
| `self::b`              | Search `b` relative to current module.                                      |
| `super::b`             | Search `b` relative to parent module.                                       |
| `use a::b;`            | **Use** `b` directly in this scope without requiring `a` anymore.           |
| `use a::{b, c};`       | Same, but bring `b` and `c` into scope.                                     |
| `use a::b as x;`       | Bring `b` into scope but name `x`, like `use std::error::Error as E`.       |
| `use a::b as _;`       | Bring `b` anonymously into scope, useful for traits with conflicting names. |
| `use a::*;`            | Bring everything from `a` into scope.                                       |
| `pub use a::b;`        | Bring `a::b` into scope and reexport from here.                             |
| `pub T`                | "Public if parent path is public" **visibility** for `T`.                   |
| `pub(crate) T`         | Visible at most in current crate.                                           |
| `pub(self) T`          | Visible at most in current module.                                          |
| `pub(super) T`         | Visible at most in parent.                                                  |
| `pub(in a::b) T`       | Visible at most in `a::b`.                                                  |
| `extern crate a;`      | Declare dependency on external **crate** ; just `use a::b` in .             |
| `extern "C" {}`        | _Declare_ external dependencies and ABI (e.g., `"C"`) from **FFI**.         |
| `extern "C" fn f() {}` | _Define_ function to be exported with ABI (e.g., `"C"`) to FFI.             |

# 内存结构

## Basic Types

## 字符串

| Example                | Explanation                                                                  |
| ---------------------- | ---------------------------------------------------------------------------- |
| `"..."`                | **String literal**, UTF-8, will interpret `\n` as _line break_ `0xA`, ...    |
| `r"..."`               | **Raw string literal**. UTF-8, won't interpret `\n`, ...                     |
| `r#"..."#`             | Raw string literal, UTF-8, but can also contain `"`. Number of `#` can vary. |
| `b"..."`               | **Byte string literal**; constructs ASCII `[u8]`, not a string.              |
| `br"..."`, `br#"..."#` | Raw byte string literal, ASCII `[u8]`, combination of the above.             |
| `'🦀'`                 | **Character literal**, fixed 4 byte unicode '**char**'.                      |
| `b'x'`                 | ASCII **byte literal**.                                                      |

# TBD

- https://mojotv.cn/rust/rust-cheatsheet-01-data-structures Rust-CheatSheet
- https://colobu.com/2020/03/05/A-half-hour-to-learn-Rust/?hmsr=toutiao.io&utm_medium=toutiao.io&utm_source=toutiao.io
