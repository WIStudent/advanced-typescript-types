# Typed Omit Function

Remove certain properties from an object.

```typescript
type OmitResult<T extends Record<string, unknown>, K extends (keyof T)[]> = {
    [K2 in Exclude<keyof T, K[number]>]: T[K2]
}

const omit = <T extends Record<string, unknown>, K extends (keyof T)[]>(obj: T, keys: K): OmitResult<T, K> => {
    return Object.fromEntries(Object.entries(obj).filter(([key]) => !keys.includes(key))) as OmitResult<T, K>
}
```


## Usage
```typescript
const obj1 = {
    a: 'a',
    b: true,
    c: 42,
    d: null
}

const obj2 = omit(obj1, ['a', 'd'])

type Obj2 = typeof obj2
// Result
type Obj2 = {
  b: boolean;
  c: number;
}
```
[Playground Link](https://www.typescriptlang.org/play?target=99&jsx=0#code/C4TwDgpgBA8gtgS2AJQgZwK4BtgB4AqUEAHsBAHYAmaUqAxgPYBOluawTC5A5gDRQZyAa3IMA7uQB8-ANJFSFalAAUQiCAYAzKPgCUAbQC6kqAF4oAbwCwAKCj2o+mQCYoXKAFFidLBkoRcNQ1tfFl9cgw4ACMIJmNDAC4dJ2dDWwBfW1tGcnYoBkRgMygCeTIqGnpmVnZOHn5BEXEpWTLFGlV1LR0DY2UGKIArJNCoILQkmV0k+CRUTBwCWRNTE2s7ByYIYAwmclghiDpgADpNJgKPcg4EdGUYQ+OTihu7gcHdM4QcWOVlfSChl0ZhMAEJxicuD4-Hcgrp4VAAIY0WYodDYPCjGSSDJZGw5PLvACMxXWDiRSQA5IjKbxbOSokkOBgIHSNvY6EkACzONnkyhJCJYLC4mzZBi5IrvVzmApIfpDIn8fTU2lQSmUSlA2ygSAHQYyqC6iDdaVAA)

## Sources
- [TypeScript Type-safe Omit Function](https://stackoverflow.com/a/53968837)