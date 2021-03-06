# Hangman Solver
 An analyzer for determining statistically optimal hangman play

This Hangman Solver keeps track of words by using tuples, made up of the word and a set of unguessed letters. As guesses are made, the set of letters decreases in size. A word would be considered guessed when the set of unguessed letters is empty. 

The solver is best at finding words that are difficult to guess. Based on the assumption that a statistically perfect hangman _guesser_ would guess the most common letter in the set of remaining words, various words can be found that would take the most guesses before a single correct letter is guessed. 

For example, the most common letter found in five letter hangman words is **e**. Thus, a great guesser would start by guessing the letter **e**. Then, of the words remaining, the most common letter is **a**. After that is guessed, if wrong, the most common letter would be **o**. Following this pattern, guesses for the letters **i** and **u** would be made, in order. If none of the vowels exist, a savvy guesser would recognize that the word _lynch_ is the only possible word of length five. 

For a six letter word, a strong word choice would be _rhythm_. It once again would yield failed guesses when a player guesses **eaiou**, the statistical best choices. Other good word choices include _church_, _luxury_, _trucks_, and _skulls_. 

For a seven letter word, a guesser should actually guess the letter **i** after a failed **e**, followed by an **a** and then an **o**. If all four of these fail, the only valid word will be _suburbs_. Other difficult words to find, if the letter **o** can be found but not **eia**, include _thought_, _unknown_, and _conduct_. 

Another complication worth considering is that guessing the most popular letter isn't always the way to go. Instead, guessing a letter than appears in about half of the words may be a better approach. For instance, if you know that 99% of possible words have the letter **e**, guessing the letter **e** might help you if the word you are looking for doesn't have it, but otherwise you aren't getting much new information. Instead, guessing a letter that appears in about 50% of possible words can help you more easily narrow down your options.

Mathematically, we can assume that for any guessed letter _l_, it will appear in k% of the words. If we determine the average percent of the current words that must be considered after _l_ is guessed (assuming every word is equally likely), we will have an average of <sup>(k<sup>2</sup> + (1-k)<sup>2</sup>)</sup>/<sub>2</sub>% of the words remaining. The minimum value of this function is 50%, when _l_ appears in exactly half of the words. As such, when we aim to select values that are in as close to half of the potential words as possible, we can greatly improve our performance.

# Potential Further Developments
The above strategy for selecting a word is a sound one, and will surely annoy plenty of opponents. However, it might not be the best. For instance, the word _rugby_ would be likely be more difficult to guess than the word _lynch_, as there is more than one word that has a **u** but no other vowel. There are 27 of them, actually, including the words _bluff_, _chuck_, _drums_, and _sunny_. 

This realization makes it clear that there is nuance in playing optimal hangman, as at some point a statistically optimal player may need to be correct in order for them to take longer to guess the correct word. 

Further Developments to this repository should take this into account, and generate a binary tree wherein nodes represent a guessed letter, the left branch of the tree represents that guess being correct, and the right branch of the tree representing the opposite. In this data structure, a tree leaf would suggest that a word has been found, and the statistical best word for a player to choose would have maximum height. 

It is worth noting that this is an oversimplificiation, as placement of the letters is a helpful clue for a hangman guesser, as well.

