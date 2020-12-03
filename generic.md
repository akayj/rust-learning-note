# 范型(Generic)和特性(Trait)

## 范型
一般用于 __功能确定、数据类型不确定__ 的场景，如链表、映射表。

## 特性
特性(trait) 更接近Java中的接口 (interface)。
- **共同点**: 行为规范, 可以标识有什么方法。
- **不同点**: _TODO_

```rust
trait Descriptive {
	fn describe(&self) -> String;
}
```
__Descriptive__ 要求实现者必须有 `describe(&self) -> String` 方法。
