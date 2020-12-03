# 范型(Generic)和特性(Trait)

## 范型
一般用于 __功能确定、数据类型不确定__ 的场景，如链表、映射表。

## 特性
特性(trait) 更接近Java中的接口 (interface)。
- **共同点**: 规范方法。
- **不同点**: trait可以定义默认方法, interface 不可以。

### 定义特性
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

### 作为参数
- 可以将特性作为函数参数传递

``` rust
fn output(object: impl Descriptive) {
	println!("{}", object.describe());
}

// 范型方式, 与以上一样的效果
fn output<T: Descriptive>(object: T) {
	println!("{}", object.describe());
}

fn output_two<T: Descriptive>(arg1: T, arg2: T) {
	println!("{}", arg1.describe());
	println!("{}", arg2.describe());
}
```

- 多个特性通过 __+__ 叠加
``` rust
fn notify(item: impl Summary + Display)

// or
fn notify<T: Summary + Display>(item: T)
```

- 使用where简化多个类型
``` rust
fn some_function<T: Display + Clone, U: Clone + Debug)(t: T, u: U);

// 简化后
fn some_function<T, U>(t: T, u: U) ->i32
	where T: Display + Clone,
		  U: Clone + Debug
```
