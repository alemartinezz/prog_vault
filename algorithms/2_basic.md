# 🐣 Basic Algorithms

### Even numbers

```tsx
function isEven(n: number): boolean {
	return n % 2 === 0;
}
```

### Remove duplicates from array

```tsx
function removeDuplicates(arr) {
	return arr.filter((item, index) => arr.indexOf(item) === index);
}
```

```tsx
function removeDuplicates(arr) {
	return [...new Set(arr)];
}
```

### Largest number

```tsx
function largestNumber(numbers: number[]): number {
	let max = numbers[0];
	for (let num of numbers) {
		if (num > max) {
			max = num;
		}
	}
	return max;
}
```

### Char count occurencies

```tsx
function countOccurrences(str: string, char: string): number {
	let count = 0;
	for (let item of str) {
		if (item === char) count++;
	}
	return count;
}
```

### Char most repeated

```tsx
function mostFrequentCharCount(s: string): [string, number] {
	const charCount: { [key: string]: number } = {};

	// Paso 1: Contar las ocurrencias de cada carácter
	for (let char of s) {
		if (charCount[char]) {
			charCount[char]++;
		} else {
			charCount[char] = 1;
		}
	}

	// Paso 2: Encontrar el carácter con la máxima ocurrencia
	let maxChar = '';
	let maxCount = 0;
	for (let char in charCount) {
		if (charCount[char] > maxCount) {
			maxChar = char;
			maxCount = charCount[char];
		}
	}

	return [maxChar, maxCount];
}

const testString = 'aabbbccddeeeeee';
const [char, count] = mostFrequentCharCount(testString);
console.log(`El carácter '${char}' se repite ${count} veces.`);
```

### Balanced Brackets

```tsx
function areParenthesesBalanced(exp: string): boolean {
	// Declare an array to act as a stack
	const stack: string[] = [];

	// Traverse the expression string
	for (let i = 0; i < exp.length; i++) {
		const char = exp[i];

		// If the current character is a starting bracket, push it onto the stack
		if (char === '(' || char === '{' || char === '[') {
			stack.push(char);
		}
		// If the current character is a closing bracket, pop from the stack and check
		else if (char === ')' || char === '}' || char === ']') {
			const last = stack.pop();

			if ((char === ')' && last !== '(') || (char === '}' && last !== '{') || (char === ']' && last !== '[')) {
				return false; // Parentheses are not balanced
			}
		}
	}

	// After complete traversal, if there are some starting brackets left in the stack, they are not balanced
	return stack.length === 0;
}

// Test the function
const testStr1 = '{[()]}';
const testStr2 = '{[(])}';
const testStr3 = '{[()]}{[()]}';

console.log(areParenthesesBalanced(testStr1)); // Output should be true
console.log(areParenthesesBalanced(testStr2)); // Output should be false
console.log(areParenthesesBalanced(testStr3)); // Output should be true
```

### First non repeated

```tsx
function firstNonRepeatedCharacter(s: string): string | null {
	const charCount = new Map<string, number>();

	for (let char of s) {
		charCount.set(char, (charCount.get(char) || 0) + 1);
	}

	for (let char of s) {
		if (charCount.get(char) === 1) return char;
	}

	return null;
}
```
