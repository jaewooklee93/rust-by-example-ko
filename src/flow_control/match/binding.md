## 바인딩

변수를 간접적으로 액세스하면 해당 변수를 사용하여 분기할 수 없으며, 다시 바인딩해야 합니다. `match`는 `@` 기호를 사용하여 값을 이름에 바인딩합니다.

```rust,editable
// `age` 함수는 `u32`를 반환합니다.
fn age() -> u32 {
    15
}

fn main() {
    println!("어떤 유형의 사람인지 말해주세요");

    match age() {
        0             => println!("아직 첫 생일을 축하하지 않았어요"),
        // `match`가 1 ..= 12를 직접적으로 사용할 수 있지만, 그렇게 하면 어떤 나이를 가진 아이라고 할까요? 대신, 1 ..= 12 범위에 대해 `n`에 바인딩하여 나이를 보고할 수 있습니다.
        n @ 1  ..= 12 => println!("나이는 {:?}세의 아이예요", n),
        n @ 13 ..= 19 => println!("나이는 {:?}세의 청소년이에요", n),
        // 아무것도 바인딩되지 않았습니다. 결과를 반환합니다.
        n             => println!("나이는 {:?}세의 노인이에요", n),
    }
}
```

`enum` 변형을 "구조화"하는 데에도 바인딩을 사용할 수 있습니다. 예를 들어 `Option`:

```rust,editable
fn some_number() -> Option<u32> {
    Some(42)
}

fn main() {
    match some_number() {
        // `Some` 변형을 얻었습니다. 값이 `n`에 바인딩된 경우, 42와 일치하는지 확인합니다.
        Some(n @ 42) => println!("정답: {}!", n),
        // 다른 모든 숫자에 대해 일치합니다.
        Some(n)      => println!("흥미롭지 않아요... {}", n),
        // `None` 변형에 대해 일치합니다.
        _            => (),
    }
}
```

### 참조:
[`함수`][함수], [`enum`][enum] 및 [`Option`][option]

[함수]: ../../fn.md
[enum]: ../../custom_types/enum.md
[option]: ../../std/option.md
