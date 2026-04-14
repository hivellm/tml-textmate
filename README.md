# tml-textmate

TextMate grammar for [TML](https://github.com/hivellm/tml) — a systems programming language targeting LLVM IR.

## Usage

Used as a submodule by [GitHub Linguist](https://github.com/github-linguist/linguist) for language detection and syntax highlighting of `.tml` files.

Also compatible with any editor that supports TextMate grammars (VS Code, Sublime Text, Atom, Nova, etc.).

## Grammar

`syntaxes/tml.tmLanguage.json` provides syntax highlighting for:

- **Keywords**: `func`, `type`, `enum`, `behavior`, `impl`, `use`, `when`, `for`, `loop`, `async`, `await`, `lowlevel`, …
- **Primitive types**: `I8`–`I128`, `U8`–`U128`, `F32`, `F64`, `Bool`, `Str`, `Char`, `Unit`, `Never`
- **Built-in types**: `Maybe`, `Outcome`, `Vec`, `HashMap`, `Heap`, `Shared`, `Arc`, `Mutex`, …
- **Literals**: strings, raw strings `r"..."`, template literals `` `{expr}` ``, numbers (hex, binary, octal, float)
- **Operators**: `->`, `=>`, `|>`, `?.`, `::`, `..`, `?`, `!`
- **Decorators**: `@test`, `@bench`, `@extern`, `@derive`, …
- **Comments**: `//`, `///`, `//!`, `/* */`

## Language overview

TML is a multi-paradigm systems language with:

- Algebraic data types (`type`/`enum` with variants)
- Trait-like behaviors (`behavior` / `impl`)
- Generic types with bounds (`func foo[T: Ord + Display](…)`)
- Pattern matching via `when`
- Ownership-based memory without lifetime annotations
- Async/await concurrency model
- Low-level memory access via `lowlevel` blocks
- A self-hosting compiler (~150k lines of standard library)

```tml
use std::io

type Shape {
    Circle(F64),
    Rectangle(F64, F64),
}

impl Shape {
    pub func area(this) -> F64 {
        when this {
            Shape::Circle(r)       => 3.14159265 * r * r,
            Shape::Rectangle(w, h) => w * h,
        }
    }
}

func main() {
    let s = Shape::Circle(5.0)
    println(`Area: {s.area()}`)
}
```

## License

MIT
