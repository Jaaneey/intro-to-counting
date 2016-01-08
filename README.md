# An Introduction to Counting and Probability for Javascript Developers

### Introduction: Who Cares?

### Prerequisites

### Objectives

### Warmup

Consider the following function. What does it do, and what is its big-O complexity?

```js
function multiplicationStatements(n) {
  for (var i = 0; i < n; i++) {
    for (var j = 0; j < n; j++) {
      console.log(`${i} * ${j} is equal to ${i * j}.`);
    }
  }
}
```

The nested for-loop may tip you off that this function is O(_n_<sup>2</sup>). But can you explain _why_ nested for loops of length _n_ typically yield a complexity of O(_n_<sup>2</sup>)? The answer lies in the grandiosely-named Fundamental Counting Principle.

### Fundamental Counting Principle

Roughly speaking, the Fundamental Counting Principle states that if there are _n_ ways to do one thing, and there are _m_ ways to do another thing, then there are _n_ * _m_ ways to do the first thing and the second thing. 

Here's an example: at Chipotle, there are six different dishes you can order: a burrito, a bowl, a salad, hard tacos (corn), soft tacos (corn), and soft tacos (flour). For each of these, you can also choose one of five different proteins: steak, carnitas, chicken, barbacoa, and sofritas. This means that altogether there are 6 * 5 = 30 lunch options from among these choices. Here's a diagram showing the choices (each line represents one lunch option):

DIAGRAM GOES HERE

In the same way, in our function `multiplicationStatements(n)` above, there are `n` possible values for `i` and `n` possible values for `j`. So, by the Fundamental Counting Principle, there are `n * n` possible values for the pair `(i,j)`. 

So far, we've only talked about the Fundamental Counting Principle as it pertains to pairs of options, but it can be extend to an arbitrary number of collections. Returning to our Chipotle example, not only can you choose the type of dish and the protein, you can also choose the type of rice (either brown or white) and the type of beans (black or brown). So, between the number of dishes (6), the number of proteins (5), the number of rice types (2), and the number of bean types (2), this gives a total of 6 * 5 * 2 * 2 = 120 different lunch options.

In general, if you have _n_<sub>1</sub> options for your first choice, _n_<sub>2</sub> options for your second choice, ... , and _n_<sub>k</sub> options for your _k_<sup>th</sup> choice, the Fundamental Counting Principle tells us that you will have _n_<sub>1</sub> * _n_<sub>2</sub> * ... * _n_<sub>k</sub> options in all.

**EXERCISE** 

Use the Fundamental Counting Principle to determine the complexity of each of the following functions:

```js
function moreMultiplicationStatements(n) {
  for (var i = 0; i < n; i++) {
    for (var j = 0; j < n; j++) {
      for (var k = 0; k < n; k++) {
        console.log(`${i} * ${j} * ${k} is equal to ${i * j * k}.`);
      }
    }
  }
}
```

```js
function moreMultiplicationStatements(n) {
  for (var i = 0; i < n; i++) {
    for (var j = 0; j < n*n; j++) {
      for (var k = 0; k < Math.sqrt(n); k++) {
        console.log(`${i} * ${j} * ${k} is equal to ${i * j * k}.`);
      }
    }
  }
}
```

```js
function moreMultiplicationStatements(n,m,l) {
  for (var i = 0; i < n; i++) {
    for (var j = 0; j < m; j++) {
      for (var k = 0; k < l; k++) {
        console.log(`${i} * ${j} * ${k} is equal to ${i * j * k}.`);
      }
    }
  }
}
```

### Permutations

Once you know about the Fundamental Counting Principle, you can begin to count more complicated sets of objects. 

One common counting problem is to count the number of _permutations_, or rearrangements, of som set of numbers. For example, consider the array `[1, 2, 3]`. There are six permutations of this array:

```js
[1, 2, 3]
[1, 3, 2]
[2, 1, 3]
[2, 3, 1]
[3, 1, 2]
[3, 2, 1]
```

Where does the number 6 come from? To answer this, let's use the Fundamental Counting Principle! There are three values we can choose for the first element of the array - 1, 2, 3. Once we've chosen that first element, we have two options for the second element of the array; for instance, if we say the first element will be 2, then the second element can be either 1 or 3. Finally, once we've chosen the second element, there is only one choice left for the value of the third element: if we say the first element will be 2, and the second element will be 3, then the last element must be 1, since that's the only value remaining.

In other words, but the fundamental counting principle, the number of permutations of the above array is 3 * 2 * 1 = 6.

Of course, this can be generalized to an array of any size. In general, we have the following fact:

**Fact:** The number of permutations of a set of _n_ elements is n * (n - 1) * (n - 2) * ... * 3 * 2 * 1 = n!

**Same Fact, Javascript-Developer-Friendly version:** the number of permutations of an array with _n_ distinct elements is n!.

**EXERCISE**

1. How many premutations of the array `[1, 2, 3, 4]` are there? List them all.
2. How many permutations of the array `[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]` are there? Why would it be impractical to list them all out?

**EXERCISE (Bonus!)** Complete [this kata](http://www.codewars.com/kata/permutations) on permutations.

### Combinations

How many ways are there to draw a 5-card hand from a deck of 52 cards? Given what you know about permutations, you might be tempted to say that the answer is 52 * 51 * 50 * 49 * 48 = 311,875,200. This is because you have 52 options for your first card, then 51 options for your second (every card is available except your first card), 50 options for your third (every card is available except your first two cards), and so on. However, typically the order of the cards in your hand doesn't matter. This hand:

is the same as this hand:

because the cards are the same, they've just been rearranged.