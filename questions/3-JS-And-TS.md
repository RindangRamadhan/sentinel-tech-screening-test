# JavaScript/TypeScript Questions & Answers

## Level 1: Expected Task Time <15 minutes.
## Question:
Make a javascript or typescript function that converts any string to Title Case.

Expected Results :
```js
titleCase("I'm a little tea pot") should return a string.
titleCase("I'm a little tea pot") should return "I'm A Little Tea Pot".
titleCase("sHoRt AnD sToUt") should return "Short And Stout".
titleCase("SHORT AND STOUT") should return "Short And Stout".
```
Or

Create a function that counts the word frequency in this string `Four One two two three Three three four  four   four`.  Case insensitive, ignore punctuation.

## Answer:

## Title Case Function
### JavaScript Version
```javascript
const titleCase = (str) =>
  str
    .toLowerCase()
    .split(" ")
    .map((word) => word.charAt(0).toUpperCase() + word.slice(1))
    .join(" ");

// Example Use :
console.log(titleCase("I'm a little tea pot")); // "I'm A Little Tea Pot"
console.log(titleCase("sHoRt AnD sToUt")); // "Short And Stout"
console.log(titleCase("SHORT AND STOUT")); // "Short And Stout"
```

### TypeScript Version
```typescript
const titleCase = (str: string): string => 
  str
    .toLowerCase()
    .split(" ")
    .map(word => word.charAt(0).toUpperCase() + word.slice(1))
    .join(" ");

// Example Use :
console.log(titleCase("I'm a little tea pot")); // "I'm A Little Tea Pot"
console.log(titleCase("sHoRt AnD sToUt")); // "Short And Stout"
console.log(titleCase("SHORT AND STOUT")); // "Short And Stout"

```


## Word Frequency Function
### JavaScript Version
```javascript
const wordFrequency = (str) => {
  const freqMap = str
    .toLowerCase()
    .match(/\b\w+\b/g) // Take only words (ignoring spaces/punctuation)
    .reduce((acc, word) => {
      acc[word] = (acc[word] || 0) + 1;
      return acc;
    }, {});

  return Object.entries(freqMap)
    .sort(([, countA], [, countB]) => countA - countB) // Sort by count string
    .map(([word, count]) => `${word} => ${count}`)
    .join("\n");
};

// Example Use :
console.log(
  wordFrequency("Four One two two three Three three four  four   four")
);
// one => 1
// two => 2
// three => 3
// four => 4
```

### TypeScript Version
```typescript

const wordFrequency = (str: string): string => {
  const freqMap: Record<string, number> = str
    .toLowerCase()
    .match(/\b\w+\b/g) // Take only words (ignoring spaces/punctuation)
    ?.reduce<Record<string, number>>((acc, word) => {
      acc[word] = (acc[word] || 0) + 1;
      return acc;
    }, {}) || {};

  return Object.entries(freqMap)
    .sort(([, countA], [, countB]) => countA - countB) // Sort by count string
    .map(([word, count]) => `${word} => ${count}`)
    .join("\n");
};

// Example Use :
console.log(
  wordFrequency("Four One two two three Three three four  four   four")
);
// one => 1
// two => 2
// three => 3
// four => 4
```
---
## Level 2:  Expected Task Time 1 minute.
## Question:
Fix this code, using promises:

```javascript
function delay(ms) {
  // add promise code here
}

delay(3000).then(() => alert('runs after 3 seconds'));
```

## Answer:
```javascript
function delay(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

delay(3000).then(() => alert('runs after 3 seconds'));
```

## Level 2.5:  Rewrite using Async/Await.
## Question:
Rewrite using Async/Await

```javascript
function fetchData(url, callback) {
  setTimeout(() => {
    if (!url) {
      callback("URL is required", null);
    } else {
      callback(null, `Data from ${url}`);
    }
  }, 1000);
}

function processData(data, callback) {
  setTimeout(() => {
    if (!data) {
      callback("Data is required", null);
    } else {
      callback(null, data.toUpperCase());
    }
  }, 1000);
}

// Using callbacks
fetchData("https://example.com", (err, data) => {
  if (err) {
    console.error("Fetch Error:", err);
  } else {
    processData(data, (err, processedData) => {
      if (err) {
        console.error("Process Error:", err);
      } else {
        console.log("Processed Data:", processedData);
      }
    });
  }
});

```

## Answer:
```javascript
// Convert callback-based functions to return Promises
function fetchData(url) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (!url) {
        reject("URL is required");
      } else {
        resolve(`Data from ${url}`);
      }
    }, 1000);
  });
}

function processData(data) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (!data) {
        reject("Data is required");
      } else {
        resolve(data.toUpperCase());
      }
    }, 1000);
  });
}

// Using async/await
async function main() {
  try {
    const url = "https://example.com";
    const data = await fetchData(url);
    const processedData = await processData(data);
    console.log("Processed Data:", processedData);
  } catch (err) {
    console.error("Error:", err);
  }
}

// Call the async function
main();
```
## Level 3-4: Expected Task Time Less Than 1 Hour.
## Question:
Create a real-time chat between two windows; using web sockets, vuejs and typescript.

## Answer:
The project implementation can be found in the following repositories:
- [Back-End Repository](https://github.com/RindangRamadhan/tech-test-chat-app-be)
- [Front-End Repository](https://github.com/RindangRamadhan/tech-test-chat-app-fe)

These repositories contain the complete setup for a real-time chat application using WebSockets, Vue.js, and TypeScript.