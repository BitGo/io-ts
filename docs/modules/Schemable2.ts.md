---
title: Schemable2.ts
nav_order: 19
parent: Modules
---

## Schemable2 overview

**This module is experimental**

Experimental features are published in order to get early feedback from the community, see these tracking
[issues](https://github.com/gcanti/io-ts/issues?q=label%3Av2.2+) for further discussions and enhancements.

A feature tagged as _Experimental_ is in a high state of flux, you're at risk of it changing without notice.

Added in v2.2.0

---

<h2 class="text-delta">Table of contents</h2>

- [utils](#utils)
  - [Schemable (interface)](#schemable-interface)
  - [Schemable1 (interface)](#schemable1-interface)
  - [Schemable2C (interface)](#schemable2c-interface)
  - [WithUnion (interface)](#withunion-interface)
  - [WithUnion1 (interface)](#withunion1-interface)
  - [WithUnion2C (interface)](#withunion2c-interface)
  - [WithUnknownContainers (interface)](#withunknowncontainers-interface)
  - [WithUnknownContainers1 (interface)](#withunknowncontainers1-interface)
  - [WithUnknownContainers2C (interface)](#withunknowncontainers2c-interface)

---

# utils

## Schemable (interface)

**Signature**

```ts
export interface Schemable<S> {
  readonly URI: S
  readonly literal: <A extends ReadonlyNonEmptyArray<DE.Literal>>(...values: A) => HKT<S, A[number]>
  readonly string: HKT<S, string>
  readonly number: HKT<S, number>
  readonly boolean: HKT<S, boolean>
  readonly struct: <A>(properties: { [K in keyof A]: HKT<S, A[K]> }) => HKT<S, { [K in keyof A]: A[K] }>
  readonly partial: <A>(properties: { [K in keyof A]: HKT<S, A[K]> }) => HKT<S, Partial<{ [K in keyof A]: A[K] }>>
  readonly tuple: <A extends ReadonlyArray<unknown>>(...components: { [K in keyof A]: HKT<S, A[K]> }) => HKT<S, A>
  readonly array: <A>(item: HKT<S, A>) => HKT<S, Array<A>>
  readonly record: <A>(codomain: HKT<S, A>) => HKT<S, Record<string, A>>
  readonly nullable: <A>(or: HKT<S, A>) => HKT<S, null | A>
  readonly intersect: <B>(right: HKT<S, B>) => <A>(left: HKT<S, A>) => HKT<S, A & B>
  readonly lazy: <A>(id: string, f: () => HKT<S, A>) => HKT<S, A>
  readonly sum: <T extends string>(
    tag: T
  ) => <A>(members: { [K in keyof A]: HKT<S, A[K] & Record<T, K>> }) => HKT<S, A[keyof A]>
}
```

Added in v2.2.3

## Schemable1 (interface)

**Signature**

```ts
export interface Schemable1<S extends URIS> {
  readonly URI: S
  readonly literal: <A extends ReadonlyNonEmptyArray<DE.Literal>>(...values: A) => Kind<S, A[number]>
  readonly string: Kind<S, string>
  readonly number: Kind<S, number>
  readonly boolean: Kind<S, boolean>
  readonly struct: <A>(properties: { [K in keyof A]: Kind<S, A[K]> }) => Kind<S, { [K in keyof A]: A[K] }>
  readonly partial: <A>(properties: { [K in keyof A]: Kind<S, A[K]> }) => Kind<S, Partial<{ [K in keyof A]: A[K] }>>
  readonly tuple: <A extends ReadonlyArray<unknown>>(...components: { [K in keyof A]: Kind<S, A[K]> }) => Kind<S, A>
  readonly array: <A>(item: Kind<S, A>) => Kind<S, Array<A>>
  readonly record: <A>(codomain: Kind<S, A>) => Kind<S, Record<string, A>>
  readonly nullable: <A>(or: Kind<S, A>) => Kind<S, null | A>
  readonly intersect: <B>(right: Kind<S, B>) => <A>(left: Kind<S, A>) => Kind<S, A & B>
  readonly lazy: <A>(id: string, f: () => Kind<S, A>) => Kind<S, A>
  readonly sum: <T extends string>(
    tag: T
  ) => <A>(members: { [K in keyof A]: Kind<S, A[K] & Record<T, K>> }) => Kind<S, A[keyof A]>
}
```

Added in v2.2.3

## Schemable2C (interface)

**Signature**

```ts
export interface Schemable2C<S extends URIS2, E> {
  readonly URI: S
  readonly _E: E
  readonly literal: <A extends ReadonlyNonEmptyArray<DE.Literal>>(...values: A) => Kind2<S, E, A[number]>
  readonly string: Kind2<S, E, string>
  readonly number: Kind2<S, E, number>
  readonly boolean: Kind2<S, E, boolean>
  readonly struct: <A>(properties: { [K in keyof A]: Kind2<S, E, A[K]> }) => Kind2<S, E, { [K in keyof A]: A[K] }>
  readonly partial: <A>(
    properties: { [K in keyof A]: Kind2<S, E, A[K]> }
  ) => Kind2<S, E, Partial<{ [K in keyof A]: A[K] }>>
  readonly tuple: <A extends ReadonlyArray<unknown>>(
    ...components: { [K in keyof A]: Kind2<S, E, A[K]> }
  ) => Kind2<S, E, A>
  readonly array: <A>(item: Kind2<S, E, A>) => Kind2<S, E, Array<A>>
  readonly record: <A>(codomain: Kind2<S, E, A>) => Kind2<S, E, Record<string, A>>
  readonly nullable: <A>(or: Kind2<S, E, A>) => Kind2<S, E, null | A>
  readonly intersect: <B>(right: Kind2<S, E, B>) => <A>(left: Kind2<S, E, A>) => Kind2<S, E, A & B>
  readonly lazy: <A>(id: string, f: () => Kind2<S, E, A>) => Kind2<S, E, A>
  readonly sum: <T extends string>(
    tag: T
  ) => <A>(members: { [K in keyof A]: Kind2<S, E, A[K] & Record<T, K>> }) => Kind2<S, E, A[keyof A]>
}
```

Added in v2.2.8

## WithUnion (interface)

**Signature**

```ts
export interface WithUnion<S> {
  readonly union: <A extends readonly [unknown, ...ReadonlyArray<unknown>]>(
    ...members: { [K in keyof A]: HKT<S, A[K]> }
  ) => HKT<S, A[number]>
}
```

Added in v2.2.3

## WithUnion1 (interface)

**Signature**

```ts
export interface WithUnion1<S extends URIS> {
  readonly union: <A extends readonly [unknown, ...ReadonlyArray<unknown>]>(
    ...members: { [K in keyof A]: Kind<S, A[K]> }
  ) => Kind<S, A[number]>
}
```

Added in v2.2.3

## WithUnion2C (interface)

**Signature**

```ts
export interface WithUnion2C<S extends URIS2, E> {
  readonly union: <A extends readonly [unknown, ...ReadonlyArray<unknown>]>(
    ...members: { [K in keyof A]: Kind2<S, E, A[K]> }
  ) => Kind2<S, E, A[number]>
}
```

Added in v2.2.8

## WithUnknownContainers (interface)

**Signature**

```ts
export interface WithUnknownContainers<S> {
  readonly UnknownArray: HKT<S, Array<unknown>>
  readonly UnknownRecord: HKT<S, Record<string, unknown>>
}
```

Added in v2.2.3

## WithUnknownContainers1 (interface)

**Signature**

```ts
export interface WithUnknownContainers1<S extends URIS> {
  readonly UnknownArray: Kind<S, Array<unknown>>
  readonly UnknownRecord: Kind<S, Record<string, unknown>>
}
```

Added in v2.2.3

## WithUnknownContainers2C (interface)

**Signature**

```ts
export interface WithUnknownContainers2C<S extends URIS2, E> {
  readonly UnknownArray: Kind2<S, E, Array<unknown>>
  readonly UnknownRecord: Kind2<S, E, Record<string, unknown>>
}
```

Added in v2.2.8