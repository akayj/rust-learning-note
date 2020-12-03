# 范型(Generic)和特性(Trait)

## 范型
一般用于 __功能确定、数据类型不确定__ 的场景，如链表、映射表。

## 特性
特性(trait) 更接近Java中的接口 (interface)。
- **共同点**: 行为规范, 可以标识有什么方法。
- **不同点**: trait可以定义方法，将之作为默认方法。可重新定义，也可以使用默认方法。

```rust
trait Descriptive {
	// 只规范方法，没有定义
	fn describe(&self) -> String;

	// 定义了默认方法
	fn describe2(&self) -> String {
		String::from("[Object]")
	}
}
```
__Descriptive__ 要求实现者必须有 `describe(&self) -> String` 方法。

实现一个结构体, 格式: `impl <特性名> for <所实现的类型名>`
```rust
struct Person {
	name: String,
	age: u8
}

impl Descriptive for Person {
	fn describe(&self) -> String {
		format!("{} {}", self.name, self.age)
	}
}
```
