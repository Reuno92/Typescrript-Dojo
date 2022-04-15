# Typescript Dojo

## Who likes it ?
You probably know the "like" system from Facebook and other pages. People can "like" blog posts, pictures or other items. We want to create the text that should be displayed next to such an item.

Implement the function which takes an array containing the names of people that like an item. It must return the display text as shown in the examples:

```
[]                                -->  "no one likes this"
["Peter"]                         -->  "Peter likes this"
["Jacob", "Alex"]                 -->  "Jacob and Alex like this"
["Max", "John", "Mark"]           -->  "Max, John and Mark like this"
["Alex", "Jacob", "Mark", "Max"]  -->  "Alex, Jacob and 2 others like this"
```

Note: For 4 or more names, the number in `"and 2 others"` simply increases.

### My code functional codes
```typescript
export const likes = (a : string[]) : string => {
  // TODO
  
  if (a.length <= 0) {
    return 'no one likes this';
  }
  
  if (a.length === 1) {
    return `${a[0]} likes this`;
  } 
  
  if (a.length === 2) {
    return `${a.join(" and ")} like this`;
  }
  
  if (a.length === 3) {
    const twoFirst = a.slice(0, a.length - 1);
    const lastNames = a[a.length - 1];
    
    return twoFirst.join(", ") + ' and ' + a[a.length -1] + ' like this';
  }
  
  if (a.length >= 4) {
    const twoFirst = a.slice(0, 2);
    const remainingNames = a.slice(2, a.length).length;
    
    return twoFirst.join(", ") + ' and ' + remainingNames + " others like this";
  }
  
  return ''
}
```

### My refactoring code

```typescript
export const likes = (a : string[]) : string => {
  // TODO
  const TWO_FIRST: Array<string> = a.slice(0, 2);
  const END_OF_SENTENCE: string  = " like this";
  
  if (a.length <= 0) {
    return 'no one likes this';
  }
  
  if (a.length === 1) {
    return `${a[0]} likes this`;
  } 
  
  if (a.length === 2) {
    // Max and John like this
    return `${a.join(" and ")}${END_OF_SENTENCE}`;
  }
  
  if (a.length === 3) {
    const lastNames = a[a.length - 1];
    // Max, John and Mark like this 
    return `${TWO_FIRST.join(", ")} and ${a[a.length - 1]}${END_OF_SENTENCE}`;
  }
  
  if (a.length >= 4) {
    const remainingNames = a.slice(2, a.length).length;
    // Max, John and x others like this
    return `${TWO_FIRST.join(", ")} and ${remainingNames} others${END_OF_SENTENCE}`;
  }
  
  return '';
}
```

### Any best Practise

```typescript
export function likes(names: string[]): string {
  switch (names.length) {
    case 0:
      return 'no one likes this';
    case 1:
      return `${names[0]} likes this`;
    case 2:
      return `${names[0]} and ${names[1]} like this`;
    case 3:
      return `${names[0]}, ${names[1]} and ${names[2]} like this`;
    default:
      return `${names[0]}, ${names[1]} and ${names.length - 2} others like this`;
  }
}
```

```typescript
export const likes = (names: string[]): string => {
    switch (names.length) {
        case 0: return 'no one likes this';
        case 1: return `${names[0]} likes this`;
        case 2: return `${names[0]} and ${names[1]} like this`;
        case 3: return `${names[0]}, ${names[1]} and ${names[2]} like this`;
        default: return `${names[0]}, ${names[1]} and ${names.length - 2} others like this`;
    }
};
```

## Find the odd int

Given an array of integers, find the one that appears an odd number of times.

There will always be only one integer that appears an odd number of times.

**Examples**

```
[7] should return 7, because it occurs 1 time (which is odd).
[0] should return 0, because it occurs 1 time (which is odd).
[1,1,2] should return 2, because it occurs 1 time (which is odd).
[0,1,0,1,0] should return 0, because it occurs 3 times (which is odd).
[1,2,2,3,3,3,4,3,3,3,2,2,1] should return 4, because it appears 1 time (which is odd).
```

### My functional code:

```typescript
export const findOdd = (xs: number[]): number => {
  // TODO counter of occurences
  let counter: number = 0;
    
  if (xs.length === 1) {
    counter = xs[0];
  } else {
        
    // Loop to browse the array
    for (var i = 0, l = xs.length; l > i; i++) {
      const OCCURENCE = xs[i];
      const ARRAY = xs.filter( (x: number) => x === OCCURENCE);
      
      if (ARRAY.length % 2 === 1) {
        return OCCURENCE;
      }
    }
  }
    
  return counter;
};
```

### Any Best practise

```typescript
export const findOdd = (xs: number[]): number => {
  // happy coding!
  return xs.reduce( (a,b)=> a^b);
};
```

```typescript
export const findOdd = (items: number[]): number => {
  const uniqueItems = Array.from(new Set(items))
  
  for (const uniqueItem of uniqueItems) {
    const numberOccurences = items.filter(item => item === uniqueItem).length
    if (isOdd(numberOccurences)) return uniqueItem
  }
  
  throw new Error('none found')
};

function isOdd(num: number): boolean {
  return num % 2 === 1
};
```

```typescript
export const findOdd = (xs: number[]): number => xs.reduce( (a, b) => a ^ b, 0);
```

```typescript
export const findOdd = (xs: number[]): number => {
  // happy coding!
  return xs.find(a => xs.filter(b => b === a).length % 2 === 1) || 0;
};
```
