# Omit Indices

Remove indices from an interface, only leaving known keys.

```typescript
type KnownKeys<T> = {
  [K in keyof T]: string extends K
    ? never
    : number extends K
      ? never
      : K
} extends { [_ in keyof T]: infer U } ? U : never

type OmitIndices<T> = Pick<T, KnownKeys<T>>
```

## Usage
```typescript
interface WithIndices {
  [key: string]: unknown;
  [key: number]: unknown;
  a: number;
  b: string;
  1?: boolean;
}

type WithoutIndices = OmitIndices<T>
// Result
type WithoutIndices = {
  a: number;
  b: string;
  1?: boolean;
}
```

## Explanation

```typescript
type KnownKeys<T> = {
  [K in keyof T]: string extends K
    ? never
    : number extends K
      ? never
      : K
}
```

takes every key of the interface and checks if string or number extends that key. If the key is a string/numerical literal type, string/number will not extend that string/numerical literal type. In that case `K` is assigned as value type to key `K`. In the other case `never` is asigned to key `K`. Using the `WithIndices` interface from above, this results in

```typescript
{
  [key: string]: never;
  [key: number]: never;
  a: 'a';
  b: 'b';
  1?: 1 | undefined;
}
```

```typescript
extends { [_ in keyof T]: infer U } ? U : never
```

then takes every value type from the previous interace and concatinates them to

```typescript
"a" | "b" | 1
```

These are then used in 

```typescript
type OmitIndices<T> = Pick<T, KnownKeys<T>>
```

to only pick the fields whose names are included in that union.

## Sources
- [How can I remove a wider type from a union type without removing its subtypes in TypeScript?](https://stackoverflow.com/questions/51954558/how-can-i-remove-a-wider-type-from-a-union-type-without-removing-its-subtypes-in/51955852#51955852)