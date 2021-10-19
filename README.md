# JavaScript TDD playing cards

The purpose of this repo is to help you become familiar with test-first design, also commonly called test-driven development, or TDD. There are lots of approaches to testing, but I recommend and prefer test-first design for several reasons. First off there is a difference in the clean design of the code. You may find that increasing complexity is _much_ easier to manage and this might increase your confidence as a developer generally. Additionally, tests communicate intent to other developers and collaborators. It also can be used to show that you have meet the client's requirements. Considered together, if by following this approach you end up with a solid design, manageable complexity and automated testing, _not_ applying these practices is just asking for pain (short term and long term).

## Setup

Clone down the repository and run `npm i` to install dependencies. This will install the `jest` testing library.


## Test 1: Test setup

I expect true to be true! This tautology is just to make sure our setup is working and is a standard first test case to write. Create `tests/index.test.js` with these contents.

```js
test('test setup working', () => {
  expect(true).toBeTruthy()
})
```

Run tests on the command line with `npm test` and post a selfie with a smile if you're getting a passing test. If so, commit it.

```shell
git add -A
git commit -m "Test setup working"
```


## Test 2: getCards

This is to make sure we can begin testing actual code and our most simple card trick is .... pick a card.

At the top of `tests/index.test.js`, add a reference to the code we intend to test.

```js
const deck = require('../deck') // this is the line to add
```

Now you'll notice you are getting an error because it can't find the `deck` reference (because it doesn't exist yet). So let's add a `./deck.js` file with the least amount of code.

```js
module.exports = {}
```

Cool, check the console and see that our single test is passing again, let's head back to `tests/index.test.js` add a test for returning the a single card from the deck.

```js
test('returns a card', () => {
  const amount = 1
  const expected = "Ace of Spades"
  const actual = deck.getCards(amount)
  expect(actual).toBe(expected)
})
```

Now our test is failing because it can't find the `getCards()` method. Should we quit coding? Nah it's easy, let's add a `getCards()` method into our `deck.js` file.

```js
module.exports = {
  getCards: getCards
}

function getCards (amount) {
}
```

Now our test is failing because it returned the wrong value (`undefined`) instead of what it was expecting (`Ace of Spades`). So let's return what it wants.

```js
function getCards (amount) {
  return "Ace of Spades"
}
```

The sweet sound of winning! Our tests are passing again. Let's commit it. Selfie number two?

```shell
git add -A
git commit -m "Getting a Card from the deck"
```


## Test 3: Properly getting cards from the deck

Now let's add a test that can check that it is possible to pick every card out of a selection of playing cards.

```js
test('gets all the cards', () => {
  const amount = 52
  const expected = 52
  const hand = deck.getCards(amount)
  const actual = hand.length
  expect(actual).toBe(expected)
})
```

This new test is failing because we were expecting a `52` and actually got `13`. I.e. the length of `Ace of Spades` was returned. Apparently our `getCards` method needs to do something more appropriate than just `return "Ace of Spades"`.

```js
function getCards (amount) {
  // what to put here?
}
```

Complete the `getCards` function to pass the test. Did you notice that the test seemed to suggest that we should return an array? High 5! But remember, the cycle is RED -> GREEN -> REFACTOR. Is there anything about your code that you could improve to make it more readable or DRY?

Don't forget to commit your changes:

```shell
git add -A
git commit -m "getting cards"
```


## Test 4: Take 5 cards

**From this point forward you will be writing the tests yourself!**

Now let's add a test for getting 5 random cards. To do this, we're going to need to pass `5` as an argument to `getCards()`.

```js
test('gets 5 cards', () => {
  // what to put here?
  // perhaps some consts?
})
```

Can you refactor your code? What could be improved? Remember to run the tests again after you've tidied up, just to make sure you didn't break anything. Now do a commit!


## Test 5: No two hands have the same cards

Now let's add a feature for ensuring the deck is legit. How might we test this? Perhaps we should cut the deck in half and check that the two halves are different.

```js
test('no two cards are the same', () => { // your turn
})
```

How's the code looking? Anything need refactoring? Make your changes, then commit them.


## Test 6: Shuffle method

Now that we have a proper deck. Let's add some abilities to shuffle the deck. First, a new test.

```js
test('shuffles the deck', () => {
  //

})
```

Once again, look for opportunities to refactor. Do you have a `shuffleDeck()` function that is easily testable? 


## Test 7 and 8: Check the suit

Maybe `isSameSuit()` and `isSameValue()` would be useful functions to have. Write a test for each of these. 

```js
test('checks two cards are of the same suit', () => {
  // test goes here :)
})
```

## Test 9: Score a hand 

Now that we can compare some aspects of types of cards let's add a feature to score a hand. Of course, this will depend on the rules that are at play in your game. Don't overthink it, just pick a game you know the rules for and _hardcode_ the values inside the test for now. Write a test for `scoreHand()`.

```js
test('scores a hand', () => {
})
```

Write your test, pass your test, check to see if you can refactor anything, and do a commit.




## STRETCH: Create a client to consume the deck module

Name it `index.js` so you can run it with `npm start`.
