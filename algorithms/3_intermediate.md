# 👦 Intermediate Algorithms

### Mergesort

```tsx
function mergeSort(arr: number[]): number[] {
	if (arr.length <= 1) return arr;

	const middle = Math.floor(arr.length / 2);
	const left = arr.slice(0, middle);
	const right = arr.slice(middle);

	return merge(mergeSort(left), mergeSort(right));
}

function merge(left: number[], right: number[]): number[] {
	let result = [];
	let leftIndex = 0;
	let rightIndex = 0;

	while (leftIndex < left.length && rightIndex < right.length) {
		if (left[leftIndex] < right[rightIndex]) {
			result.push(left[leftIndex]);
			leftIndex++;
		} else {
			result.push(right[rightIndex]);
			rightIndex++;
		}
	}

	return result.concat(left.slice(leftIndex)).concat(right.slice(rightIndex));
}
```

### Mex number

```tsx
function mex(arr) {
	arr.sort();
	let mex = 0;
	for (let i = 0; i < arr.length; i++) {
		if (arr[i] == mex) {
			// Increment mex
			mex += 1;
		}
	}
	return mex;
}
```

### Reverse linked list

```tsx
class ListNode {
	value: number;
	next: null | ListNode = null;

	constructor(value: number) {
		this.value = value;
	}
}

function reverseLinkedList(head: ListNode): ListNode {
	let prev = null;
	let current = head;
	let next = null;
	while (current !== null) {
		next = current.next;
		current.next = prev;
		prev = current;
		current = next;
	}
	head = prev;
	return head;
}
```
