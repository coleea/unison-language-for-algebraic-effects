# Unison For Algebraic Effects

## Official Website
https://www.unison-lang.org/

## Unison official youtube channel
https://www.youtube.com/@unisonlanguage5679/videos

## "Unison: a new distributed programming language" by Paul Chiusano (in Strange Loop Conference)

https://www.youtube.com/watch?v=gCWtkvDQ2ZI

## Unison: program differently by Adam Warski | Lambda Days 2023

https://www.youtube.com/watch?v=Z-fUqrvmxgo


## MacOS 에서의 설치
```sh
brew install unisonweb/unison/unison-language
```

# 공식 튜토리얼

https://www.unison-lang.org/docs/quickstart/

# 핵심 개념 : Abilities

Unison의 Algebraic Effects 구현체는 `abilities`라고 부른다

> Terminology note: other languages with ability systems typically call them 'effect handlers' or 'algebraic effects', but many of the ideas are the same.



> Unison's system of abilities (often called "algebraic effects" in the literature) is based onthe Frank language 

> Unison diverges slightly from the scheme detailed in this paper. In particular:

> Unison's ability polymorphism is provided by ordinary polymorphic types, and a Unison type with an empty ability set explicitly disallows any abilities. In Frank, the empty ability set implies an ability-polymorphic type.

> Unison doesn't overload function application syntax to do ability handling; instead it has a separate




# 관련문서


## Unison abilities - unofficial alternative tutorial
https://gist.github.com/atacratic/7a91901d5535391910a2d34a2636a93c

## Using abilities part 1
https://www.unison-lang.org/docs/fundamentals/abilities/using-abilities-pt1/

## Using abilities part 2
https://www.unison-lang.org/docs/fundamentals/abilities/using-abilities-pt2/

## Error handling with abilities
https://www.unison-lang.org/docs/fundamentals/abilities/error-handling/

## Abilities and ability handlers
https://www.unison-lang.org/docs/language-reference/abilities-and-ability-handlers/

Unison에는 에러를 처리하는 4가지 방법이 있다

### `Abort` Abilities

아래와 같이 Optional 모나드로 래핑하여 처리한다
```
toOptional! '(divByException 1 0)
```

### `Throw` Abilities

아래와 같이 toEither의 인자로 호출한다
```
toEither '(divByThrow 1 0)
```

값의 타입은 Either이다
```
Left "Cannot divide by zero"
```

### `Exception` Abilities

아래와 같이 catch의 인자로 실행한다

```
catch '(divByException 1 0)
```

값은  `Either Failure a` 타입이 된다

```
Left (Failure (typeLink Generic) "Cannot divide by zero" (Any 0))
```

### unsafeRun

아래와 같이 예외처리 없이 호출할 수도 있다
```
unsafeRun! '(divByException 4 0)
```

이 경우 예외가 발생하면 프로그램은 크래시가 발생하며 그 즉시 종료된다

## Ability handlers
https://www.unison-lang.org/docs/language-reference/ability-handlers/