# Learn ObjectId and Uuid

Learning how to generate `ObjectId` and `Uuid` using `hexadecimal` values.

Basic hexadecimal values

`0123456789abcdef`

contains 15 characters

## ObjectId Long Syntax

```ts
const __ObjectId = () => {
    /** Create function to convert decimal to hexadecimal */
    const toHex = (n: number) => Math.floor(n).toString(16); // Hexadecimal is Base 16
    /** Optional to add timestamp (contains 8 length) */
    const timestamp = toHex(Date.now() / 1000);
    /** Complete the missing 16 length to complete 24 total length */
    const hextra = ' '.repeat(16).replace(/./g, () => toHex(Math.random() * 16));

    return timestamp + hextra;
};

console.log(__ObjectId(), `-- from Long syntax`); // ==> 62b5c61c690af6b5464fabdd -- from Long syntax
```

## ObjectId Short Syntax

```ts
const ObjectId = (d = Date, m = Math, h = 16, x = (n: number) => m.floor(n).toString(h)) =>
    x(d.now() / 1000) + ' '.repeat(h).replace(/./g, () => x(m.random() * h));
// x(d.now() / 1000) + ' '.repeat(h).replace(/./g, x(m.random() * h)) // ==> without the `() =>` it will generate same values and not new instances

console.log(ObjectId(), `-- from Short syntax`); // ==> 62b5c61cee4292a9c7acf067 -- from Short syntax
```

## ObjectId without Timestamp

```ts
const AnyObjectId = (m = Math, h = 16, x = (n: number) => m.floor(n).toString(16)) =>
    ' '.repeat(24).replace(/./g, () => x(m.random() * h));

console.log(AnyObjectId(), `-- without timestamp\n`); // ==> af3dcf029d3e6be954fd003d -- without timestamp
```

## Uuid

```ts
const uuid = (d = Date, m = Math, h = 16, x = (n: number) => m.floor(n).toString(h), u = (n: number) => ' '.repeat(n).replace(/./g, () => x(m.random() * h))) =>
    x(d.now() / 1000) + '-' +
    u(4) + '-' + u(4) + '-' + u(4) + '-' + u(12);

console.log(uuid(), `-- uuid with timestamp`); // ==> 62b5c61c-3985-dd5d-223a-e275e1f1776d -- uuid with timestamp
```

## Uuid with timestamp
```ts
const anyUuid = (m = Math, h = 16, x = (n: number) => m.floor(n).toString(h), u = (n: number) => ' '.repeat(n).replace(/./g, () => x(m.random() * h))) =>
    u(8) + '-' + u(4) + '-' + u(4) + '-' + u(4) + '-' + u(12);

console.log(anyUuid(), `-- uuid without timestamp\n`); // ==> 22339f73-dd93-2919-1da4-a4381c69e7f0 -- uuid without timestamp
```

## Get timestamp from Hexadecimal

```ts
// ? To get the timestamp from hexadecimal

// extract the first 8 values
// ex. 62b5c61c690af6b5464fabdd
//
// timestamp in hex:
// 62b5c61c
// parseInt('62b5c61c', 16) * 1000
// = 1656079900000
// new Date(1656079900000)
// Fri Jun 24 2022 22:11:40 GMT+0800 (Singapore Standard Time)
```

## Manually convert Hexadecimal to Decimal

```ts
// ? Manually convert hexadecimal to decimal
// ex. 2df (3-char hexadecimal)
//
// start Base 16 from RIGHT to LEFT
// 16^0 = 1 
// 16^1 = 16 
// 16^2 = 256 = 16x16
//
// Just like Base 10
// 10^0 = 1     = 1
// 10^1 = 10    = 10
// 10^2 = 100   = 10 * 10
// 10^3 = 1000  = 10 * 10 * 10
//
// (know the hexadecimal values) = 0123456789abcdef
// a = 10
// b = 11
// c = 12
// d = 13
// e = 14
// f = 15
//
// going back to "2df"
// f = 16^0
// d = 16^1
// 2 = 16^2
// 
// f = 15
// 16^0 = 1
//
// d = 13
// 16^2 = 16
//
// 2 = 2
// 16^3 = 256
//
// 15 *  1 =  15
// 13 * 16 = 208
// 2 * 256 = 512
//
// 15 + 208 + 512 = 735
console.log(Math.floor(735).toString(16)); // ==> 2df
```