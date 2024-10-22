# fishy_javascript_sort


[Python version of this repository](https://github.com/sergemoskalenko/fishy_python_sort)

This is a deliberately very inefficient, fishy, one-liner code that does seemingly useful things in a strange, roundabout way...

So, what do we have here? We’ve created a random number generator that loves to do bit shifts and called it R9. Then we use this generator to pick two random indices of an array and swap them if they are out of order. All this happens in the srt_f function, which is called in a loop inside the shit_sort function until the array is sorted.
And yes, the name shit_sort hints that this is not the most efficient way to sort, but it’s fun! 😄

```javascript
// This is a deliberately very inefficient, fishy, one-liner code that does seemingly useful things in a strange, roundabout way...

// Create a <pre> container for output
document.body.innerHTML = '<pre id="output"></pre>';
const output = document.getElementById('output');

// Function to print to the <pre> container
const print = (...args) => {
    output.innerHTML += args.join(' ') + '\n';
};

// R9 function is our random number generator that loves to do bit shifts.
const R9 = (s, c) => Math.abs((s = parseInt(s)) ^ (s << 13) ^ (s >> 17) ^ (s << 5)) % c;

// ij function is our magical way to pick two random indices of an array.
const ij = (a, s) => {
    const i = R9(s, a.length);
    const j = R9(s + 731, a.length);
    return i > j ? [j, i] : [i, j];
};

// pr function is our way to nicely print arrays before and after sorting.
const pr = (arr, src_arr) => {
    print("\nSRC (in):", src_arr);
    print("\nWRK (out):", arr);
};

// srt_f function is our sorting algorithm that swaps elements if they are out of order.
const srt_f = (arr) => {
    seed += Math.floor(Date.now() / 1000);  // Update seed to have something new each time.
    const [i, j] = ij(arr, seed);  // Get two random indices.
    if (arr[i] > arr[j]) {
        print(i, "<-->", j);  // Print indices if elements are out of order.
        [arr[i], arr[j]] = [arr[j], arr[i]];  // Swap elements if needed.
    }
};

// shit_sort function is our main sorting algorithm that uses srt_f to sort the array.
const shit_sort = (arr, src_arr) => {
    while (!arr.every((val, i, array) => !i || array[i - 1] <= val)) {
        srt_f(arr);
    }
};

// Start by generating a random seed based on the current time.
let seed = Math.floor(Date.now() / 1000);

// Generate an array WRK of 100 random numbers.
const WRK = Array.from({ length: 100 }, (_, i) => R9(seed + i, 1000));

// Copy WRK to SRC to keep the original array.
const SRC = [...WRK];

// Print a message about starting the sorting.
print("\nSorting WRK...");

// Start sorting the WRK array.
shit_sort(WRK, SRC);

// Print arrays before and after sorting.
pr(WRK, SRC);
```
