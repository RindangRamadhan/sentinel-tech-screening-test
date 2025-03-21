# Golang Questions & Answers

## Question:
https://goplay.tools/

Create a function that counts the word frequency in this string "Four, One two two three Three three four  four   four".  Case insensitive, ignore punctuation.

Expected Answer (order doesn’t matter):
- one   => 1
- two   => 2
- three => 3
- four  => 4


## Answer:
You can check the answer directly here: https://goplay.tools/snippet/LwZXKzCiBjh

Here is the function used to count word frequency in a string:
```go
package main

import (
	"fmt"
	"regexp"
	"sort"
	"strings"
)

func main() {
	text := "Four, One two two three Three three four  four   four"
	freq := wordFrequency(text)

	printWordFrequency(freq)
	// Output :
	// Word frequencies (alphabetical order):
	// four => 4
	// one => 1
	// three => 3
	// two => 2

	printWordFrequencyByCount(freq)
	// Output :
	// Word frequencies (by count, descending):
	// four => 4
	// three => 3
	// two => 2
	// one => 1
}

func wordFrequency(input string) map[string]int {
	// Convert to lowercase for case-insensitivity
	input = strings.ToLower(input)

	// Regex to match only words (alphanumeric sequences)
	re := regexp.MustCompile(`\w+`)
	words := re.FindAllString(input, -1)

	// Map to store word frequencies
	freq := make(map[string]int)

	// Count occurrences of each word (case-insensitive)
	for _, word := range words {
		freq[word]++
	}

	return freq
}

// Print word frequencies in alphabetical order
func printWordFrequency(freq map[string]int) {
	fmt.Println("Word frequencies (alphabetical order):")

	// Get all words and sort them
	words := make([]string, 0, len(freq))
	for word := range freq {
		words = append(words, word)
	}
	sort.Strings(words)

	// Print sorted results
	for _, word := range words {
		fmt.Printf("%s => %d\n", word, freq[word])
	}
}

// Print word frequencies sorted by count (descending)
func printWordFrequencyByCount(freq map[string]int) {
	fmt.Println("\nWord frequencies (by count, descending):")

	// Create a slice of word-count pairs
	type wordCount struct {
		word  string
		count int
	}
	pairs := make([]wordCount, 0, len(freq))

	for word, count := range freq {
		pairs = append(pairs, wordCount{word, count})
	}

	// Sort by count (descending), then by word (ascending) for same counts
	sort.Slice(pairs, func(i, j int) bool {
		if pairs[i].count == pairs[j].count {
			return pairs[i].word < pairs[j].word
		}
		return pairs[i].count > pairs[j].count
	})

	// Print sorted results
	for _, pair := range pairs {
		fmt.Printf("%s => %d\n", pair.word, pair.count)
	}
}
```