# PPT - DSA Assignment 24

## Answer 1:
```js
const romanToInt = (str) => {
    let result = 0;

    for (let i = 0; i < str.length; i++) {
        if (i > 0 && c2n(str[i]) > c2n(str[i - 1])) {
            result -= 2 * c2n(str[i - 1]); // because previously added [!!!]
        }

        result += c2n(str[i]);
    }

    return result;
};

//Define characters -> c2n = characters to number
const c2n = (c) => {
    switch (c) {
        case "I":
            return 1;
        case "V":
            return 5;
        case "X":
            return 10;
        case "L":
            return 50;
        case "C":
            return 100;
        case "D":
            return 500;
        case "M":
            return 1000;
        default:
            return 0;
    }
};
```

<br/>

## Answer 2:
```js
const lengthOfLongestSubstring = (str) => {
    let count = 0;
    let spacer = 0;

    let letterMap = new Map();

    for (let i = 0; i < str.length; i++) {
        let letter = str[i];

        if (letterMap.has(letter)) {
            spacer = Math.max(letterMap.get(letter), spacer);
        }

        letterMap.set(letter, i + 1);

        count = Math.max(count, i - spacer + 1);
    }
    return count;
};
```

<br/>

## Answer 3:
```js
const majorityElement = (nums) => {
    let map = {};
    let max = 0;
    let majorNum = 0;
    let len = nums.length;
    for (let i = 0; i < len; i++) {
        if (!map[nums[i]]) map[nums[i]] = 0;
        map[nums[i]]++;
        if (map[nums[i]] > max) {
            majorNum = nums[i];
            max = map[nums[i]];
        }
    }
    return majorNum;
};
```

<br/>

## Answer 4;
```js
const groupAnagrams = (strs) => {
    // define output array
    const output = []
    // define map
    const map = {}
    // loop through strs
    for (let i = 0; i < strs.length; i++) {
        // sort current str
        const strSorted = strs[i].split('').sort().join('')
        // if sorted string is present in map
        if (map[strSorted] !== undefined) {
            // get index of output array to push current str
            output[map[strSorted]].push(strs[i])
        } else {
            // push current str into output array
            output.push([strs[i]])
            // add sorted str to map
            // set map[sorted str] = output array length - 1 
            map[strSorted] = output.length - 1
        }

    }

    // return output array
    return output
};
```

<br/>

## Answer 5:
```js
const nthUglyNumber = (n) => {
    let uglys = [1];
    let p2 = 0;
    let p3 = 0;
    let p5 = 0;

    while (uglys.length < n) {
        let ugly2 = uglys[p2] * 2;
        let ugly3 = uglys[p3] * 3;
        let ugly5 = uglys[p5] * 5;

        let minV = Math.min(ugly2, ugly3, ugly5);

        if (minV === ugly2) {
            p2++;
        }
        if (minV === ugly3) {
            p3++;
        }
        if (minV === ugly5) {
            p5++;
        }
        if (minV !== uglys[uglys.length - 1]) {
            uglys.push(minV);
        }
    }

    return uglys[n - 1];
};
```

<br/>

## Answer 6:
```js
const topKFrequent = (words, k) => {
    let hash = {};
    for (let word of words) {
        hash[word] = hash[word] + 1 || 1;
    }

    let result = Object.keys(hash).sort((a, b) => {
        let countCompare = hash[b] - hash[a];
        if (countCompare == 0)
            return a.localeCompare(b);
        else
            return countCompare;
    }
    );
    return result.slice(0, k);
};
```

<br/>

## Answer 7:
```js
var maxSlidingWindow = function (nums, k) {
    // Decreasing monotonic queue so the maximum value is at the front
    const dequeue = [];
    const output = [];

    for (let i = 0; i < nums.length; i++) {
        // add the number at the right position queue
        while (nums[i] > dequeue[dequeue.length - 1]) {
            dequeue.pop();
        }
        dequeue.push(nums[i]);

        // once the window fully overlaps the array, we can start register the maximum values in each iteration.
        if (i >= k - 1) {
            output.push(dequeue[0]);
            // remove maximum value when it's moving outside of the window
            if (nums[i - k + 1] === dequeue[0]) {
                dequeue.shift();
            }
        }
    }

    return output;
};
```

<br/>

## Answer 8:
```js
const findClosestElements = function (arr, k, x) {
    return arr.sort((a, b) => {
        const distanceA = Math.abs(a - x)
        const distanceB = Math.abs(b - x)
        if (distanceA === distanceB) {
            return a - b
        }
        return distanceA - distanceB
    }).slice(0, k)
        .sort((a, b) => a - b)
}
```