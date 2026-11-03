<a id="top"></a>

[⬅ Back](./README.md) | [⬅ Return to Root README](../README.md)

# TypeScript Coding Interview Questions & Answers

Solutions use strict-friendly TypeScript, preserve caller-owned inputs, and make return types explicit where useful. Complexity describes expected time and auxiliary space.

## 1. Two Sum

**Question:** Given an array of numbers and a target, return the indices of two distinct values that add up to the target. Assume exactly one solution exists.

**Answer:**

```ts
function twoSum(numbers: readonly number[], target: number): [number, number] {
  const indexByValue = new Map<number, number>();

  for (let index = 0; index < numbers.length; index += 1) {
    const complement = target - numbers[index];
    const complementIndex = indexByValue.get(complement);
    if (complementIndex !== undefined) {
      return [complementIndex, index];
    }
    indexByValue.set(numbers[index], index);
  }

  throw new Error('No two values sum to the target');
}
```

**Why it works:** The map stores values already visited and their indices. At each position, the algorithm checks whether the needed complement has appeared earlier.

**Complexity:** O(n) time and O(n) space.

**Alternative (brute force):** Check every pair. This needs no extra data structure but takes O(n²) time.

```ts
function twoSumBruteForce(
  numbers: readonly number[],
  target: number,
): [number, number] {
  for (let left = 0; left < numbers.length; left += 1) {
    for (let right = left + 1; right < numbers.length; right += 1) {
      if (numbers[left] + numbers[right] === target) {
        return [left, right];
      }
    }
  }

  throw new Error('No two values sum to the target');
}
```

## 2. First Non-Repeating Character

**Question:** Return the first character in a string that appears exactly once, or `null` if there is no such character.

**Answer:**

```ts
function firstUniqueCharacter(text: string): string | null {
  const counts = new Map<string, number>();

  for (const character of text) {
    counts.set(character, (counts.get(character) ?? 0) + 1);
  }

  for (const character of text) {
    if (counts.get(character) === 1) {
      return character;
    }
  }

  return null;
}
```

**Why it works:** The first pass counts characters; the second pass preserves input order and returns the first count of one.

**Complexity:** O(n) time and O(k) space, where k is the number of distinct characters.

**Alternative:** Use `indexOf` and `lastIndexOf` to test each character. This is concise, but takes O(n²) time in the worst case.

```ts
function firstUniqueCharacterBySearch(text: string): string | null {
  for (const character of text) {
    if (text.indexOf(character) === text.lastIndexOf(character)) {
      return character;
    }
  }

  return null;
}
```

## 3. Valid Parentheses

**Question:** Given a string containing only `()`, `{}`, and `[]`, determine whether every opening bracket is closed in the correct order.

**Answer:**

```ts
function hasValidParentheses(text: string): boolean {
  const matchingOpen: Readonly<Record<string, string>> = {
    ')': '(',
    ']': '[',
    '}': '{',
  };
  const stack: string[] = [];

  for (const character of text) {
    if (character === '(' || character === '[' || character === '{') {
      stack.push(character);
    } else if (stack.pop() !== matchingOpen[character]) {
      return false;
    }
  }

  return stack.length === 0;
}
```

**Why it works:** A stack makes the most recent unmatched opening bracket the next one that must close.

**Complexity:** O(n) time and O(n) space.

**Alternative:** Use an array as the stack and a plain lookup object for closing-to-opening bracket pairs.

```ts
function hasValidParenthesesWithObject(text: string): boolean {
  const matchingOpen: Record<string, string> = {
    ')': '(',
    ']': '[',
    '}': '{',
  };
  const stack: string[] = [];

  for (const character of text) {
    if ('([{'.includes(character)) {
      stack.push(character);
    } else if (stack.pop() !== matchingOpen[character]) {
      return false;
    }
  }

  return stack.length === 0;
}
```

## 4. Merge Two Sorted Arrays

**Question:** Merge two ascending arrays into a new ascending array without sorting the combined result.

**Answer:**

```ts
function mergeSortedArrays(
  left: readonly number[],
  right: readonly number[],
): number[] {
  const merged: number[] = [];
  let leftIndex = 0;
  let rightIndex = 0;

  while (leftIndex < left.length && rightIndex < right.length) {
    if (left[leftIndex] <= right[rightIndex]) {
      merged.push(left[leftIndex]);
      leftIndex += 1;
    } else {
      merged.push(right[rightIndex]);
      rightIndex += 1;
    }
  }

  return merged
    .concat(left.slice(leftIndex))
    .concat(right.slice(rightIndex));
}
```

**Why it works:** At each step, the smaller current value is the next value in the final ordering. The remaining tail is already sorted.

**Complexity:** O(n + m) time and O(n + m) space.

**Alternative:** Concatenate and sort the values. This is simpler, but takes O((n + m) log(n + m)) time and does not take advantage of the arrays already being sorted.

```ts
function mergeAndSort(left: readonly number[], right: readonly number[]): number[] {
  return [...left, ...right].sort((a, b) => a - b);
}
```

## 5. Remove Duplicates While Preserving Order

**Question:** Return a new array containing each value from the input only once, keeping the first occurrence order.

**Answer:**

```ts
function uniqueInOrder<T>(values: readonly T[]): T[] {
  const seen = new Set<T>();
  const result: T[] = [];

  for (const value of values) {
    if (!seen.has(value)) {
      seen.add(value);
      result.push(value);
    }
  }

  return result;
}
```

**Why it works:** A `Set` tracks values already emitted, while the result array records their original order.

**Complexity:** O(n) expected time and O(n) space.

**Alternative:** Construct a `Set` directly from the input; sets preserve insertion order.

```ts
const uniqueValues = [...new Set(values)];
```

## 6. Flatten a Nested Array

**Question:** Flatten an array nested to any depth into a new one-dimensional array.

**Answer:**

```ts
type NestedArray<T> = T | readonly NestedArray<T>[];

function isNestedArray<T>(
  value: NestedArray<T>,
): value is readonly NestedArray<T>[] {
  return Array.isArray(value);
}

function flattenArray<T>(values: readonly NestedArray<T>[]): T[] {
  const flattened: T[] = [];

  for (const value of values) {
    if (isNestedArray(value)) {
      flattened.push(...flattenArray(value));
    } else {
      flattened.push(value);
    }
  }

  return flattened;
}
```

**Why it works:** Each nested array is recursively flattened before its values are appended to the result.

**Complexity:** O(n) time and O(n + d) space, where n is the total number of values and d is the maximum nesting depth.

**Alternative:** Use the built-in `flat` method when the target runtime supports it.

```ts
const flattenedValues = values.flat(Infinity);
```

## 7. Debounce a Function

**Question:** Implement `debounce(fn, delay)` so that calls within the delay window cancel earlier scheduled calls. Preserve the latest call's `this` value and arguments.

**Answer:**

```ts
function debounce<This, Args extends unknown[]>(
  fn: (this: This, ...args: Args) => void,
  delay: number,
): (this: This, ...args: Args) => void {
  let timeoutId: ReturnType<typeof setTimeout> | undefined;

  return function (this: This, ...args: Args): void {
    if (timeoutId !== undefined) {
      clearTimeout(timeoutId);
    }
    const context = this;
    timeoutId = setTimeout(() => {
      fn.apply(context, args);
    }, delay);
  };
}
```

**Why it works:** Each call replaces the pending timer, so only the most recent call runs after the input has been quiet for `delay` milliseconds.

**Complexity:** O(1) work per call and O(1) auxiliary space, excluding the timer.

**Alternative:** Use `Reflect.apply` to invoke the callback with the latest call's receiver and arguments.

```ts
function debounceWithReflect<This, Args extends unknown[]>(
  fn: (this: This, ...args: Args) => void,
  delay: number,
): (this: This, ...args: Args) => void {
  let timeoutId: ReturnType<typeof setTimeout> | undefined;

  return function (this: This, ...args: Args): void {
    if (timeoutId !== undefined) {
      clearTimeout(timeoutId);
    }
    const context = this;
    timeoutId = setTimeout(
      () => Reflect.apply(fn, context, args),
      delay,
    );
  };
}
```

## 8. Group Items by a Key

**Question:** Implement `groupBy(items, keySelector)` to return a map from selected keys to the matching items.

**Answer:**

```ts
function groupBy<T, K>(
  items: readonly T[],
  keySelector: (item: T) => K,
): Map<K, T[]> {
  const groups = new Map<K, T[]>();

  for (const item of items) {
    const key = keySelector(item);
    const group = groups.get(key);
    if (group) {
      group.push(item);
    } else {
      groups.set(key, [item]);
    }
  }

  return groups;
}
```

**Example:**

```ts
interface Person {
  name: string;
  team: string;
}

const people: Person[] = [
  { name: 'Asha', team: 'blue' },
  { name: 'Ravi', team: 'green' },
  { name: 'Mina', team: 'blue' },
];

groupBy(people, (person) => person.team);
// Map {
//   'blue' => [{ name: 'Asha', team: 'blue' }, { name: 'Mina', team: 'blue' }],
//   'green' => [{ name: 'Ravi', team: 'green' }]
// }
```

**Why it works:** Each item is appended to the array associated with its selected key, creating that array on first use. A `Map` preserves key types instead of converting them to strings.

**Complexity:** O(n) expected time and O(n) space.

**Alternative:** Use `reduce` to build the map.

```ts
function groupByWithReduce<T, K>(
  items: readonly T[],
  keySelector: (item: T) => K,
): Map<K, T[]> {
  return items.reduce((groups, item) => {
    const key = keySelector(item);
    const group = groups.get(key) ?? [];
    group.push(item);
    groups.set(key, group);
    return groups;
  }, new Map<K, T[]>());
}
```

## 9. Check Whether a Sentence Has Repeated Characters

**Question:** Write a function that returns `true` if a sentence contains no repeated characters, ignoring whitespace and letter case. Otherwise, return `false`.

**Answer:**

```ts
function hasNoRepeatedCharacters(sentence: string): boolean {
  const cleanedSentence = sentence.replace(/\s+/g, '').toLowerCase();
  return new Set(cleanedSentence).size === cleanedSentence.length;
}

const input: string = 'you want to handle sentences';
console.log(hasNoRepeatedCharacters(input)); // false
```

**Why it works:** The function removes whitespace and lowercases the sentence so differences in spacing and case do not affect the result. A `Set` keeps only unique characters; if its size is smaller than the cleaned string's length, at least one character repeats.

**Complexity:** O(n) time and O(k) space, where n is the sentence length and k is the number of distinct characters.

**Note:** Punctuation is counted as a character. JavaScript string iteration and `Set` compare Unicode code points, not user-perceived grapheme clusters.

**Alternative:** Check each normalized character as it is encountered, returning as soon as one has already been seen.

```ts
function hasNoRepeatedCharactersInOnePass(sentence: string): boolean {
  const seen = new Set<string>();

  for (const character of sentence.replace(/\s+/g, '').toLowerCase()) {
    if (seen.has(character)) {
      return false;
    }
    seen.add(character);
  }

  return true;
}
```

## 10. Check That Each Word Has No Repeated Characters

**Question:** Write a function that returns `true` if every word in a sentence contains no repeated characters. Ignore punctuation and letter case. Return `false` if any word contains a repeated character.

**Answer:**

```ts
function hasNoRepeatedWords(sentence: string): boolean {
  const words = sentence.toLowerCase().match(/\b\w+\b/g) ?? [];

  for (const word of words) {
    if (new Set(word).size !== word.length) {
      return false;
    }
  }

  return true;
}

console.log(hasNoRepeatedWords('you want to handle sentences')); // false
console.log(hasNoRepeatedWords('you come')); // true
```

**Why it works:** The regular expression extracts alphanumeric words and underscores, excluding punctuation. Each word is lowercased and checked independently; a `Set` smaller than the word length means that word contains a repeated character. Repeated words in different positions are allowed if each word itself has unique characters.

**Complexity:** O(n) time and O(n) space, where n is the sentence length.

**Note:** In JavaScript, `\w` and `\b` are primarily ASCII-oriented, so this expression does not fully support words containing many non-ASCII letters.

**Alternative:** Use `every` to express the “all words pass” condition directly.

```ts
function hasNoRepeatedWordsWithEvery(sentence: string): boolean {
  const words = sentence.toLowerCase().match(/\b\w+\b/g) ?? [];
  return words.every((word) => new Set(word).size === word.length);
}
```

## 11. Explain and Create Shallow and Deep Copies

**Question:** How do you copy an object or array in TypeScript? Explain the difference between a shallow copy and a deep copy.

**Answer:**

```ts
interface Preferences {
  theme: string;
}

interface UserSettings {
  name: string;
  preferences: Preferences;
  tags: string[];
}

const original: UserSettings = {
  name: 'Asha',
  preferences: { theme: 'dark' },
  tags: ['interview', 'typescript'],
};

const shallowObjectCopy: UserSettings = { ...original };
const shallowArrayCopy: string[] = [...original.tags];
const assignedCopy: UserSettings = Object.assign({}, original);

const deepCopy: UserSettings = structuredClone(original);
```

**Why it works:** Spread syntax and `Object.assign` create new outer containers, but nested objects and arrays are still shared references. `structuredClone` recursively clones supported values, so nested data is independent.

**Important distinction:** JSON serialization (`JSON.parse(JSON.stringify(value))`) is only a limited workaround. It drops or changes values such as `undefined`, functions, symbols, and special numeric values; it also cannot handle circular references or preserve types such as `Date` and `Map`. Prefer `structuredClone` when its supported types fit the data.

**Complexity:** Shallow copies take O(n) time for the copied top-level properties/elements. Deep cloning takes time and space proportional to the cloned data.

**Alternative for JSON-safe data only:** JSON serialization can clone simple data made only of JSON-compatible values. It is not a general replacement for `structuredClone`.

```ts
const jsonDeepCopy: UserSettings = JSON.parse(JSON.stringify(original));
```

## 12. Find Duplicate Values in an Array

**Question:** Given an array, return the distinct values that appear more than once.

**Answer:**

```ts
function findDuplicates<T>(values: readonly T[]): T[] {
  const seen = new Set<T>();
  const duplicates = new Set<T>();

  for (const value of values) {
    if (seen.has(value)) {
      duplicates.add(value);
    } else {
      seen.add(value);
    }
  }

  return [...duplicates];
}

const values = [1, 2, 3, 42, 21, 3, 1];
console.log(findDuplicates(values)); // [3, 1]
```

**Why it works:** `seen` records values already encountered. A value is added to `duplicates` when it appears again; using a second `Set` ensures each duplicate is returned once.

**Complexity:** O(n) expected time and O(n) space.

**Alternative:** Filter values whose first and last positions differ, then use a `Set` to avoid returning a duplicate more than once. This takes O(n²) time in the worst case.

```ts
function findDuplicatesBySearch<T>(values: readonly T[]): T[] {
  return [...new Set(values.filter(
    (value) => values.indexOf(value) !== values.lastIndexOf(value),
  ))];
}
```

## 13. Map Words to Their Lengths

**Question:** Given a sentence, create a mapping from each whitespace-separated word to its character length.

**Answer:**

```ts
function wordLengths(sentence: string): Map<string, number> {
  const result = new Map<string, number>();
  const words = sentence.trim().split(/\s+/).filter(Boolean);

  for (const word of words) {
    result.set(word, word.length);
  }

  return result;
}

const lengths = wordLengths('this is an awesome day!.');
console.log([...lengths]);
// [['this', 4], ['is', 2], ['an', 2], ['awesome', 7], ['day!.', 5]]
```

**Why it works:** The sentence is split on one or more whitespace characters, then each word is paired with its length. A `Map` safely supports arbitrary word keys; punctuation stays attached to the word.

**Complexity:** O(n) time and O(k) space, where n is the sentence length and k is the number of distinct words.

**Alternative:** Use `Object.fromEntries` when string-keyed object output is preferred.

```ts
function wordLengthsAsObject(sentence: string): Record<string, number> {
  const words = sentence.trim().split(/\s+/).filter(Boolean);
  return Object.fromEntries(words.map((word) => [word, word.length]));
}
```

## 14. Extract Vowels from a String

**Question:** Return all English vowels found in a string, preserving their original order and case.

**Answer:**

```ts
function extractVowels(text: string): string[] {
  return text.match(/[aeiou]/gi) ?? [];
}

console.log(extractVowels('This is an awesome day!.'));
// ['i', 'i', 'a', 'a', 'e', 'o', 'e', 'a']
```

**Why it works:** The character class matches `a`, `e`, `i`, `o`, or `u`; the `i` flag makes matching case-insensitive, and `g` finds every occurrence. `match` returns `null` when no vowel is found, so `?? []` gives a consistent array result.

**Complexity:** O(n) time and O(k) space for k matched vowels.

**Alternative:** Iterate over the string and test each character against a vowel pattern.

```ts
function extractVowelsWithLoop(text: string): string[] {
  const vowels: string[] = [];
  for (const character of text) {
    if (/[aeiou]/i.test(character)) {
      vowels.push(character);
    }
  }
  return vowels;
}
```

## 15. Explain the Loop-Closure Timeout Pattern

**Question:** Why does an immediately invoked function expression (IIFE) make this loop log `0` through `4`, and what is the modern alternative?

**Answer:**

```ts
for (var i = 0; i < 5; i += 1) {
  (function (capturedIndex: number): void {
    setTimeout(() => {
      console.log(capturedIndex);
    }, 1000);
  })(i);
}
```

Each IIFE call receives the current value of `i` as `capturedIndex`, creating a separate function-scoped binding for that callback. With `var` and no IIFE, callbacks would share the same binding and typically log `5` after the loop finishes.

**Alternative:** Use block-scoped `let`, which creates a per-iteration binding and removes the need for the IIFE:

```ts
for (let i = 0; i < 5; i += 1) {
  setTimeout(() => {
    console.log(i);
  }, 1000);
}
```

**Complexity:** O(n) time and O(n) scheduled callbacks for n iterations.

## 16. Flatten a Nested Array

**Question:** Flatten a nested array of numbers into a new one-dimensional array.

**Answer:**

```ts
type NestedNumber = number | readonly NestedNumber[];

function flatten(array: readonly NestedNumber[]): number[] {
  return array.reduce<number[]>((result, value) => {
    return Array.isArray(value)
      ? result.concat(flatten(value))
      : result.concat(value);
  }, []);
}

const nested: NestedNumber[] = [1, [2, [3, 4]], [5, 6, [7, 8, 9]]];
console.log(flatten(nested)); // [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

**Alternative:** Use the built-in `flat` method:

```ts
console.log(nested.flat(Infinity));
```

`flat(Infinity)` is convenient when the target TypeScript library includes `Array.prototype.flat`; the recursive implementation above also works without relying on that built-in.

**Why it works:** The recursive solution descends into each nested array and appends its flattened values.

**Avoid:** `array.toString().split(',').map(Number)` is not a general flattening solution. It converts values to strings, loses nested structure and types, and can mishandle strings, `null`, empty slots, and other values.

**Complexity:** O(n) time and O(n + d) space, where n is the total number of elements and d is the maximum nesting depth.

## 17. Reverse a String

**Question:** Reverse a string without using the built-in `.reverse()` method.

**Answer:**

```ts
function reverseString(text: string): string {
  const characters = Array.from(text);
  let reversed = '';

  for (let index = characters.length - 1; index >= 0; index -= 1) {
    reversed += characters[index];
  }

  return reversed;
}
```

**Alternative:** Build the result from left to right by prepending each character. Repeated concatenation can be less efficient for long strings.

```ts
function reverseStringByPrepending(text: string): string {
  let reversed = '';
  for (const character of text) {
    reversed = character + reversed;
  }
  return reversed;
}
```

**Complexity:** O(n) time and O(n) space for the character array and result. `Array.from` iterates Unicode code points, but not multi-code-point grapheme clusters.

## 18. Check Whether a String Is a Palindrome

**Question:** Determine whether a string reads the same forward and backward, ignoring whitespace and letter case.

**Answer:**

```ts
function isPalindrome(text: string): boolean {
  const characters = Array.from(text.replace(/\s+/g, '').toLowerCase());
  let left = 0;
  let right = characters.length - 1;

  while (left < right) {
    if (characters[left] !== characters[right]) return false;
    left += 1;
    right -= 1;
  }

  return true;
}
```

**Alternative:** Create a normalized string, manually reverse its characters, and compare the two strings.

```ts
function isPalindromeByReversing(text: string): boolean {
  const normalized = Array.from(text.replace(/\s+/g, '').toLowerCase());
  let reversed = '';

  for (let index = normalized.length - 1; index >= 0; index -= 1) {
    reversed += normalized[index];
  }

  return normalized.join('') === reversed;
}
```

**Complexity:** O(n) time and O(n) space. Punctuation is not ignored; only whitespace and case are normalized.

## 19. Count Vowels

**Question:** Return the number of English vowels (`a`, `e`, `i`, `o`, `u`) in a string, regardless of case.

**Answer:**

```ts
function countVowels(text: string): number {
  return (text.match(/[aeiou]/gi) ?? []).length;
}
```

**Alternative:** Iterate through the characters and increment a counter when the character is in the vowel set.

```ts
function countVowelsWithLoop(text: string): number {
  const vowels = new Set(['a', 'e', 'i', 'o', 'u']);
  let count = 0;

  for (const character of text.toLowerCase()) {
    if (vowels.has(character)) count += 1;
  }

  return count;
}
```

**Complexity:** O(n) time and O(k) space for the regex result, or O(1) auxiliary space for the loop.

## 20. FizzBuzz

**Question:** For integers from 1 through 100, produce `"Fizz"` for multiples of 3, `"Buzz"` for multiples of 5, `"FizzBuzz"` for both, and the number otherwise.

**Answer:**

```ts
function fizzBuzz(limit = 100): string[] {
  const result: string[] = [];

  for (let number = 1; number <= limit; number += 1) {
    if (number % 15 === 0) result.push('FizzBuzz');
    else if (number % 3 === 0) result.push('Fizz');
    else if (number % 5 === 0) result.push('Buzz');
    else result.push(String(number));
  }

  return result;
}
```

**Alternative:** Build each output from independent divisibility checks.

```ts
function fizzBuzzByComposition(limit = 100): string[] {
  return Array.from({ length: limit }, (_, index) => {
    const number = index + 1;
    const label = `${number % 3 === 0 ? 'Fizz' : ''}${number % 5 === 0 ? 'Buzz' : ''}`;
    return label || String(number);
  });
}
```

**Complexity:** O(n) time and O(n) space for n output values.

## 21. Find the Minimum and Maximum

**Question:** Return the minimum and maximum numbers in an array, or `null` when the array is empty.

**Answer:**

```ts
function findMinMax(numbers: readonly number[]): { min: number; max: number } | null {
  if (numbers.length === 0) return null;

  let min = numbers[0];
  let max = numbers[0];
  for (const number of numbers) {
    if (number < min) min = number;
    if (number > max) max = number;
  }
  return { min, max };
}
```

**Alternative:** Use `Math.min` and `Math.max` with spread for modest-sized arrays.

```ts
function findMinMaxWithMath(
  numbers: readonly number[],
): { min: number; max: number } | null {
  if (numbers.length === 0) return null;
  return { min: Math.min(...numbers), max: Math.max(...numbers) };
}
```

**Complexity:** O(n) time and O(1) auxiliary space. The spread alternative may exceed argument limits for very large arrays.

## 22. Remove Array Duplicates

**Question:** Return a new array containing each value once, preserving its first-occurrence order.

**Answer:**

```ts
function removeDuplicates<T>(values: readonly T[]): T[] {
  return [...new Set(values)];
}
```

**Alternative:** Filter values that occur at their first index. This can take O(n²) time.

```ts
function removeDuplicatesByIndex<T>(values: readonly T[]): T[] {
  return values.filter((value, index) => values.indexOf(value) === index);
}
```

**Complexity:** The `Set` solution takes O(n) expected time and O(n) space.

## 23. Compute a Factorial Recursively

**Question:** Compute `n!` recursively for a non-negative integer `n`. Define `0!` as `1`.

**Answer:**

```ts
function factorial(n: number): number {
  if (!Number.isInteger(n) || n < 0) {
    throw new RangeError('n must be a non-negative integer');
  }
  if (n <= 1) return 1;
  return n * factorial(n - 1);
}
```

**Alternative:** Use an iterative loop to avoid recursive call-stack limits.

```ts
function factorialIterative(n: number): number {
  if (!Number.isInteger(n) || n < 0) {
    throw new RangeError('n must be a non-negative integer');
  }
  let result = 1;
  for (let value = 2; value <= n; value += 1) result *= value;
  return result;
}
```

**Complexity:** O(n) time. Recursion uses O(n) call-stack space; iteration uses O(1) auxiliary space. JavaScript `number` precision limits exact results.

## 24. Return the Nth Fibonacci Number

**Question:** Return the zero-based Nth Fibonacci number, with `F(0) = 0` and `F(1) = 1`.

**Answer:**

```ts
function fibonacci(n: number): number {
  if (!Number.isInteger(n) || n < 0) {
    throw new RangeError('n must be a non-negative integer');
  }

  let previous = 0;
  let current = 1;
  for (let index = 0; index < n; index += 1) {
    [previous, current] = [current, previous + current];
  }
  return previous;
}
```

**Alternative:** Use recursion with memoization to retain the recursive definition without recomputing values.

```ts
function fibonacciMemoized(
  n: number,
  memo = new Map<number, number>([[0, 0], [1, 1]]),
): number {
  if (!Number.isInteger(n) || n < 0) {
    throw new RangeError('n must be a non-negative integer');
  }
  if (!memo.has(n)) {
    memo.set(n, fibonacciMemoized(n - 1, memo) + fibonacciMemoized(n - 2, memo));
  }
  return memo.get(n)!;
}
```

**Complexity:** The iterative version takes O(n) time and O(1) auxiliary space. The memoized version takes O(n) time and O(n) space.

## 25. Convert a Sentence to Title Case

**Question:** Capitalize the first character of each whitespace-separated word and lowercase the remaining characters.

**Answer:**

```ts
function toTitleCase(sentence: string): string {
  return sentence
    .toLowerCase()
    .replace(/\b\w/g, (character) => character.toUpperCase());
}
```

**Alternative:** Split while retaining whitespace, then transform each word segment.

```ts
function toTitleCaseByWords(sentence: string): string {
  return sentence
    .split(/(\s+)/)
    .map((part) => {
      if (/^\s+$/.test(part) || part.length === 0) return part;
      return part[0].toUpperCase() + part.slice(1).toLowerCase();
    })
    .join('');
}
```

**Complexity:** O(n) time and O(n) space. The regex solution uses JavaScript's ASCII-oriented `\w` word-character class.

## 26. Chunk an Array

**Question:** Split an array into consecutive sub-arrays of at most `size` elements. Require `size` to be a positive integer.

**Answer:**

```ts
function chunkArray<T>(values: readonly T[], size: number): T[][] {
  if (!Number.isInteger(size) || size <= 0) {
    throw new RangeError('size must be a positive integer');
  }
  const chunks: T[][] = [];
  for (let index = 0; index < values.length; index += size) {
    chunks.push(values.slice(index, index + size));
  }
  return chunks;
}
```

**Alternative:** Use `reduce` to accumulate chunks.

```ts
function chunkArrayWithReduce<T>(values: readonly T[], size: number): T[][] {
  if (!Number.isInteger(size) || size <= 0) {
    throw new RangeError('size must be a positive integer');
  }
  return values.reduce<T[][]>((chunks, value, index) => {
    if (index % size === 0) chunks.push([]);
    chunks[chunks.length - 1].push(value);
    return chunks;
  }, []);
}
```

**Complexity:** O(n) time and O(n) space for n input values. The input is not mutated.

## 27. Detect Anagrams

**Question:** Determine whether two strings contain the same English letters and digits with the same frequencies, ignoring case, whitespace, and punctuation.

**Answer:**

```ts
function areAnagrams(left: string, right: string): boolean {
  const normalize = (text: string): string =>
    text.toLowerCase().replace(/[^a-z0-9]/g, '');
  const counts = new Map<string, number>();

  for (const character of normalize(left)) {
    counts.set(character, (counts.get(character) ?? 0) + 1);
  }
  for (const character of normalize(right)) {
    const count = counts.get(character);
    if (count === undefined) return false;
    if (count === 1) counts.delete(character);
    else counts.set(character, count - 1);
  }
  return counts.size === 0;
}
```

**Alternative:** Normalize, sort both character arrays, and compare them.

```ts
function areAnagramsBySorting(left: string, right: string): boolean {
  const normalize = (text: string): string =>
    text.toLowerCase().replace(/[^a-z0-9]/g, '');
  const sortCharacters = (text: string): string =>
    Array.from(normalize(text)).sort().join('');
  return sortCharacters(left) === sortCharacters(right);
}
```

**Complexity:** Frequency counting takes O(n + m) time and O(k) space. Sorting takes O(n log n + m log m) time.

## 28. Sum Array Elements

**Question:** Return the sum of an array of numbers using `.reduce()`. The sum of an empty array is `0`.

**Answer:**

```ts
function sumArray(numbers: readonly number[]): number {
  return numbers.reduce((sum, number) => sum + number, 0);
}
```

**Alternative:** Use a loop with an accumulator.

```ts
function sumArrayWithLoop(numbers: readonly number[]): number {
  let sum = 0;
  for (const number of numbers) sum += number;
  return sum;
}
```

**Complexity:** O(n) time and O(1) auxiliary space.

## 29. Filter Out Falsy Values

**Question:** Return a new array with `false`, `null`, `0`, `""`, `undefined`, and `NaN` removed.

**Answer:**

```ts
function removeFalsy(values: readonly unknown[]): unknown[] {
  return values.filter(Boolean);
}
```

**Alternative:** Use an explicit runtime predicate.

```ts
function removeFalsyExplicitly(values: readonly unknown[]): unknown[] {
  return values.filter((value) =>
    value !== false &&
    value !== null &&
    value !== 0 &&
    value !== '' &&
    value !== undefined &&
    !Number.isNaN(value)
  );
}
```

**Why it works:** `Boolean` converts each value to its truthiness. This also removes other falsy values such as `-0` and `0n`; it retains empty arrays and empty objects because they are truthy.

**Complexity:** O(n) time and O(n) space.

## 30. Check Whether a Number Is Prime

**Question:** Return `true` if an integer greater than 1 is prime; otherwise, return `false`.

**Answer:**

```ts
function isPrime(number: number): boolean {
  if (!Number.isInteger(number) || number <= 1) return false;
  if (number === 2) return true;
  if (number % 2 === 0) return false;
  for (let divisor = 3; divisor * divisor <= number; divisor += 2) {
    if (number % divisor === 0) return false;
  }
  return true;
}
```

**Alternative:** Test every possible divisor from `2` through `Math.sqrt(number)`.

```ts
function isPrimeSimple(number: number): boolean {
  if (!Number.isInteger(number) || number <= 1) return false;
  for (let divisor = 2; divisor <= Math.sqrt(number); divisor += 1) {
    if (number % divisor === 0) return false;
  }
  return true;
}
```

**Complexity:** O(√n) time and O(1) auxiliary space.

## 31. Find the Longest Word

**Question:** Return the first longest word in a sentence. Treat whitespace as word separators and ignore punctuation at each word's edges. Return an empty string if no words are present.

**Answer:**

```ts
function longestWord(sentence: string): string {
  const words = sentence
    .split(/\s+/)
    .map((word) => word.replace(/^[^\p{L}\p{N}]+|[^\p{L}\p{N}]+$/gu, ''))
    .filter(Boolean);

  let longest = '';
  for (const word of words) {
    if (word.length > longest.length) longest = word;
  }
  return longest;
}
```

**Alternative:** Use `reduce` to select the first word with the greatest length.

```ts
function longestWordWithReduce(sentence: string): string {
  const words = sentence
    .split(/\s+/)
    .map((word) => word.replace(/^[^\p{L}\p{N}]+|[^\p{L}\p{N}]+$/gu, ''))
    .filter(Boolean);
  return words.reduce(
    (longest, word) => word.length > longest.length ? word : longest,
    '',
  );
}
```

**Complexity:** O(n) time and O(n) space for the split and normalized words.

## 32. Truncate a String

**Question:** If a string is longer than `maxCharacters`, keep that many leading characters and append `"..."`. Otherwise, return it unchanged. Require a non-negative integer limit.

**Answer:**

```ts
function truncateString(text: string, maxCharacters: number): string {
  if (!Number.isInteger(maxCharacters) || maxCharacters < 0) {
    throw new RangeError('maxCharacters must be a non-negative integer');
  }
  return text.length > maxCharacters
    ? `${text.slice(0, maxCharacters)}...`
    : text;
}
```

**Alternative:** Use `substring` with the same boundary.

```ts
function truncateStringWithSubstring(text: string, maxCharacters: number): string {
  if (!Number.isInteger(maxCharacters) || maxCharacters < 0) {
    throw new RangeError('maxCharacters must be a non-negative integer');
  }
  return text.length > maxCharacters
    ? `${text.substring(0, maxCharacters)}...`
    : text;
}
```

**Complexity:** O(k) time and space for the returned prefix of length k. The limit counts UTF-16 code units.

## 33. Linear Search

**Question:** Return the index of the first matching target in an array, or `-1` if it is not present.

**Answer:**

```ts
function linearSearch<T>(values: readonly T[], target: T): number {
  for (let index = 0; index < values.length; index += 1) {
    if (values[index] === target) return index;
  }
  return -1;
}
```

**Alternative:** Use the built-in `indexOf` for strict-equality searches.

```ts
const targetIndex = values.indexOf(target);
```

**Complexity:** O(n) time and O(1) auxiliary space.

## 34. Check a String Ending Without `endsWith`

**Question:** Determine whether `text` ends with `target` without calling `.endsWith()`.

**Answer:**

```ts
function confirmEnding(text: string, target: string): boolean {
  if (target.length > text.length) return false;
  return text.slice(text.length - target.length) === target;
}
```

**Alternative:** Compare characters backward without creating a substring.

```ts
function confirmEndingByLoop(text: string, target: string): boolean {
  if (target.length > text.length) return false;
  for (let offset = 1; offset <= target.length; offset += 1) {
    if (text[text.length - offset] !== target[target.length - offset]) {
      return false;
    }
  }
  return true;
}
```

**Complexity:** O(m) time for target length m; the loop uses O(1) auxiliary space.

## 35. Repeat a String Without `.repeat()`

**Question:** Return `text` repeated `count` times without using the native `.repeat()` method. Require a non-negative integer count.

**Answer:**

```ts
function repeatString(text: string, count: number): string {
  if (!Number.isInteger(count) || count < 0) {
    throw new RangeError('count must be a non-negative integer');
  }
  let result = '';
  for (let index = 0; index < count; index += 1) result += text;
  return result;
}
```

**Alternative:** Use exponentiation by doubling so fewer concatenation steps are needed.

```ts
function repeatStringByDoubling(text: string, count: number): string {
  if (!Number.isInteger(count) || count < 0) {
    throw new RangeError('count must be a non-negative integer');
  }
  let result = '';
  let fragment = text;
  let remaining = count;
  while (remaining > 0) {
    if (remaining % 2 === 1) result += fragment;
    remaining = Math.floor(remaining / 2);
    if (remaining > 0) fragment += fragment;
  }
  return result;
}
```

**Complexity:** O(L) output work, where L is the length of the resulting string.

## 36. Merge Two Sorted Arrays

**Question:** Merge two ascending numeric arrays into one ascending array.

**Answer:**

```ts
function mergeSortedNumbers(
  left: readonly number[],
  right: readonly number[],
): number[] {
  const merged: number[] = [];
  let leftIndex = 0;
  let rightIndex = 0;
  while (leftIndex < left.length && rightIndex < right.length) {
    if (left[leftIndex] <= right[rightIndex]) {
      merged.push(left[leftIndex++]);
    } else {
      merged.push(right[rightIndex++]);
    }
  }
  return merged.concat(left.slice(leftIndex), right.slice(rightIndex));
}
```

**Alternative:** Concatenate and numerically sort; this does not use the fact that both arrays are already sorted.

```ts
function mergeSortedNumbersBySorting(
  left: readonly number[],
  right: readonly number[],
): number[] {
  return [...left, ...right].sort((a, b) => a - b);
}
```

**Complexity:** Two-pointer merge is O(n + m) time and space; sorting takes O((n + m) log(n + m)) time.

## 37. Check Whether a Year Is a Leap Year

**Question:** Return `true` if an integer year is a leap year in the Gregorian calendar. A year is leap if divisible by 4, except century years must also be divisible by 400.

**Answer:**

```ts
function isLeapYear(year: number): boolean {
  if (!Number.isInteger(year)) throw new RangeError('year must be an integer');
  return year % 400 === 0 || (year % 4 === 0 && year % 100 !== 0);
}
```

**Alternative:** Express the century exception first.

```ts
function isLeapYearByRules(year: number): boolean {
  if (!Number.isInteger(year)) throw new RangeError('year must be an integer');
  if (year % 100 === 0) return year % 400 === 0;
  return year % 4 === 0;
}
```

**Complexity:** O(1) time and O(1) space.

## 38. Extract Object Values

**Question:** Convert an object's own enumerable values into an array.

**Answer:**

```ts
function extractObjectValues<T extends Record<string, unknown>>(
  object: T,
): Array<T[keyof T]> {
  return Object.values(object);
}
```

**Alternative:** Get the object's entries and map each entry to its value.

```ts
function extractObjectValuesFromEntries<T extends Record<string, unknown>>(
  object: T,
): Array<T[keyof T]> {
  return Object.entries(object).map(([, value]) => value) as Array<T[keyof T]>;
}
```

**Complexity:** O(p) time and O(p) space for p enumerable own properties.

## 39. Count Element Frequencies

**Question:** Return an object mapping each string or number value in an array to its number of occurrences.

**Answer:**

```ts
function countFrequencies(values: readonly (string | number)[]): Record<string, number> {
  const counts: Record<string, number> = Object.create(null);
  for (const value of values) {
    const key = String(value);
    counts[key] = (counts[key] ?? 0) + 1;
  }
  return counts;
}
```

**Alternative:** Use a `Map` to preserve the original key type and avoid converting keys to strings.

```ts
function countFrequenciesWithMap<T>(values: readonly T[]): Map<T, number> {
  const counts = new Map<T, number>();
  for (const value of values) {
    counts.set(value, (counts.get(value) ?? 0) + 1);
  }
  return counts;
}
```

**Complexity:** O(n) expected time and O(k) space for k distinct values. In the object version, number `1` and string `'1'` share the same property key.

## 40. Compute an Average

**Question:** Return the average of an array of scores, or `null` when the array is empty.

**Answer:**

```ts
function average(scores: readonly number[]): number | null {
  if (scores.length === 0) return null;
  const total = scores.reduce((sum, score) => sum + score, 0);
  return total / scores.length;
}
```

**Alternative:** Accumulate the total using a loop.

```ts
function averageWithLoop(scores: readonly number[]): number | null {
  if (scores.length === 0) return null;
  let total = 0;
  for (const score of scores) total += score;
  return total / scores.length;
}
```

**Complexity:** O(n) time and O(1) auxiliary space.

## 41. Check Whether an Array Is Sorted

**Question:** Return `true` if a numeric array is sorted in non-decreasing order; equal adjacent values are allowed.

**Answer:**

```ts
function isSortedAscending(values: readonly number[]): boolean {
  for (let index = 1; index < values.length; index += 1) {
    if (values[index] < values[index - 1]) return false;
  }
  return true;
}
```

**Alternative:** Use `.every()` to check each adjacent pair.

```ts
function isSortedAscendingWithEvery(values: readonly number[]): boolean {
  return values.every(
    (value, index) => index === 0 || value >= values[index - 1],
  );
}
```

**Complexity:** O(n) time and O(1) auxiliary space; both versions stop once an inversion is found.

## Additional Coding Challenges

## 42. Two Sum

**Question:** Find two values that add to a target and return their distinct indices. Assume exactly one solution exists.

**Answer:**

```ts
function twoSumFast(values: readonly number[], target: number): [number, number] {
  const indexByValue = new Map<number, number>();
  for (let index = 0; index < values.length; index += 1) {
    const otherIndex = indexByValue.get(target - values[index]);
    if (otherIndex !== undefined) return [otherIndex, index];
    indexByValue.set(values[index], index);
  }
  throw new Error('No matching pair');
}
```

**Alternative:** Check every pair. This uses O(1) auxiliary space but takes O(n²) time.

```ts
function twoSumByPairs(values: readonly number[], target: number): [number, number] {
  for (let left = 0; left < values.length; left += 1) {
    for (let right = left + 1; right < values.length; right += 1) {
      if (values[left] + values[right] === target) return [left, right];
    }
  }
  throw new Error('No matching pair');
}
```

## 43. Valid Parentheses Parser

**Question:** Check whether `()`, `[]`, and `{}` are balanced and correctly nested.

**Answer:**

```ts
function validBrackets(text: string): boolean {
  const pairs: Record<string, string> = { ')': '(', ']': '[', '}': '{' };
  const stack: string[] = [];
  for (const character of text) {
    if ('([{'.includes(character)) stack.push(character);
    else if (stack.pop() !== pairs[character]) return false;
  }
  return stack.length === 0;
}
```

**Alternative:** Use a `Map` for the closing-to-opening lookup and keep the same stack algorithm.

```ts
function validBracketsWithMap(text: string): boolean {
  const pairs = new Map([[')', '('], [']', '['], ['}', '{']]);
  const stack: string[] = [];
  for (const character of text) {
    if ('([{'.includes(character)) stack.push(character);
    else if (stack.pop() !== pairs.get(character)) return false;
  }
  return stack.length === 0;
}
```

**Complexity:** O(n) time and O(n) space.

## 44. Flatten a Nested Array

**Question:** Recursively flatten an array containing nested arrays of arbitrary depth.

**Answer:**

```ts
type NestedValue<T> = T | readonly NestedValue<T>[];

function flattenDeep<T>(values: readonly NestedValue<T>[]): T[] {
  return values.reduce<T[]>(
    (result, value) => result.concat(Array.isArray(value) ? flattenDeep(value) : value as T),
    [],
  );
}
```

**Alternative:** Use the built-in `flat` method when the target library supports it.

```ts
const flattened = values.flat(Infinity);
```

**Complexity:** O(n) time and O(n + d) space, where d is nesting depth.

## 45. Binary Search

**Question:** Return the index of a target in an ascending sorted array, or `-1` when absent.

**Answer:**

```ts
function binarySearch(values: readonly number[], target: number): number {
  let low = 0;
  let high = values.length - 1;
  while (low <= high) {
    const middle = low + Math.floor((high - low) / 2);
    if (values[middle] === target) return middle;
    if (values[middle] < target) low = middle + 1;
    else high = middle - 1;
  }
  return -1;
}
```

**Alternative:** Implement the same divide-and-conquer search recursively.

```ts
function binarySearchRecursive(
  values: readonly number[],
  target: number,
  low = 0,
  high = values.length - 1,
): number {
  if (low > high) return -1;
  const middle = low + Math.floor((high - low) / 2);
  if (values[middle] === target) return middle;
  return values[middle] < target
    ? binarySearchRecursive(values, target, middle + 1, high)
    : binarySearchRecursive(values, target, low, middle - 1);
}
```

**Complexity:** O(log n) time. Iteration uses O(1) space; recursion uses O(log n) call-stack space.

## 46. Move Zeroes

**Question:** Move every numeric zero to the end of an array in place, preserving the relative order of non-zero values.

**Answer:**

```ts
function moveZeroes(values: number[]): number[] {
  let write = 0;
  for (const value of values) {
    if (value !== 0) values[write++] = value;
  }
  while (write < values.length) values[write++] = 0;
  return values;
}
```

**Alternative:** Partition non-zero values and zeros into temporary arrays, then copy them back.

```ts
function moveZeroesWithPartition(values: number[]): number[] {
  const ordered = values.filter((value) => value !== 0)
    .concat(values.filter((value) => value === 0));
  values.splice(0, values.length, ...ordered);
  return values;
}
```

**Complexity:** First solution is O(n) time/O(1) extra space; partitioning uses O(n) extra space.

## 47. Find the Missing Number from 1 to N

**Question:** An array contains distinct integers from `1` through `N`, with one number missing. The array length is `N - 1`.

**Answer:**

```ts
function missingNumber(values: readonly number[], n: number): number {
  return (n * (n + 1)) / 2 - values.reduce((sum, value) => sum + value, 0);
}
```

**Alternative:** XOR all numbers from 1 through N and all values in the array; matching values cancel.

```ts
function missingNumberWithXor(values: readonly number[], n: number): number {
  let result = 0;
  for (let value = 1; value <= n; value += 1) result ^= value;
  for (const value of values) result ^= value;
  return result;
}
```

**Complexity:** O(n) time and O(1) auxiliary space. The input must satisfy the stated range and uniqueness assumptions.

## 48. Intersection of Arrays

**Question:** Return the unique values shared by two arrays.

**Answer:**

```ts
function arrayIntersection<T>(left: readonly T[], right: readonly T[]): T[] {
  const rightValues = new Set(right);
  return [...new Set(left.filter((value) => rightValues.has(value)))];
}
```

**Alternative:** Filter the first array using `includes`, then deduplicate. This can take O(nm) time.

```ts
function arrayIntersectionByIncludes<T>(left: readonly T[], right: readonly T[]): T[] {
  return [...new Set(left.filter((value) => right.includes(value)))];
}
```

**Complexity:** Set-based solution takes O(n + m) expected time and O(m + k) space.

## 49. Rotate an Array to the Right

**Question:** Rotate a mutable array right by `k` positions in place. Treat negative or oversized `k` modulo the array length.

**Answer:**

```ts
function rotateRight<T>(values: T[], k: number): T[] {
  if (values.length === 0) return values;
  const steps = ((k % values.length) + values.length) % values.length;
  const reverse = (start: number, end: number): void => {
    while (start < end) {
      [values[start], values[end]] = [values[end], values[start]];
      start += 1;
      end -= 1;
    }
  };
  reverse(0, values.length - 1);
  reverse(0, steps - 1);
  reverse(steps, values.length - 1);
  return values;
}
```

**Alternative:** Copy the last `k` values and prepend them to the remaining values.

```ts
function rotateRightCopy<T>(values: readonly T[], k: number): T[] {
  if (values.length === 0) return [];
  const steps = ((k % values.length) + values.length) % values.length;
  return values.slice(-steps).concat(values.slice(0, values.length - steps));
}
```

**Complexity:** In-place reversal takes O(n) time/O(1) extra space; copying uses O(n) extra space.

## 50. Compress a String

**Question:** Run-length encode consecutive repeated characters, such as `"aaabbc"` to `"a3b2c1"`. Return the original if encoding does not shorten it.

**Answer:**

```ts
function compressString(text: string): string {
  let encoded = '';
  for (let index = 0; index < text.length;) {
    let end = index + 1;
    while (end < text.length && text[end] === text[index]) end += 1;
    encoded += `${text[index]}${end - index}`;
    index = end;
  }
  return encoded.length < text.length ? encoded : text;
}
```

**Alternative:** Store encoded runs in an array and join once.

```ts
function compressStringWithParts(text: string): string {
  const parts: string[] = [];
  for (let index = 0; index < text.length;) {
    let end = index + 1;
    while (end < text.length && text[end] === text[index]) end += 1;
    parts.push(`${text[index]}${end - index}`);
    index = end;
  }
  const encoded = parts.join('');
  return encoded.length < text.length ? encoded : text;
}
```

**Complexity:** O(n) time and O(n) output space.

## 51. Deep Clone an Object

**Question:** Clone an object with nested data without using `JSON.parse`.

**Answer:**

```ts
function deepClone<T>(value: T): T {
  return structuredClone(value);
}
```

**Alternative:** Recursively clone arrays and plain objects while preserving cycles. This does not cover every built-in class or custom prototype.

```ts
function deepClonePlain<T>(value: T, seen = new WeakMap<object, object>()): T {
  if (value === null || typeof value !== 'object') return value;
  if (seen.has(value)) return seen.get(value) as T;
  const copy: object = Array.isArray(value) ? [] : {};
  seen.set(value, copy);
  for (const key of Reflect.ownKeys(value)) {
    Object.defineProperty(copy, key, {
      value: deepClonePlain((value as Record<PropertyKey, unknown>)[key], seen),
      enumerable: true,
      configurable: true,
      writable: true,
    });
  }
  return copy as T;
}
```

**Complexity:** O(n) time and space for n reachable values. `structuredClone` supports many built-ins but not functions or arbitrary custom prototypes.

## 52. Implement a Map Method

**Question:** Implement the core behavior of `Array.prototype.map` using a loop. Preserve sparse-array holes and pass value, index, and source array to the callback.

**Answer:**

```ts
function myMap<T, U, This = undefined>(
  array: T[],
  callback: (this: This, value: T, index: number, source: T[]) => U,
  thisArg?: This,
): U[] {
  const result = new Array<U>(array.length);
  for (let index = 0; index < array.length; index += 1) {
    if (index in array) result[index] = callback.call(thisArg!, array[index], index, array);
  }
  return result;
}
```

**Alternative:** Use `forEach`, which also skips holes.

```ts
function myMapWithForEach<T, U>(
  array: T[],
  callback: (value: T, index: number, source: T[]) => U,
): U[] {
  const result = new Array<U>(array.length);
  array.forEach((value, index) => { result[index] = callback(value, index, array); });
  return result;
}
```

**Note:** This covers ordinary arrays, not every specification detail such as generic array-like receivers and species constructors.

## 53. Implement a Filter Method

**Question:** Implement the core behavior of `Array.prototype.filter` using a loop, including skipping sparse-array holes.

**Answer:**

```ts
function myFilter<T>(
  array: T[],
  predicate: (value: T, index: number, source: T[]) => unknown,
  thisArg?: unknown,
): T[] {
  const result: T[] = [];
  for (let index = 0; index < array.length; index += 1) {
    if (index in array && predicate.call(thisArg, array[index], index, array)) {
      result.push(array[index]);
    }
  }
  return result;
}
```

**Alternative:** Use the native `.filter()` method.

```ts
const selected = values.filter((value, index, source) => predicate(value, index, source));
```

**Note:** The custom version implements normal-array behavior, not all generic/species behavior of the built-in.

## 54. Implement a Reduce Method

**Question:** Implement the core behavior of `Array.prototype.reduce`, supporting an optional initial value and skipping sparse-array holes.

**Answer:**

```ts
function myReduce<T, U>(
  array: T[],
  callback: (accumulator: U, value: T, index: number, source: T[]) => U,
  initialValue: U,
): U;
function myReduce<T>(
  array: T[],
  callback: (accumulator: T, value: T, index: number, source: T[]) => T,
): T;
function myReduce<T, U>(
  array: T[],
  callback: (accumulator: U | T, value: T, index: number, source: T[]) => U | T,
  ...initial: [U?]
): U | T {
  let index = 0;
  let accumulator: U | T;
  if (initial.length > 0) accumulator = initial[0] as U;
  else {
    while (index < array.length && !(index in array)) index += 1;
    if (index >= array.length) throw new TypeError('Reduce of empty array');
    accumulator = array[index++];
  }
  for (; index < array.length; index += 1) {
    if (index in array) accumulator = callback(accumulator, array[index], index, array);
  }
  return accumulator;
}
```

**Alternative:** Use the native `.reduce()` method when a custom implementation is not required.

```ts
const total = values.reduce((sum, value) => sum + value, 0);
```

**Note:** The custom version handles ordinary arrays, including holes and an empty array without an initial value.

## 55. Build a Closure Counter

**Question:** Create a counter factory with private state and increment, decrement, and read operations.

**Answer:**

```ts
function createCounter(initialValue = 0): {
  increment: () => number;
  decrement: () => number;
  value: () => number;
} {
  let count = initialValue;
  return {
    increment: () => ++count,
    decrement: () => --count,
    value: () => count,
  };
}
```

**Alternative:** Encapsulate private state in a class with a private field.

```ts
class Counter {
  #count: number;
  constructor(initialValue = 0) { this.#count = initialValue; }
  increment(): number { return ++this.#count; }
  decrement(): number { return --this.#count; }
  value(): number { return this.#count; }
}
```

**Complexity:** Each operation takes O(1) time and space.

## 56. Debounce a Function

**Question:** Delay invocation until no call has occurred for the specified wait duration. Use the latest call's arguments and receiver.

**Answer:**

```ts
function debounce<This, Args extends unknown[]>(
  fn: (this: This, ...args: Args) => void,
  wait: number,
): (this: This, ...args: Args) => void {
  let timer: ReturnType<typeof setTimeout> | undefined;
  return function (this: This, ...args: Args): void {
    if (timer !== undefined) clearTimeout(timer);
    const context = this;
    timer = setTimeout(() => fn.apply(context, args), wait);
  };
}
```

**Alternative:** Use a wrapper with the same timer-reset behavior when callback `this` is not needed.

```ts
function debounceWithoutThis<Args extends unknown[]>(
  fn: (...args: Args) => void,
  wait: number,
): (...args: Args) => void {
  let timer: ReturnType<typeof setTimeout> | undefined;
  return (...args) => {
    if (timer !== undefined) clearTimeout(timer);
    timer = setTimeout(() => fn(...args), wait);
  };
}
```

**Complexity:** O(1) per call and O(1) timer state.

## 57. Throttle a Function

**Question:** Limit a function to at most one call per `wait` milliseconds, invoking immediately on the first call in each window.

**Answer:**

```ts
function throttle<This, Args extends unknown[]>(
  fn: (this: This, ...args: Args) => void,
  wait: number,
): (this: This, ...args: Args) => void {
  let lastRun = -Infinity;
  return function (this: This, ...args: Args): void {
    const now = Date.now();
    if (now - lastRun >= wait) {
      lastRun = now;
      fn.apply(this, args);
    }
  };
}
```

**Alternative:** Use a timer lock that reopens after each invocation.

```ts
function throttleWithTimer<Args extends unknown[]>(
  fn: (...args: Args) => void,
  wait: number,
): (...args: Args) => void {
  let locked = false;
  return (...args) => {
    if (locked) return;
    locked = true;
    fn(...args);
    setTimeout(() => { locked = false; }, wait);
  };
}
```

**Complexity:** O(1) time and O(1) state per call. These variants do not retain trailing calls.

## 58. Memoize a Function

**Question:** Cache function results by argument list so repeated calls with the same primitive arguments do not recompute the result.

**Answer:**

```ts
function memoize<Args extends readonly (string | number | boolean | null)[], Result>(
  fn: (...args: Args) => Result,
): (...args: Args) => Result {
  const cache = new Map<string, Result>();
  return (...args) => {
    const key = JSON.stringify(args) ?? 'undefined';
    if (!cache.has(key)) cache.set(key, fn(...args));
    return cache.get(key)!;
  };
}
```

**Alternative:** For one primitive argument, key a map directly by that value.

```ts
function memoizeUnary<Arg, Result>(fn: (value: Arg) => Result): (value: Arg) => Result {
  const cache = new Map<Arg, Result>();
  return (value) => {
    if (!cache.has(value)) cache.set(value, fn(value));
    return cache.get(value)!;
  };
}
```

**Note:** The JSON-key implementation is limited to JSON-safe arguments. Cache size and lifetime need consideration.

## 59. Curry a Function

**Question:** Transform a three-argument function `f(a, b, c)` into calls of the form `f(a)(b)(c)`.

**Answer:**

```ts
function curry3<A, B, C, R>(fn: (a: A, b: B, c: C) => R):
  (a: A) => (b: B) => (c: C) => R {
  return (a) => (b) => (c) => fn(a, b, c);
}
```

**Alternative:** Accumulate arguments until the function's declared arity is met.

```ts
function curry<Args extends unknown[], Result>(
  fn: (...args: Args) => Result,
  collected: unknown[] = [],
): (...args: unknown[]) => Result | ((...args: unknown[]) => unknown) {
  return (...args: unknown[]) => {
    const all = [...collected, ...args];
    return all.length >= fn.length
      ? fn(...(all as Args))
      : curry(fn, all);
  };
}
```

**Complexity:** O(1) per curried step, excluding the original function; accumulated arguments require O(n) space.

## 60. Flatten an Object

**Question:** Convert nested plain-object properties into dot-notated keys. Treat arrays and non-plain objects as leaf values.

**Answer:**

```ts
type FlatValue = unknown;

function flattenObject(
  object: Record<string, unknown>,
  prefix = '',
  result: Record<string, FlatValue> = {},
): Record<string, FlatValue> {
  for (const [key, value] of Object.entries(object)) {
    const path = prefix ? `${prefix}.${key}` : key;
    if (value !== null && Object.getPrototypeOf(value) === Object.prototype) {
      flattenObject(value as Record<string, unknown>, path, result);
    } else {
      result[path] = value;
    }
  }
  return result;
}
```

**Alternative:** Use an explicit stack to avoid recursion depth limits.

```ts
function flattenObjectIterative(object: Record<string, unknown>): Record<string, unknown> {
  const result: Record<string, unknown> = {};
  const stack: Array<[string, unknown]> = Object.entries(object);
  while (stack.length > 0) {
    const [path, value] = stack.pop()!;
    if (value !== null && Object.getPrototypeOf(value) === Object.prototype) {
      for (const [key, child] of Object.entries(value)) stack.push([`${path}.${key}`, child]);
    } else {
      result[path] = value;
    }
  }
  return result;
}
```

**Complexity:** O(p) time and space for p visited properties. Dot-containing keys can make paths ambiguous.

## 61. Simple Event Emitter

**Question:** Implement `.on()`, `.off()`, and `.emit()` for named events.

**Answer:**

```ts
type Listener = (...args: unknown[]) => void;

class EventEmitter {
  private readonly listeners = new Map<string, Set<Listener>>();

  on(event: string, listener: Listener): void {
    const listeners = this.listeners.get(event) ?? new Set<Listener>();
    listeners.add(listener);
    this.listeners.set(event, listeners);
  }

  off(event: string, listener: Listener): void {
    this.listeners.get(event)?.delete(listener);
  }

  emit(event: string, ...args: unknown[]): void {
    for (const listener of [...(this.listeners.get(event) ?? [])]) listener(...args);
  }
}
```

**Alternative:** Store listeners in arrays and remove a listener by filtering.

```ts
class ArrayEventEmitter {
  private readonly listeners = new Map<string, Listener[]>();
  on(event: string, listener: Listener): void {
    this.listeners.set(event, [...(this.listeners.get(event) ?? []), listener]);
  }
  off(event: string, listener: Listener): void {
    this.listeners.set(event, (this.listeners.get(event) ?? []).filter((item) => item !== listener));
  }
  emit(event: string, ...args: unknown[]): void {
    for (const listener of [...(this.listeners.get(event) ?? [])]) listener(...args);
  }
}
```

**Complexity:** O(k) to emit to k listeners; `Set` removal is expected O(1).

## 62. Transpose a Matrix

**Question:** Return the transpose of a rectangular 2D matrix, swapping rows and columns. Return an empty array for an empty matrix.

**Answer:**

```ts
function transpose<T>(matrix: readonly (readonly T[])[]): T[][] {
  if (matrix.length === 0) return [];
  return Array.from({ length: matrix[0].length }, (_, column) =>
    matrix.map((row) => row[column])
  );
}
```

**Alternative:** Use nested loops to construct each output row.

```ts
function transposeWithLoops<T>(matrix: readonly (readonly T[])[]): T[][] {
  if (matrix.length === 0) return [];
  const result: T[][] = [];
  for (let column = 0; column < matrix[0].length; column += 1) {
    const row: T[] = [];
    for (let sourceRow = 0; sourceRow < matrix.length; sourceRow += 1) {
      row.push(matrix[sourceRow][column]);
    }
    result.push(row);
  }
  return result;
}
```

**Complexity:** O(r × c) time and space. The matrix is assumed rectangular.

## 63. Collect Unique Substrings of Length K

**Question:** Return the distinct contiguous substrings of length `k`; return an empty array if `k` is not positive or exceeds the string length.

**Answer:**

```ts
function uniqueSubstrings(text: string, k: number): string[] {
  if (!Number.isInteger(k) || k <= 0 || k > text.length) return [];
  const result = new Set<string>();
  for (let index = 0; index <= text.length - k; index += 1) {
    result.add(text.slice(index, index + k));
  }
  return [...result];
}
```

**Alternative:** Generate windows with `Array.from` and deduplicate them.

```ts
function uniqueSubstringsWithArrayFrom(text: string, k: number): string[] {
  if (!Number.isInteger(k) || k <= 0 || k > text.length) return [];
  return [...new Set(Array.from(
    { length: text.length - k + 1 },
    (_, index) => text.slice(index, index + k),
  ))];
}
```

**Complexity:** O(nk) time to construct substrings and O(nk) space in the worst case.

## 64. Find All Duplicates

**Question:** Return each value that occurs more than once, once, in order of its second occurrence.

**Answer:**

```ts
function findAllDuplicates<T>(values: readonly T[]): T[] {
  const seen = new Set<T>();
  const duplicates = new Set<T>();
  for (const value of values) {
    if (seen.has(value)) duplicates.add(value);
    else seen.add(value);
  }
  return [...duplicates];
}
```

**Alternative:** Count values first, then select those with frequency greater than one.

```ts
function findDuplicatesByCounting<T>(values: readonly T[]): T[] {
  const counts = new Map<T, number>();
  for (const value of values) counts.set(value, (counts.get(value) ?? 0) + 1);
  return [...counts].filter(([, count]) => count > 1).map(([value]) => value);
}
```

**Complexity:** O(n) expected time and O(n) space.

## 65. Diff Two Arrays

**Question:** Return the unique values present in exactly one of two arrays (the symmetric difference).

**Answer:**

```ts
function diffArrays<T>(left: readonly T[], right: readonly T[]): T[] {
  const leftSet = new Set(left);
  const rightSet = new Set(right);
  return [...new Set([
    ...left.filter((value) => !rightSet.has(value)),
    ...right.filter((value) => !leftSet.has(value)),
  ])];
}
```

**Alternative:** Toggle membership in a `Set` while traversing both arrays.

```ts
function diffArraysByToggling<T>(left: readonly T[], right: readonly T[]): T[] {
  const result = new Set(left);
  for (const value of right) {
    if (result.has(value)) result.delete(value);
    else result.add(value);
  }
  return [...result];
}
```

**Complexity:** O(n + m) expected time and O(n + m) space.

## 66. Generate Pascal's Triangle

**Question:** Return the first `n` rows of Pascal's Triangle. For `n <= 0`, return an empty array.

**Answer:**

```ts
function pascalsTriangle(n: number): number[][] {
  const rows: number[][] = [];
  for (let rowIndex = 0; rowIndex < n; rowIndex += 1) {
    const row = Array<number>(rowIndex + 1).fill(1);
    for (let column = 1; column < rowIndex; column += 1) {
      row[column] = rows[rowIndex - 1][column - 1] + rows[rowIndex - 1][column];
    }
    rows.push(row);
  }
  return rows;
}
```

**Alternative:** Derive each value directly using binomial coefficients.

```ts
function pascalsTriangleByCombinations(n: number): number[][] {
  const rows: number[][] = [];
  for (let row = 0; row < n; row += 1) {
    const values = [1];
    for (let column = 1; column <= row; column += 1) {
      values[column] = values[column - 1] * (row - column + 1) / column;
    }
    rows.push(values);
  }
  return rows;
}
```

**Complexity:** O(n²) time and O(n²) space for the returned values.

## 67. Validate an IPv4 Address

**Question:** Return `true` if a string contains exactly four decimal IPv4 octets from 0 to 255. Reject leading zeroes except for `"0"`.

**Answer:**

```ts
function isValidIPv4(address: string): boolean {
  const parts = address.split('.');
  return parts.length === 4 && parts.every((part) =>
    /^(0|[1-9]\d{0,2})$/.test(part) && Number(part) <= 255
  );
}
```

**Alternative:** Parse and validate each part without a regular expression.

```ts
function isValidIPv4ByParsing(address: string): boolean {
  const parts = address.split('.');
  return parts.length === 4 && parts.every((part) => {
    if (part.length === 0 || (part.length > 1 && part[0] === '0')) return false;
    const value = Number(part);
    return Number.isInteger(value) && value >= 0 && value <= 255;
  });
}
```

**Complexity:** O(n) time and O(1) space for this fixed-size address.

## 68. Run-Length Encode a String

**Question:** Encode consecutive runs as character-count pairs, for example `"aaabbc"` as `"a3b2c1"`.

**Answer:**

```ts
function runLengthEncode(text: string): string {
  const parts: string[] = [];
  for (let index = 0; index < text.length;) {
    let end = index + 1;
    while (end < text.length && text[end] === text[index]) end += 1;
    parts.push(`${text[index]}${end - index}`);
    index = end;
  }
  return parts.join('');
}
```

**Alternative:** Match consecutive character runs with a regular expression.

```ts
function runLengthEncodeWithRegex(text: string): string {
  return (text.match(/(.)\1*/gs) ?? [])
    .map((run) => `${run[0]}${run.length}`)
    .join('');
}
```

**Complexity:** O(n) time and O(n) output space. The regex operates on UTF-16 code units.

## 69. Caesar Cipher

**Question:** Shift each English letter by `k` places, wrapping around the alphabet, preserving case, and leaving non-letters unchanged.

**Answer:**

```ts
function caesarCipher(text: string, shift: number): string {
  const offset = ((shift % 26) + 26) % 26;
  return Array.from(text, (character) => {
    const code = character.charCodeAt(0);
    const base = code >= 65 && code <= 90 ? 65 : code >= 97 && code <= 122 ? 97 : null;
    return base === null
      ? character
      : String.fromCharCode(((code - base + offset) % 26) + base);
  }).join('');
}
```

**Alternative:** Use uppercase and lowercase alphabet lookup strings.

```ts
function caesarCipherByLookup(text: string, shift: number): string {
  const lower = 'abcdefghijklmnopqrstuvwxyz';
  const upper = lower.toUpperCase();
  const offset = ((shift % 26) + 26) % 26;
  return Array.from(text, (character) => {
    const alphabet = character >= 'A' && character <= 'Z' ? upper : lower;
    const index = alphabet.indexOf(character);
    return index < 0 ? character : alphabet[(index + offset) % 26];
  }).join('');
}
```

**Complexity:** O(n) time and O(n) output space.

## 70. Find the First Unique Character

**Question:** Return the first character that occurs exactly once, or `null` if no such character exists.

**Answer:**

```ts
function firstUniqueCharacter(text: string): string | null {
  const counts = new Map<string, number>();
  for (const character of text) {
    counts.set(character, (counts.get(character) ?? 0) + 1);
  }
  for (const character of text) {
    if (counts.get(character) === 1) return character;
  }
  return null;
}
```

**Alternative:** Search each character's first and last positions; this may take O(n²).

```ts
function firstUniqueCharacterBySearch(text: string): string | null {
  for (const character of text) {
    if (text.indexOf(character) === text.lastIndexOf(character)) return character;
  }
  return null;
}
```

**Complexity:** O(n) time and O(k) space for k distinct characters.

## 71. Group Items by a Key

**Question:** Group objects by the value returned by a key selector, preserving key types.

**Answer:**

```ts
function groupBy<T, K>(items: readonly T[], keySelector: (item: T) => K): Map<K, T[]> {
  const groups = new Map<K, T[]>();
  for (const item of items) {
    const key = keySelector(item);
    const group = groups.get(key) ?? [];
    group.push(item);
    groups.set(key, group);
  }
  return groups;
}
```

**Alternative:** Use `reduce` to build the map.

```ts
function groupByWithReduce<T, K>(
  items: readonly T[],
  keySelector: (item: T) => K,
): Map<K, T[]> {
  return items.reduce((groups, item) => {
    const key = keySelector(item);
    const group = groups.get(key) ?? [];
    group.push(item);
    groups.set(key, group);
    return groups;
  }, new Map<K, T[]>());
}
```

**Complexity:** O(n) expected time and O(n) space.

## 72. Implement Power Without `Math.pow` or `**`

**Question:** Compute `base` raised to an integer exponent without `Math.pow()` or the exponentiation operator. Reject zero to a negative exponent.

**Answer:**

```ts
function power(base: number, exponent: number): number {
  if (!Number.isInteger(exponent)) throw new RangeError('exponent must be an integer');
  if (base === 0 && exponent < 0) throw new RangeError('zero cannot have a negative exponent');
  let result = 1;
  let factor = base;
  let remaining = Math.abs(exponent);
  while (remaining > 0) {
    if (remaining % 2 === 1) result *= factor;
    factor *= factor;
    remaining = Math.floor(remaining / 2);
  }
  return exponent < 0 ? 1 / result : result;
}
```

**Alternative:** Multiply by the base repeatedly; this is simpler but O(|exponent|).

```ts
function powerByMultiplication(base: number, exponent: number): number {
  if (!Number.isInteger(exponent)) throw new RangeError('exponent must be an integer');
  if (base === 0 && exponent < 0) throw new RangeError('zero cannot have a negative exponent');
  let result = 1;
  for (let index = 0; index < Math.abs(exponent); index += 1) result *= base;
  return exponent < 0 ? 1 / result : result;
}
```

**Complexity:** Exponentiation by squaring takes O(log |exponent|) time and O(1) space.

## 73. Deep Equality

**Question:** Compare nested arrays and plain objects for structural equality, including recursively nested values.

**Answer:**

```ts
function deepEqual(left: unknown, right: unknown): boolean {
  if (Object.is(left, right)) return true;
  if (left === null || right === null || typeof left !== 'object' || typeof right !== 'object') {
    return false;
  }
  if (Array.isArray(left) !== Array.isArray(right)) return false;
  const leftKeys = Reflect.ownKeys(left);
  const rightKeys = Reflect.ownKeys(right);
  if (leftKeys.length !== rightKeys.length) return false;
  const rightRecord = right as Record<PropertyKey, unknown>;
  const leftRecord = left as Record<PropertyKey, unknown>;
  return leftKeys.every((key) =>
    Object.hasOwn(right, key) && deepEqual(leftRecord[key], rightRecord[key])
  );
}
```

**Alternative:** Compare JSON serializations only for JSON-safe values with controlled property ordering.

```ts
function deepEqualJsonSafe(left: unknown, right: unknown): boolean {
  return JSON.stringify(left) === JSON.stringify(right);
}
```

**Note:** The recursive version is for acyclic arrays/objects; cycles and special built-ins need additional handling. JSON comparison is not general deep equality.

## 74. Parse URL Query Parameters

**Question:** Parse a URL's query string into an object. Preserve repeated parameter names as arrays.

**Answer:**

```ts
type QueryValue = string | string[];

function parseQuery(url: string): Record<string, QueryValue> {
  const params = new URL(url, 'https://example.invalid').searchParams;
  const result = Object.create(null) as Record<string, QueryValue>;
  for (const [key, value] of params) {
    const previous = result[key];
    if (previous === undefined) result[key] = value;
    else result[key] = Array.isArray(previous) ? [...previous, value] : [previous, value];
  }
  return result;
}
```

**Alternative:** Return `URLSearchParams` directly when a structured object is not required.

```ts
function getQueryParams(url: string): URLSearchParams {
  return new URL(url, 'https://example.invalid').searchParams;
}
```

**Complexity:** O(p) time and space for p query parameters. Values remain strings; bracket notation is not interpreted as nested objects.

## 75. Climbing Stairs

**Question:** Count the distinct ways to reach step `n` when each move is either one or two steps. Define `n = 0` as one way.

**Answer:**

```ts
function climbingStairs(n: number): number {
  if (!Number.isInteger(n) || n < 0) throw new RangeError('n must be non-negative');
  let previous = 1;
  let current = 1;
  for (let step = 2; step <= n; step += 1) {
    [previous, current] = [current, previous + current];
  }
  return n === 0 ? 1 : current;
}
```

**Alternative:** Use memoized recursion based on the two possible last moves.

```ts
function climbingStairsMemoized(n: number, memo = new Map([[0, 1], [1, 1]])): number {
  if (!Number.isInteger(n) || n < 0) throw new RangeError('n must be non-negative');
  if (!memo.has(n)) {
    memo.set(n, climbingStairsMemoized(n - 1, memo) + climbingStairsMemoized(n - 2, memo));
  }
  return memo.get(n)!;
}
```

**Complexity:** Iteration takes O(n) time and O(1) space; memoized recursion takes O(n) space.

## 76. Maximum Sum Subarray

**Question:** Find a non-empty contiguous subarray with the greatest sum. Return the sum and inclusive start/end indices.

**Answer:**

```ts
interface MaximumSubarrayResult {
  sum: number;
  start: number;
  end: number;
}

function maximumSubarray(values: readonly number[]): MaximumSubarrayResult {
  if (values.length === 0) throw new RangeError('values must not be empty');
  let current = values[0];
  let best = values[0];
  let start = 0;
  let bestStart = 0;
  let bestEnd = 0;
  for (let index = 1; index < values.length; index += 1) {
    if (values[index] > current + values[index]) {
      current = values[index];
      start = index;
    } else {
      current += values[index];
    }
    if (current > best) {
      best = current;
      bestStart = start;
      bestEnd = index;
    }
  }
  return { sum: best, start: bestStart, end: bestEnd };
}
```

**Alternative:** Return only the maximum sum using Kadane's recurrence.

```ts
function maximumSubarraySum(values: readonly number[]): number {
  if (values.length === 0) throw new RangeError('values must not be empty');
  let current = values[0];
  let best = current;
  for (const value of values.slice(1)) {
    current = Math.max(value, current + value);
    best = Math.max(best, current);
  }
  return best;
}
```

**Complexity:** O(n) time and O(1) auxiliary space.

## 77. Search a Sorted 2D Matrix

**Question:** Search a matrix whose rows and columns are each ascending. Return `true` if the target is present.

**Answer:**

```ts
function searchSortedMatrix(matrix: readonly (readonly number[])[], target: number): boolean {
  if (matrix.length === 0 || matrix[0].length === 0) return false;
  let row = 0;
  let column = matrix[0].length - 1;
  while (row < matrix.length && column >= 0) {
    const value = matrix[row][column];
    if (value === target) return true;
    if (value > target) column -= 1;
    else row += 1;
  }
  return false;
}
```

**Alternative:** Binary-search each row independently.

```ts
function searchMatrixByRows(matrix: readonly (readonly number[])[], target: number): boolean {
  return matrix.some((row) => {
    let low = 0;
    let high = row.length - 1;
    while (low <= high) {
      const middle = low + Math.floor((high - low) / 2);
      if (row[middle] === target) return true;
      if (row[middle] < target) low = middle + 1;
      else high = middle - 1;
    }
    return false;
  });
}
```

**Complexity:** Staircase search takes O(rows + columns); row-wise binary search takes O(rows × log(columns)).

## 78. Capitalize Selected Nested String Paths

**Question:** Given a nested object and dot-separated paths, uppercase the first character of each targeted string value without mutating the input.

**Answer:**

```ts
function capitalizePaths<T extends Record<string, unknown>>(
  source: T,
  paths: readonly string[],
): T {
  const result = structuredClone(source);
  for (const path of paths) {
    const keys = path.split('.');
    let parent: Record<string, unknown> | undefined = result;
    for (const key of keys.slice(0, -1)) {
      const child: unknown = parent?.[key];
      parent = child !== null && typeof child === 'object'
        ? child as Record<string, unknown>
        : undefined;
    }
    const lastKey = keys[keys.length - 1];
    const value = parent?.[lastKey];
    if (typeof value === 'string') {
      parent![lastKey] = value.charAt(0).toUpperCase() + value.slice(1);
    }
  }
  return result;
}
```

**Alternative:** Recursively capitalize values for selected leaf keys rather than full paths.

```ts
function capitalizeSelectedKeys(
  value: unknown,
  selectedKeys: ReadonlySet<string>,
): unknown {
  if (Array.isArray(value)) return value.map((item) => capitalizeSelectedKeys(item, selectedKeys));
  if (value === null || typeof value !== 'object') return value;
  return Object.fromEntries(Object.entries(value).map(([key, child]) => {
    if (selectedKeys.has(key) && typeof child === 'string') {
      return [key, child.charAt(0).toUpperCase() + child.slice(1)];
    }
    return [key, capitalizeSelectedKeys(child, selectedKeys)];
  }));
}
```

**Complexity:** Work is proportional to the cloned object size plus path lengths.

## 79. Product of Array Except Self

**Question:** Return an array where each index contains the product of every input value except the value at that index. Do not use division.

**Answer:**

```ts
function productExceptSelf(values: readonly number[]): number[] {
  const result = Array<number>(values.length).fill(1);
  let prefix = 1;
  for (let index = 0; index < values.length; index += 1) {
    result[index] = prefix;
    prefix *= values[index];
  }
  let suffix = 1;
  for (let index = values.length - 1; index >= 0; index -= 1) {
    result[index] *= suffix;
    suffix *= values[index];
  }
  return result;
}
```

**Alternative:** Multiply every value except the current index. This is straightforward but O(n²).

```ts
function productExceptSelfBruteForce(values: readonly number[]): number[] {
  return values.map((_, excluded) =>
    values.reduce((product, value, index) => index === excluded ? product : product * value, 1)
  );
}
```

**Complexity:** Prefix/suffix solution takes O(n) time and O(1) extra space excluding output.

## 80. Convert Roman Numerals to an Integer

**Question:** Convert a valid canonical Roman numeral using `I, V, X, L, C, D, M` into an integer.

**Answer:**

```ts
function romanToInteger(roman: string): number {
  const values: Record<string, number> = { I: 1, V: 5, X: 10, L: 50, C: 100, D: 500, M: 1000 };
  let total = 0;
  for (let index = 0; index < roman.length; index += 1) {
    const current = values[roman[index]];
    const next = values[roman[index + 1]] ?? 0;
    total += current < next ? -current : current;
  }
  return total;
}
```

**Alternative:** Scan right to left, subtracting values smaller than the greatest value already seen.

```ts
function romanToIntegerRightToLeft(roman: string): number {
  const values: Record<string, number> = { I: 1, V: 5, X: 10, L: 50, C: 100, D: 500, M: 1000 };
  let total = 0;
  let greatest = 0;
  for (let index = roman.length - 1; index >= 0; index -= 1) {
    const value = values[roman[index]];
    total += value < greatest ? -value : value;
    greatest = Math.max(greatest, value);
  }
  return total;
}
```

**Note:** Conversion assumes valid input; canonical Roman numeral syntax needs separate validation.

**Complexity:** O(n) time and O(1) auxiliary space.

## 81. Print a Matrix in Clockwise Spiral Order

**Question:** Return the elements of a rectangular matrix in clockwise spiral order.

**Answer:**

```ts
function spiralOrder<T>(matrix: readonly (readonly T[])[]): T[] {
  if (matrix.length === 0 || matrix[0].length === 0) return [];
  let top = 0;
  let bottom = matrix.length - 1;
  let left = 0;
  let right = matrix[0].length - 1;
  const result: T[] = [];
  while (top <= bottom && left <= right) {
    for (let column = left; column <= right; column += 1) result.push(matrix[top][column]);
    top += 1;
    for (let row = top; row <= bottom; row += 1) result.push(matrix[row][right]);
    right -= 1;
    if (top <= bottom) {
      for (let column = right; column >= left; column -= 1) result.push(matrix[bottom][column]);
      bottom -= 1;
    }
    if (left <= right) {
      for (let row = bottom; row >= top; row -= 1) result.push(matrix[row][left]);
      left += 1;
    }
  }
  return result;
}
```

**Alternative:** Repeatedly take the top row, rotate the remaining matrix counterclockwise, and continue. This allocates arrays repeatedly.

```ts
function spiralOrderByRotation<T>(matrix: readonly (readonly T[])[]): T[] {
  const result: T[] = [];
  let remaining = matrix.map((row) => [...row]);
  while (remaining.length > 0 && remaining[0].length > 0) {
    result.push(...remaining.shift()!);
    remaining = remaining[0]?.map((_, column) =>
      remaining.map((row) => row[row.length - 1 - column])
    ) ?? [];
  }
  return result;
}
```

**Complexity:** Boundary traversal takes O(r × c) time and O(1) auxiliary space excluding output.

## 82. Implement a `Promise.all` Alternative

**Question:** Accept an iterable of values/promises, preserve result order, resolve when all fulfill, and reject on the first rejection.

**Answer:**

```ts
function promiseAll<T>(iterable: Iterable<T | PromiseLike<T>>): Promise<T[]> {
  return new Promise((resolve, reject) => {
    const items = Array.from(iterable);
    if (items.length === 0) { resolve([]); return; }
    const results = new Array<T>(items.length);
    let remaining = items.length;
    items.forEach((item, index) => {
      Promise.resolve(item).then((value) => {
        results[index] = value;
        if (--remaining === 0) resolve(results);
      }, reject);
    });
  });
}
```

**Alternative:** Use an async function and await each item in a loop.

```ts
async function promiseAllSequential<T>(iterable: Iterable<T | PromiseLike<T>>): Promise<T[]> {
  const results: T[] = [];
  for (const item of iterable) results.push(await item);
  return results;
}
```

**Note:** The alternative is sequential and does not match concurrent `Promise.all` timing.

## 83. Implement a `Promise.race` Alternative

**Question:** Resolve or reject with the first settled promise from an iterable. An empty iterable remains pending.

**Answer:**

```ts
function promiseRace<T>(iterable: Iterable<T | PromiseLike<T>>): Promise<T> {
  return new Promise((resolve, reject) => {
    for (const item of iterable) Promise.resolve(item).then(resolve, reject);
  });
}
```

**Alternative:** Normalize the iterable to an array before registering settlement handlers.

```ts
function promiseRaceArray<T>(iterable: Iterable<T | PromiseLike<T>>): Promise<T> {
  return new Promise((resolve, reject) => {
    Array.from(iterable).forEach((item) => Promise.resolve(item).then(resolve, reject));
  });
}
```

**Note:** Both preserve pending behavior for an empty iterable and assimilate thenables with `Promise.resolve`.

## 84. Run Promise Tasks Sequentially

**Question:** Execute an array of asynchronous task functions one after another, passing each task its index and collecting results in order.

**Answer:**

```ts
async function runSequentially<T>(tasks: readonly ((index: number) => Promise<T>)[]): Promise<T[]> {
  const results: T[] = [];
  for (let index = 0; index < tasks.length; index += 1) results.push(await tasks[index](index));
  return results;
}
```

**Alternative:** Reduce the task list into a promise chain.

```ts
function runSequentiallyWithReduce<T>(
  tasks: readonly ((index: number) => Promise<T>)[],
): Promise<T[]> {
  return tasks.reduce(
    (chain, task, index) => chain.then(async (results) => [...results, await task(index)]),
    Promise.resolve([] as T[]),
  );
}
```

**Complexity:** O(n) task dispatches; tasks run serially and any rejection stops the sequence.

## 85. Retry an Asynchronous Task

**Question:** Retry a promise-returning task up to `retries` additional times, waiting `delayMs` between attempts.

**Answer:**

```ts
async function retry<T>(task: () => Promise<T>, retries: number, delayMs: number): Promise<T> {
  for (let attempt = 0; ; attempt += 1) {
    try { return await task(); }
    catch (error) {
      if (attempt >= retries) throw error;
      await new Promise<void>((resolve) => setTimeout(resolve, delayMs));
    }
  }
}
```

**Alternative:** Use exponential backoff.

```ts
async function retryWithBackoff<T>(
  task: () => Promise<T>, retries: number, baseDelayMs: number,
): Promise<T> {
  for (let attempt = 0; ; attempt += 1) {
    try { return await task(); }
    catch (error) {
      if (attempt >= retries) throw error;
      await new Promise<void>((resolve) => setTimeout(resolve, baseDelayMs * 2 ** attempt));
    }
  }
}
```

**Note:** `retries` counts retries after the initial attempt. Production network retries should consider cancellation and retryable error types.

## 86. Implement an LRU Cache

**Question:** Implement a least-recently-used cache with a positive capacity. Reads and writes refresh recency; evict the least recently used entry when full.

**Answer:**

```ts
class LRUCache<K, V> {
  private readonly entries = new Map<K, V>();
  constructor(private readonly capacity: number) {
    if (!Number.isInteger(capacity) || capacity < 1) throw new RangeError('capacity must be positive');
  }
  get(key: K): V | undefined {
    if (!this.entries.has(key)) return undefined;
    const value = this.entries.get(key)!;
    this.entries.delete(key);
    this.entries.set(key, value);
    return value;
  }
  put(key: K, value: V): void {
    this.entries.delete(key);
    this.entries.set(key, value);
    if (this.entries.size > this.capacity) {
      const oldest = this.entries.keys().next();
      if (!oldest.done) this.entries.delete(oldest.value);
    }
  }
}
```

**Alternative:** Use a doubly linked list plus a map from keys to list nodes for explicit O(1) recency updates and eviction.

```ts
// Keep sentinel head/tail nodes; move accessed nodes to the head and evict
// the node immediately before the tail when the capacity is exceeded.
```

**Complexity:** `Map` operations are expected O(1); storage is bounded by capacity.

## 87. Longest Substring Without Repeating Characters

**Question:** Return the length of the longest contiguous substring containing no repeated characters.

**Answer:**

```ts
function longestUniqueSubstringLength(text: string): number {
  const lastSeen = new Map<string, number>();
  let start = 0;
  let longest = 0;
  for (let index = 0; index < text.length; index += 1) {
    const previous = lastSeen.get(text[index]);
    if (previous !== undefined && previous >= start) start = previous + 1;
    lastSeen.set(text[index], index);
    longest = Math.max(longest, index - start + 1);
  }
  return longest;
}
```

**Alternative:** Maintain a set for the active window and remove from its left edge until unique.

```ts
function longestUniqueSubstringWithSet(text: string): number {
  const window = new Set<string>();
  let start = 0;
  let longest = 0;
  for (let end = 0; end < text.length; end += 1) {
    while (window.has(text[end])) window.delete(text[start++]);
    window.add(text[end]);
    longest = Math.max(longest, end - start + 1);
  }
  return longest;
}
```

**Complexity:** O(n) time and O(k) space for k distinct characters.

## 88. Merge Overlapping Intervals

**Question:** Merge overlapping `[start, end]` intervals and return them sorted by start.

**Answer:**

```ts
type Interval = [number, number];
function mergeIntervals(intervals: readonly Interval[]): Interval[] {
  const sorted = intervals.map(([start, end]) => [start, end] as Interval)
    .sort((a, b) => a[0] - b[0]);
  const merged: Interval[] = [];
  for (const interval of sorted) {
    const last = merged[merged.length - 1];
    if (!last || interval[0] > last[1]) merged.push(interval);
    else last[1] = Math.max(last[1], interval[1]);
  }
  return merged;
}
```

**Alternative:** Sort a copied array and merge into output with a loop, preserving the caller's input.

```ts
function mergeIntervalsAlternative(intervals: readonly Interval[]): Interval[] {
  const sorted = [...intervals].sort((a, b) => a[0] - b[0]);
  const result: Interval[] = [];
  for (const [start, end] of sorted) {
    const last = result[result.length - 1];
    if (last && start <= last[1]) last[1] = Math.max(last[1], end);
    else result.push([start, end]);
  }
  return result;
}
```

**Complexity:** O(n log n) time from sorting and O(n) output space.

## 89. Three Sum

**Question:** Return unique triplets of values whose sum is zero.

**Answer:**

```ts
function threeSum(values: readonly number[]): number[][] {
  const sorted = [...values].sort((a, b) => a - b);
  const result: number[][] = [];
  for (let first = 0; first < sorted.length - 2; first += 1) {
    if (first > 0 && sorted[first] === sorted[first - 1]) continue;
    let left = first + 1;
    let right = sorted.length - 1;
    while (left < right) {
      const sum = sorted[first] + sorted[left] + sorted[right];
      if (sum === 0) {
        result.push([sorted[first], sorted[left], sorted[right]]);
        left += 1; right -= 1;
        while (left < right && sorted[left] === sorted[left - 1]) left += 1;
        while (left < right && sorted[right] === sorted[right + 1]) right -= 1;
      } else if (sum < 0) left += 1;
      else right -= 1;
    }
  }
  return result;
}
```

**Alternative:** Enumerate all triples, sort each matching triple, and deduplicate by a string key.

```ts
function threeSumBruteForce(values: readonly number[]): number[][] {
  const result = new Map<string, number[]>();
  for (let a = 0; a < values.length; a += 1) {
    for (let b = a + 1; b < values.length; b += 1) {
      for (let c = b + 1; c < values.length; c += 1) {
        if (values[a] + values[b] + values[c] === 0) {
          const triplet = [values[a], values[b], values[c]].sort((x, y) => x - y);
          result.set(triplet.join(','), triplet);
        }
      }
    }
  }
  return [...result.values()];
}
```

**Complexity:** Two-pointer solution takes O(n²) time and O(n) space for sorting/output.

## 90. Container With Most Water

**Question:** Given non-negative heights, return the maximum area between two vertical lines.

**Answer:**

```ts
function maxContainerArea(heights: readonly number[]): number {
  let left = 0;
  let right = heights.length - 1;
  let area = 0;
  while (left < right) {
    area = Math.max(area, (right - left) * Math.min(heights[left], heights[right]));
    if (heights[left] < heights[right]) left += 1;
    else right -= 1;
  }
  return area;
}
```

**Alternative:** Check every pair of boundaries.

```ts
function maxContainerAreaBruteForce(heights: readonly number[]): number {
  let area = 0;
  for (let left = 0; left < heights.length; left += 1) {
    for (let right = left + 1; right < heights.length; right += 1) {
      area = Math.max(area, (right - left) * Math.min(heights[left], heights[right]));
    }
  }
  return area;
}
```

**Complexity:** Two-pointer solution takes O(n) time and O(1) space.

## 91. Implement a Trie

**Question:** Create a prefix tree with insert, exact-word search, and prefix search.

**Answer:**

```ts
class TrieNode {
  readonly children = new Map<string, TrieNode>();
  isWord = false;
}
class Trie {
  private readonly root = new TrieNode();
  insert(word: string): void {
    let node = this.root;
    for (const character of word) {
      if (!node.children.has(character)) node.children.set(character, new TrieNode());
      node = node.children.get(character)!;
    }
    node.isWord = true;
  }
  private find(text: string): TrieNode | undefined {
    let node = this.root;
    for (const character of text) {
      const child = node.children.get(character);
      if (!child) return undefined;
      node = child;
    }
    return node;
  }
  search(word: string): boolean { return this.find(word)?.isWord ?? false; }
  startsWith(prefix: string): boolean { return this.find(prefix) !== undefined; }
}
```

**Alternative:** Use nested records keyed by characters and a terminal marker such as `$word`.

```ts
// This uses the same traversal with Record<string, TrieRecord>; set node.$word
// after inserting a full word and test that marker for exact search.
type TrieRecord = { [key: string]: TrieRecord | boolean };
```

**Complexity:** O(L) per operation for a string of length L; storage is proportional to inserted prefixes.

## 92. Detect a Cycle in a Directed Graph

**Question:** Detect whether a directed graph represented as `Map<T, T[]>` contains a cycle.

**Answer:**

```ts
function hasDirectedCycle<T>(graph: ReadonlyMap<T, readonly T[]>): boolean {
  const visiting = new Set<T>();
  const visited = new Set<T>();
  const visit = (node: T): boolean => {
    if (visiting.has(node)) return true;
    if (visited.has(node)) return false;
    visiting.add(node);
    for (const neighbor of graph.get(node) ?? []) if (visit(neighbor)) return true;
    visiting.delete(node);
    visited.add(node);
    return false;
  };
  for (const node of graph.keys()) if (visit(node)) return true;
  return false;
}
```

**Alternative:** Use iterative DFS with explicit stack frames and visitation states to avoid recursive call-stack limits.

```ts
// Track nodes as unseen, active, or complete. Encountering an active node
// during traversal means a cycle; mark a node complete after all neighbors.
```

**Complexity:** O(V + E) time and O(V) space.

## 93. Validate a Binary Search Tree

**Question:** Validate a binary tree under the strict BST rule: left values are smaller and right values are larger.

**Answer:**

```ts
interface TreeNode { value: number; left: TreeNode | null; right: TreeNode | null }
function isValidBST(root: TreeNode | null): boolean {
  function validate(node: TreeNode | null, lower: number, upper: number): boolean {
    if (!node) return true;
    if (node.value <= lower || node.value >= upper) return false;
    return validate(node.left, lower, node.value) && validate(node.right, node.value, upper);
  }
  return validate(root, -Infinity, Infinity);
}
```

**Alternative:** Perform iterative in-order traversal and check strict monotonic increase.

```ts
function isValidBSTInOrder(root: TreeNode | null): boolean {
  const stack: TreeNode[] = [];
  let node = root;
  let previous = -Infinity;
  while (node || stack.length) {
    while (node) { stack.push(node); node = node.left; }
    node = stack.pop()!;
    if (node.value <= previous) return false;
    previous = node.value;
    node = node.right;
  }
  return true;
}
```

**Complexity:** O(n) time and O(h) space for tree height h.

## 94. Edit Distance (Levenshtein)

**Question:** Return the minimum number of insertions, deletions, and substitutions needed to transform one string into another.

**Answer:**

```ts
function editDistance(left: string, right: string): number {
  let previous = Array.from({ length: right.length + 1 }, (_, index) => index);
  for (let i = 1; i <= left.length; i += 1) {
    const current = [i];
    for (let j = 1; j <= right.length; j += 1) {
      current[j] = left[i - 1] === right[j - 1] ? previous[j - 1]
        : 1 + Math.min(previous[j], current[j - 1], previous[j - 1]);
    }
    previous = current;
  }
  return previous[right.length];
}
```

**Alternative:** Use a complete two-dimensional dynamic-programming table.

```ts
function editDistanceTable(left: string, right: string): number {
  const dp = Array.from({ length: left.length + 1 }, () => Array<number>(right.length + 1).fill(0));
  for (let i = 0; i <= left.length; i += 1) dp[i][0] = i;
  for (let j = 0; j <= right.length; j += 1) dp[0][j] = j;
  for (let i = 1; i <= left.length; i += 1) for (let j = 1; j <= right.length; j += 1) {
    dp[i][j] = left[i - 1] === right[j - 1] ? dp[i - 1][j - 1]
      : 1 + Math.min(dp[i - 1][j], dp[i][j - 1], dp[i - 1][j - 1]);
  }
  return dp[left.length][right.length];
}
```

**Complexity:** O(mn) time; rolling rows use O(n) space, full table O(mn).

## 95. Rate Limiter

**Question:** Allow at most `limit` actions per client within a rolling time window.

**Answer:**

```ts
function createRateLimiter(limit: number, windowMs: number, now = Date.now): (id: string) => boolean {
  const timestamps = new Map<string, number[]>();
  return (clientId) => {
    const cutoff = now() - windowMs;
    const recent = (timestamps.get(clientId) ?? []).filter((time) => time > cutoff);
    if (recent.length >= limit) { timestamps.set(clientId, recent); return false; }
    recent.push(now());
    timestamps.set(clientId, recent);
    return true;
  };
}
```

**Alternative:** Use a token bucket with configurable refill rate.

```ts
function createTokenBucket(capacity: number, refillPerMs: number, now = Date.now) {
  const buckets = new Map<string, { tokens: number; time: number }>();
  return (id: string): boolean => {
    const time = now();
    const bucket = buckets.get(id) ?? { tokens: capacity, time };
    bucket.tokens = Math.min(capacity, bucket.tokens + (time - bucket.time) * refillPerMs);
    bucket.time = time;
    if (bucket.tokens < 1) { buckets.set(id, bucket); return false; }
    bucket.tokens -= 1;
    buckets.set(id, bucket);
    return true;
  };
}
```

**Complexity:** Rolling-window work depends on stored timestamps; token-bucket operations are O(1).

## 96. Promisify a Node-Style Callback

**Question:** Convert an error-first callback API `(error, value)` into a function returning a promise.

**Answer:**

```ts
function promisify<Args extends unknown[], Result>(
  fn: (...args: [...Args, (error: Error | null, value: Result) => void]) => void,
): (...args: Args) => Promise<Result> {
  return (...args) => new Promise((resolve, reject) => {
    fn(...args, (error, value) => error ? reject(error) : resolve(value));
  });
}
```

**Alternative:** Wrap a specific callback API at its call site.

```ts
function readAsPromise(
  readFile: (path: string, callback: (error: Error | null, data: string) => void) => void,
  path: string,
): Promise<string> {
  return new Promise((resolve, reject) => {
    readFile(path, (error, data) => error ? reject(error) : resolve(data));
  });
}
```

**Note:** The generic wrapper assumes one success value and no special `this` binding or abort behavior.

## 97. Generate an Infinite Sequence

**Question:** Create a generator that yields an unbounded arithmetic sequence from a start value and step.

**Answer:**

```ts
function* arithmeticSequence(start = 0, step = 1): Generator<number, never, unknown> {
  for (let value = start; ; value += step) yield value;
}
```

**Alternative:** Implement the iterator protocol directly.

```ts
function arithmeticIterator(start = 0, step = 1): IterableIterator<number> {
  let value = start;
  return {
    next: () => {
      const current = value;
      value += step;
      return { value: current, done: false as const };
    },
    [Symbol.iterator]() { return this; },
  };
}
```

**Note:** Consume only a bounded number of values from an infinite iterator.

## 98. Validate Assignments with a Proxy

**Question:** Create a proxy that rejects property assignments not satisfying a validation rule.

**Answer:**

```ts
function validatedObject<T extends object>(
  target: T,
  validate: (property: PropertyKey, value: unknown) => boolean,
): T {
  return new Proxy(target, {
    set(object, property, value, receiver) {
      if (!validate(property, value)) throw new TypeError(`Invalid value for ${String(property)}`);
      return Reflect.set(object, property, value, receiver);
    },
  });
}
```

**Alternative:** Define a setter for a known property.

```ts
function createPositiveValue() {
  let value = 0;
  return Object.defineProperty({}, 'value', {
    get: () => value,
    set(next: number) {
      if (typeof next !== 'number' || next < 0) throw new TypeError('value must be non-negative');
      value = next;
    },
  });
}
```

**Note:** Proxy validation only covers operations that pass through that proxy.

## 99. Run Asynchronous Tasks with a Concurrency Limit

**Question:** Execute task functions with at most `limit` concurrent operations and return results in input order.

**Answer:**

```ts
async function promisePool<T>(tasks: readonly (() => Promise<T>)[], limit: number): Promise<T[]> {
  if (!Number.isInteger(limit) || limit < 1) throw new RangeError('limit must be positive');
  const results = new Array<T>(tasks.length);
  let next = 0;
  async function worker(): Promise<void> {
    while (next < tasks.length) {
      const index = next++;
      results[index] = await tasks[index]();
    }
  }
  await Promise.all(Array.from({ length: Math.min(limit, tasks.length) }, () => worker()));
  return results;
}
```

**Alternative:** Use a semaphore when jobs arrive dynamically instead of being provided as a fixed list.

```ts
// Track active jobs and queue waiting callers; release one waiter in each
// task's finally block so rejection cannot permanently consume a permit.
```

**Complexity:** O(n) scheduling with at most O(limit) active tasks. A rejection rejects the pool result.

## 100. Implement a JSON Stringifier

**Question:** Write a limited recursive serializer for null, booleans, finite numbers, strings, arrays, and plain objects.

**Answer:**

```ts
function stringifyJson(value: unknown): string {
  if (value === null) return 'null';
  if (typeof value === 'string') return JSON.stringify(value);
  if (typeof value === 'boolean') return String(value);
  if (typeof value === 'number') return Number.isFinite(value) ? String(value) : 'null';
  if (Array.isArray(value)) return `[${value.map((item) =>
    item === undefined || typeof item === 'function' || typeof item === 'symbol'
      ? 'null' : stringifyJson(item)
  ).join(',')}]`;
  if (typeof value === 'object') {
    const entries = Object.entries(value as Record<string, unknown>)
      .filter(([, item]) => item !== undefined && typeof item !== 'function' && typeof item !== 'symbol')
      .map(([key, item]) => `${JSON.stringify(key)}:${stringifyJson(item)}`);
    return `{${entries.join(',')}}`;
  }
  throw new TypeError('Top-level value is not JSON serializable');
}
```

**Alternative:** Use native `JSON.stringify` with a replacer for application-specific filtering.

```ts
const json = JSON.stringify(value, (key, item: unknown) => key.startsWith('_') ? undefined : item);
```

**Note:** This educational version omits cycle detection, `toJSON`, boxed primitives, and exact spec edge cases.

## 101. Compile Basic Markdown to HTML

**Question:** Convert simple line headings and `**bold**` markers to HTML.

**Answer:**

```ts
function escapeHtml(text: string): string {
  return text.replaceAll('&', '&amp;').replaceAll('<', '&lt;').replaceAll('>', '&gt;');
}
function markdownToHtml(markdown: string): string {
  return markdown.split('\n').map((line) => {
    const heading = /^(#{1,6})\s+(.+)$/.exec(line);
    const body = escapeHtml(heading ? heading[2] : line).replace(/\*\*(.+?)\*\*/g, '<strong>$1</strong>');
    return heading ? `<h${heading[1].length}>${body}</h${heading[1].length}>` : `<p>${body}</p>`;
  }).join('\n');
}
```

**Alternative:** Parse lines into typed intermediate nodes, then render the nodes.

```ts
type MarkdownLine = { type: 'heading'; level: number; text: string } | { type: 'paragraph'; text: string };
function parseMarkdownLine(line: string): MarkdownLine {
  const match = /^(#{1,6})\s+(.+)$/.exec(line);
  return match ? { type: 'heading', level: match[1].length, text: match[2] }
    : { type: 'paragraph', text: line };
}
```

**Note:** Escape HTML before inserting tags; this is not a full Markdown or sanitization implementation.

## 102. Breadth-First Graph Traversal

**Question:** Return nodes reachable from a start node in breadth-first order, handling cycles.

**Answer:**

```ts
function breadthFirst<T>(graph: ReadonlyMap<T, readonly T[]>, start: T): T[] {
  const queue = [start];
  const visited = new Set<T>([start]);
  const order: T[] = [];
  for (let index = 0; index < queue.length; index += 1) {
    const node = queue[index];
    order.push(node);
    for (const neighbor of graph.get(node) ?? []) {
      if (!visited.has(neighbor)) { visited.add(neighbor); queue.push(neighbor); }
    }
  }
  return order;
}
```

**Alternative:** Use a queue class with a head pointer; avoid `Array.shift()` because it moves remaining entries.

**Complexity:** O(V + E) time and O(V) space for the reachable component.

## 103. Depth-First Graph Traversal

**Question:** Return nodes reachable from a start node in depth-first order, handling cycles.

**Answer:**

```ts
function depthFirst<T>(graph: ReadonlyMap<T, readonly T[]>, start: T): T[] {
  const visited = new Set<T>();
  const order: T[] = [];
  const visit = (node: T): void => {
    if (visited.has(node)) return;
    visited.add(node);
    order.push(node);
    for (const neighbor of graph.get(node) ?? []) visit(neighbor);
  };
  visit(start);
  return order;
}
```

**Alternative:** Use an explicit stack to avoid recursion depth limits.

```ts
function depthFirstIterative<T>(graph: ReadonlyMap<T, readonly T[]>, start: T): T[] {
  const stack = [start];
  const visited = new Set<T>();
  const order: T[] = [];
  while (stack.length) {
    const node = stack.pop()!;
    if (visited.has(node)) continue;
    visited.add(node);
    order.push(node);
    const neighbors = graph.get(node) ?? [];
    for (let index = neighbors.length - 1; index >= 0; index -= 1) stack.push(neighbors[index]);
  }
  return order;
}
```

**Complexity:** O(V + E) time and O(V) space.

## 104. QuickSort

**Question:** Sort a numeric array using the QuickSort divide-and-conquer algorithm.

**Answer:**

```ts
function quickSort(values: readonly number[]): number[] {
  if (values.length < 2) return [...values];
  const [pivot, ...rest] = values;
  const lower = rest.filter((value) => value < pivot);
  const equal = rest.filter((value) => value === pivot);
  const higher = rest.filter((value) => value > pivot);
  return [...quickSort(lower), pivot, ...equal, ...quickSort(higher)];
}
```

**Alternative:** Use in-place partitioning to reduce allocations.

```ts
function quickSortInPlace(values: number[], low = 0, high = values.length - 1): number[] {
  if (low >= high) return values;
  const pivot = values[Math.floor((low + high) / 2)];
  let left = low;
  let right = high;
  while (left <= right) {
    while (values[left] < pivot) left += 1;
    while (values[right] > pivot) right -= 1;
    if (left <= right) {
      [values[left], values[right]] = [values[right], values[left]];
      left += 1; right -= 1;
    }
  }
  if (low < right) quickSortInPlace(values, low, right);
  if (left < high) quickSortInPlace(values, left, high);
  return values;
}
```

**Complexity:** Average O(n log n), worst O(n²). The functional version allocates O(n log n) space on average.

## 105. MergeSort

**Question:** Sort a numeric array using the stable MergeSort algorithm.

**Answer:**

```ts
function mergeSort(values: readonly number[]): number[] {
  if (values.length < 2) return [...values];
  const middle = Math.floor(values.length / 2);
  const left = mergeSort(values.slice(0, middle));
  const right = mergeSort(values.slice(middle));
  const result: number[] = [];
  let i = 0;
  let j = 0;
  while (i < left.length && j < right.length) result.push(left[i] <= right[j] ? left[i++] : right[j++]);
  return result.concat(left.slice(i), right.slice(j));
}
```

**Alternative:** Perform iterative bottom-up merging to avoid recursive calls.

```ts
function mergeSortIterative(values: readonly number[]): number[] {
  let result = [...values];
  for (let width = 1; width < result.length; width *= 2) {
    const merged: number[] = [];
    for (let start = 0; start < result.length; start += 2 * width) {
      const left = result.slice(start, start + width);
      const right = result.slice(start + width, start + 2 * width);
      let i = 0; let j = 0;
      while (i < left.length && j < right.length) merged.push(left[i] <= right[j] ? left[i++] : right[j++]);
      merged.push(...left.slice(i), ...right.slice(j));
    }
    result = merged;
  }
  return result;
}
```

**Complexity:** O(n log n) time and O(n) auxiliary space.

## 106. Validate a Sudoku Board

**Question:** Validate a 9×9 Sudoku board, allowing `"."` for empty cells and requiring no repeated digits in rows, columns, or 3×3 boxes.

**Answer:**

```ts
function isValidSudoku(board: readonly (readonly string[])[]): boolean {
  if (board.length !== 9 || board.some((row) => row.length !== 9)) return false;
  const rows = Array.from({ length: 9 }, () => new Set<string>());
  const columns = Array.from({ length: 9 }, () => new Set<string>());
  const boxes = Array.from({ length: 9 }, () => new Set<string>());
  for (let row = 0; row < 9; row += 1) for (let column = 0; column < 9; column += 1) {
    const value = board[row][column];
    if (value === '.') continue;
    if (!/^[1-9]$/.test(value)) return false;
    const box = Math.floor(row / 3) * 3 + Math.floor(column / 3);
    if (rows[row].has(value) || columns[column].has(value) || boxes[box].has(value)) return false;
    rows[row].add(value); columns[column].add(value); boxes[box].add(value);
  }
  return true;
}
```

**Alternative:** Validate each row, column, and box separately with one helper.

```ts
function isValidSudokuByUnits(board: readonly (readonly string[])[]): boolean {
  const valid = (cells: readonly string[]) => {
    const values = cells.filter((value) => value !== '.');
    return values.every((value) => /^[1-9]$/.test(value)) && new Set(values).size === values.length;
  };
  if (board.length !== 9 || board.some((row) => row.length !== 9)) return false;
  for (let index = 0; index < 9; index += 1) {
    if (!valid(board[index]) || !valid(board.map((row) => row[index]))) return false;
  }
  for (let top = 0; top < 9; top += 3) for (let left = 0; left < 9; left += 3) {
    const cells = board.slice(top, top + 3).flatMap((row) => row.slice(left, left + 3));
    if (!valid(cells)) return false;
  }
  return true;
}
```

**Complexity:** O(1) time and space for the fixed 9×9 board.

## 107. A* Grid Pathfinding

**Question:** Find a shortest four-directional path in a rectangular grid where `true` cells are blocked. Start and goal must be walkable; return coordinates or `null` when unreachable.

**Answer:**

```ts
type Point = [number, number];
function aStar(grid: readonly (readonly boolean[])[], start: Point, goal: Point): Point[] | null {
  if (grid[start[0]]?.[start[1]] !== false || grid[goal[0]]?.[goal[1]] !== false) return null;
  const key = ([row, column]: Point) => `${row},${column}`;
  const heuristic = ([row, column]: Point) => Math.abs(row - goal[0]) + Math.abs(column - goal[1]);
  const open: Point[] = [start];
  const cameFrom = new Map<string, Point>();
  const cost = new Map<string, number>([[key(start), 0]]);
  const closed = new Set<string>();
  while (open.length) {
    open.sort((a, b) => cost.get(key(a))! + heuristic(a) - cost.get(key(b))! - heuristic(b));
    const current = open.shift()!;
    if (key(current) === key(goal)) {
      const path = [current];
      while (cameFrom.has(key(path[0]))) path.unshift(cameFrom.get(key(path[0]))!);
      return path;
    }
    if (closed.has(key(current))) continue;
    closed.add(key(current));
    for (const [dr, dc] of [[1, 0], [-1, 0], [0, 1], [0, -1]] as const) {
      const next: Point = [current[0] + dr, current[1] + dc];
      if (grid[next[0]]?.[next[1]] !== false) continue;
      const nextKey = key(next);
      const tentative = cost.get(key(current))! + 1;
      if (tentative < (cost.get(nextKey) ?? Infinity)) {
        cameFrom.set(nextKey, current); cost.set(nextKey, tentative); open.push(next);
      }
    }
  }
  return null;
}
```

**Alternative:** Use BFS on a uniform-cost grid; it also finds a shortest path and does not require a heuristic.

```ts
// Keep a FIFO queue and a parent map. Visit each walkable coordinate once,
// then reconstruct the path by following parents back from the goal.
```

**Note:** A binary heap improves A* open-set performance; the simple sorted array favors readability.

## 108. Diff Two Virtual DOM Trees

**Question:** Compare mock virtual DOM nodes `{ type, props, children }` and report replacements, prop changes, and child insertions/removals.

**Answer:**

```ts
interface VNode { type: string; props?: Record<string, unknown>; children?: VNode[] }
type VChange = { type: string; path: string; key?: string; value?: unknown };
function diffVdom(oldNode: VNode | null, newNode: VNode | null, path = 'root', changes: VChange[] = []): VChange[] {
  if (!oldNode || !newNode || oldNode.type !== newNode.type) {
    changes.push({ type: 'replace', path, value: newNode });
    return changes;
  }
  const keys = new Set([...Object.keys(oldNode.props ?? {}), ...Object.keys(newNode.props ?? {})]);
  for (const key of keys) {
    if (!Object.is(oldNode.props?.[key], newNode.props?.[key])) {
      changes.push({ type: 'prop', path, key, value: newNode.props?.[key] });
    }
  }
  const before = oldNode.children ?? [];
  const after = newNode.children ?? [];
  for (let index = 0; index < Math.max(before.length, after.length); index += 1) {
    if (index >= before.length) changes.push({ type: 'insert', path: `${path}.${index}`, value: after[index] });
    else if (index >= after.length) changes.push({ type: 'remove', path: `${path}.${index}` });
    else diffVdom(before[index], after[index], `${path}.${index}`, changes);
  }
  return changes;
}
```

**Alternative:** Compare serialized trees and return one root replacement if any difference exists.

```ts
function diffVdomAsReplacement(oldTree: VNode, newTree: VNode): VChange[] {
  return JSON.stringify(oldTree) === JSON.stringify(newTree)
    ? [] : [{ type: 'replace', path: 'root', value: newTree }];
}
```

**Note:** This minimal diff ignores keyed reconciliation and DOM-specific patch semantics.

## 109. Lazily Evaluate a Property

**Question:** Define an object property whose calculation runs only when first read, then caches the result.

**Answer:**

```ts
function defineLazy<T extends object, V>(object: T, property: string, calculate: () => V): T {
  Object.defineProperty(object, property, {
    configurable: true, enumerable: true,
    get(this: T): V {
      const value = calculate.call(this);
      Object.defineProperty(this, property, { value, writable: true, configurable: true });
      return value;
    },
  });
  return object;
}
```

**Alternative:** Use a closure-backed getter to cache without redefining the descriptor.

```ts
function defineLazyClosure<T extends object, V>(object: T, property: string, calculate: () => V): T {
  let evaluated = false;
  let value: V;
  Object.defineProperty(object, property, {
    configurable: true,
    get() { if (!evaluated) { value = calculate.call(this); evaluated = true; } return value; },
  });
  return object;
}
```

**Note:** If calculation throws, both examples allow a later read to retry.

## 110. Safely Serialize Circular Structures

**Question:** Serialize data that may contain circular references by replacing repeated references with a marker.

**Answer:**

```ts
function stringifyCircular(value: unknown): string | undefined {
  const seen = new WeakSet<object>();
  return JSON.stringify(value, (_key, item: unknown) => {
    if (item && typeof item === 'object') {
      if (seen.has(item)) return '[Circular]';
      seen.add(item);
    }
    return item;
  });
}
```

**Alternative:** Assign reference IDs in a `WeakMap` and replace repeats with a reference object.

```ts
function stringifyWithReferenceIds(value: unknown): string | undefined {
  const seen = new WeakMap<object, number>();
  let nextId = 1;
  return JSON.stringify(value, (_key, item: unknown) => {
    if (!item || typeof item !== 'object') return item;
    if (seen.has(item)) return { $ref: seen.get(item) };
    seen.set(item, nextId++);
    return item;
  });
}
```

**Note:** The marker also labels shared-but-acyclic repeated references; a custom format needs a matching decoder.

## 111. Observe Array Mutations

**Question:** Wrap an array so calls to `push` and `pop` notify a listener with the operation and resulting array.

**Answer:**

```ts
type ArrayChange<T> = { method: 'push' | 'pop'; args: unknown[]; snapshot: T[] };
function observableArray<T>(values: T[], listener: (change: ArrayChange<T>) => void): T[] {
  return new Proxy(values, {
    get(target, property, receiver) {
      if (property === 'push' || property === 'pop') {
        if (property === 'push') {
          return (...args: T[]) => {
            const result = target.push(...args);
            listener({ method: 'push', args, snapshot: [...target] });
            return result;
          };
        }
        return () => {
          const result = target.pop();
          listener({ method: 'pop', args: [], snapshot: [...target] });
          return result;
        };
      }
      return Reflect.get(target, property, receiver);
    },
  });
}
```

**Alternative:** Expose explicit methods on a wrapper object instead of intercepting with a proxy.

```ts
function createObservedList<T>(values: T[], listener: (method: string, snapshot: T[]) => void) {
  const items = [...values];
  return {
    items,
    push(value: T) { const result = items.push(value); listener('push', [...items]); return result; },
    pop() { const result = items.pop(); listener('pop', [...items]); return result; },
  };
}
```

**Note:** Direct index writes and other mutation methods are not observed by this limited proxy.

## 112. Resolve Dependencies for Injection

**Question:** Register named dependencies and invoke a function by resolving its declared dependency names.

**Answer:**

```ts
function createContainer() {
  const providers = new Map<string, unknown>();
  return {
    register(name: string, provider: unknown): void { providers.set(name, provider); },
    resolve<T>(name: string): T {
      if (!providers.has(name)) throw new Error(`Unknown dependency: ${name}`);
      return providers.get(name) as T;
    },
    invoke<T>(dependencies: readonly string[], fn: (...args: unknown[]) => T): T {
      return fn(...dependencies.map((name) => {
        if (!providers.has(name)) throw new Error(`Unknown dependency: ${name}`);
        return providers.get(name);
      }));
    },
  };
}
```

**Alternative:** Pass a dependency object directly to the target function.

```ts
function invokeWith<T, D>(dependencies: D, fn: (dependencies: D) => T): T {
  return fn(dependencies);
}
```

**Note:** This minimal container stores values; factories, lifetimes, and circular dependency detection are additional features.

## 113. Compose a Left-to-Right Pipeline

**Question:** Compose single-argument functions so each output is passed to the next from left to right.

**Answer:**

```ts
function pipe<T>(...functions: Array<(value: T) => T>): (initial: T) => T {
  return (initial) => functions.reduce((value, fn) => fn(value), initial);
}
```

**Alternative:** Use a loop.

```ts
function pipeWithLoop<T>(...functions: Array<(value: T) => T>): (initial: T) => T {
  return (initial) => {
    let value = initial;
    for (const fn of functions) value = fn(value);
    return value;
  };
}
```

**Complexity:** O(k) calls for k functions; an empty pipeline returns its input unchanged.

## 114. Build a Chained Calculator

**Question:** Build a fluent calculator supporting `.add()`, `.multiply()`, and `.print()`.

**Answer:**

```ts
class Calculator {
  constructor(private value = 0) {}
  add(value: number): this { this.value += value; return this; }
  multiply(value: number): this { this.value *= value; return this; }
  print(): number { return this.value; }
}
```

**Alternative:** Use a closure factory with chainable methods.

```ts
function createCalculator(initial = 0) {
  let value = initial;
  const calculator = {
    add(amount: number) { value += amount; return calculator; },
    multiply(amount: number) { value *= amount; return calculator; },
    print() { return value; },
  };
  return calculator;
}
```

**Example:** `new Calculator().add(5).multiply(2).print()` returns `10`.

## 115. Evaluate Dynamic Query Rules

**Question:** Filter records using rules shaped like `{ field, operator, value }`. Support `>`, `<`, `=`, and `!=`.

**Answer:**

```ts
type Rule = { field: string; operator: '>' | '<' | '=' | '!='; value: unknown };
function filterByRules<T extends Record<string, unknown>>(records: readonly T[], rules: readonly Rule[]): T[] {
  const operators: Record<Rule['operator'], (left: unknown, right: unknown) => boolean> = {
    '>': (a, b) => (a as number) > (b as number),
    '<': (a, b) => (a as number) < (b as number),
    '=': (a, b) => a === b,
    '!=': (a, b) => a !== b,
  };
  return records.filter((record) =>
    rules.every(({ field, operator, value }) => operators[operator](record[field], value))
  );
}
```

**Alternative:** Compile validated rules to reusable predicates.

```ts
function compileRules<T extends Record<string, unknown>>(rules: readonly Rule[]): (records: readonly T[]) => T[] {
  return (records) => filterByRules(records, rules);
}
```

**Note:** Numeric operators assume numeric-compatible field values; validate schemas and fields for production.

## 116. Process an Async Stream

**Question:** Consume an async iterable of chunks one at a time and transform each chunk in arrival order.

**Answer:**

```ts
async function processStream<T, R>(
  stream: AsyncIterable<T>,
  transform: (chunk: T) => R | Promise<R>,
): Promise<R[]> {
  const output: R[] = [];
  for await (const chunk of stream) output.push(await transform(chunk));
  return output;
}
```

**Alternative:** Return an async generator to process lazily.

```ts
async function* transformStream<T, R>(
  stream: AsyncIterable<T>,
  transform: (chunk: T) => R | Promise<R>,
): AsyncGenerator<R> {
  for await (const chunk of stream) yield await transform(chunk);
}
```

**Complexity:** O(n) transform calls; collecting output uses O(n) space, lazy yielding uses bounded additional space.

## 117. Schedule Tasks by Priority

**Question:** Execute tasks in descending priority order, one at a time, and return results in execution order.

**Answer:**

```ts
type PriorityTask<T> = { priority: number; run: () => Promise<T> };
async function runByPriority<T>(tasks: readonly PriorityTask<T>[]): Promise<T[]> {
  const sorted = tasks.map((task, index) => ({ task, index }))
    .sort((a, b) => b.task.priority - a.task.priority || a.index - b.index);
  const results: T[] = [];
  for (const { task } of sorted) results.push(await task.run());
  return results;
}
```

**Alternative:** Use a max-heap for tasks that arrive dynamically; remove the highest-priority task at each scheduling step.

```ts
// A max-heap supports O(log n) insertion and removal; drain its top task
// and await it for sequential priority execution.
```

**Complexity:** O(n log n) sorting plus task execution time; ties retain input order.

## 118. Bind an Object Property to a DOM Input

**Question:** Keep a plain object property and a DOM input value synchronized from input events.

**Answer:**

```ts
function bindInput<T extends object, K extends keyof T>(
  model: T, property: K, input: HTMLInputElement,
): () => void {
  input.value = String(model[property] ?? '');
  const onInput = () => { model[property] = input.value as T[K]; };
  input.addEventListener('input', onInput);
  return () => input.removeEventListener('input', onInput);
}
```

**Alternative:** Define an accessor that updates the DOM when the model value is changed by code.

```ts
function bindInputTwoWay<T extends object, K extends keyof T>(
  model: T, property: K, input: HTMLInputElement,
): () => void {
  let value = model[property];
  Object.defineProperty(model, property, {
    configurable: true,
    get: () => value,
    set: (next: T[K]) => { value = next; input.value = String(next ?? ''); },
  });
  const onInput = () => { model[property] = input.value as T[K]; };
  input.addEventListener('input', onInput);
  return () => input.removeEventListener('input', onInput);
}
```

**Note:** Requires a browser DOM; callers should invoke the returned cleanup function.

## 119. Collect AST Nodes by Type

**Question:** Traverse a nested AST object and return every node whose `type` matches a target.

**Answer:**

```ts
type AstNode = { type?: string; [key: string]: unknown };
function collectAstNodes(root: unknown, targetType: string): AstNode[] {
  const matches: AstNode[] = [];
  const visit = (value: unknown): void => {
    if (Array.isArray(value)) { value.forEach(visit); return; }
    if (value === null || typeof value !== 'object') return;
    const node = value as AstNode;
    if (node.type === targetType) matches.push(node);
    Object.values(node).forEach(visit);
  };
  visit(root);
  return matches;
}
```

**Alternative:** Use an explicit stack to avoid recursive call-stack limits.

```ts
function collectAstNodesIterative(root: unknown, targetType: string): AstNode[] {
  const matches: AstNode[] = [];
  const stack: unknown[] = [root];
  while (stack.length) {
    const value = stack.pop();
    if (Array.isArray(value)) stack.push(...value);
    else if (value !== null && typeof value === 'object') {
      const node = value as AstNode;
      if (node.type === targetType) matches.push(node);
      stack.push(...Object.values(node));
    }
  }
  return matches;
}
```

**Note:** Assumes an acyclic AST; use a `WeakSet` if objects may be shared or cyclic.

## 120. Tokenize a Math Expression

**Question:** Tokenize non-negative integer/decimal numbers and the operators `+ - * /` in a simple arithmetic expression.

**Answer:**

```ts
function tokenizeMath(expression: string): string[] {
  const tokens = expression.match(/\d+(?:\.\d+)?|[+\-*/()]|\s+/g) ?? [];
  const compact = tokens.filter((token) => !/^\s+$/.test(token));
  if (compact.join('') !== expression.replace(/\s+/g, '')) throw new SyntaxError('Invalid token');
  return compact;
}
```

**Alternative:** Use a sticky expression to match each token from the current offset.

```ts
function tokenizeMathSticky(expression: string): string[] {
  const tokens: string[] = [];
  const pattern = /\s*(\d+(?:\.\d+)?|[+\-*/()])/y;
  let offset = 0;
  while (offset < expression.length) {
    pattern.lastIndex = offset;
    const match = pattern.exec(expression);
    if (!match) throw new SyntaxError(`Invalid token at ${offset}`);
    tokens.push(match[1]);
    offset = pattern.lastIndex;
  }
  return tokens;
}
```

**Note:** Tokenizing does not parse precedence, unary operators, or validate balanced parentheses.

## 121. Topological Sort

**Question:** Order tasks so every dependency appears before the task that depends on it. Each map entry lists the tasks that depend on its key. Return `null` if the directed graph contains a cycle.

**Answer:**

```ts
function topologicalSort<T>(graph: ReadonlyMap<T, readonly T[]>): T[] | null {
  const indegree = new Map<T, number>();
  for (const [node, neighbors] of graph) {
    if (!indegree.has(node)) indegree.set(node, 0);
    for (const neighbor of neighbors) indegree.set(neighbor, (indegree.get(neighbor) ?? 0) + 1);
  }
  const queue = [...indegree].filter(([, degree]) => degree === 0).map(([node]) => node);
  const order: T[] = [];
  for (let index = 0; index < queue.length; index += 1) {
    const node = queue[index];
    order.push(node);
    for (const next of graph.get(node) ?? []) {
      const degree = indegree.get(next)! - 1;
      indegree.set(next, degree);
      if (degree === 0) queue.push(next);
    }
  }
  return order.length === indegree.size ? order : null;
}
```

**Alternative:** Use DFS with temporary/permanent marks; finding an active node again means a cycle.

```ts
function topologicalSortDfs<T>(graph: ReadonlyMap<T, readonly T[]>): T[] | null {
  const visiting = new Set<T>();
  const visited = new Set<T>();
  const order: T[] = [];
  const visit = (node: T): boolean => {
    if (visiting.has(node)) return false;
    if (visited.has(node)) return true;
    visiting.add(node);
    for (const next of graph.get(node) ?? []) if (!visit(next)) return false;
    visiting.delete(node);
    visited.add(node);
    order.push(node);
    return true;
  };
  for (const node of graph.keys()) if (!visit(node)) return null;
  return order.reverse();
}
```

**Complexity:** O(V + E) time and O(V) space.

[⬆ Return to Top](#top) | [⬅ Return to Root README](../README.md)
