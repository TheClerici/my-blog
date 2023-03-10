---
layout: post
title:  "All combinations algorithm"
date:   2023-03-10 12:18:25 -0000
category: Log
---
## Create a function that creates an array from 1 to n and uses combination to get all possible permutations in TheAlgorithms/Java and test it.

------------------------------------------------------------------------------------------
<blockquote> <p> Overview: </p> </blockquote> 

[The Algorithms][algo] open source project is a group of programmers helping each other build new things, whether it be writing complex encryption programs, or simple ciphers. Our goal is to work together to document and model beautiful, helpful and interesting algorithms using code. They are an open-source community - anyone can contribute. They check each other's work, communicate and collaborate to solve problems. They strive to be welcoming, respectful, yet make sure that our code follows the latest programming guidelines.

------------------------------------------------------------------------------------------
<blockquote> <p> Context: </p> </blockquote> 

[[FEATURE REQUEST] Backtracking algorithms (All combinations)][cj-dor] issue:

In this problem, we want to determine all possible combinations of k numbers out of 1 ... n. We use backtracking to solve this problem.

* Example:
>> generate_all_combinations(n=4, k=2)
>> [[1, 2], [1, 3], [1, 4], [2, 3], [2, 4], [3, 4]]

------------------------------------------------------------------------------------------
<blockquote> <p> Solution: </p> </blockquote> 

The first challenge was to understand how the project I was going to contribute worked, after that, I needed to see the contributing guide so I can follow it, making sure to follow
GitHub's code of conduct for open-source projects, which stipulates that everyone must be gracious, respectful and professional.

While proposing this algorithm, siriak talked to me about a way of implementing it that can be better than how I proposed it, here is the conversation:

<p align="center">
    <img src="https://github.com/TheClerici/my-blog/blob/main/images/siriakone.png?raw=true">
</p>
<div align="center">
    <h5><strong>Fig 1. GitHub 1st feedback</strong></h5>
</div>

Knowing what was expected to implement I was ready to start working on it, as I needed to use an already implemented Algorithm, I had to check it to see how it worked. I managed to get with the following solution: 

* Started by creating the new class in the backtracking directory.
* Instead of `Combination`, I called it `ArrayCombination`, because it was now gonna use `Combination` in order to make the backtracking part of the code.

```java
/**
 * Finds all permutations of 1...n of length k
 */
public class ArrayCombination {
    private static int length;

    /**
     * Find all combinations of 1..n by creating an array and using backtracking in Combination.java
     * @param n max value of the array.
     * @param k length of combination
     * @return a list of all combinations of length k. If k == 0, return null.
     */
    public static List<TreeSet<Integer>> combination(int n, int k) {
        if (n <= 0) {
            return null;
        }
        length = k;
        Integer[] arr = new Integer[n];
        for (int i = 1; i <= n; i++) {
            arr[i-1] = i;
        }
        return Combination.combination(arr, length);
    }
}
```

* Then, I tested it to see if it was working correctly. (Only showing 3 examples)

```java
public class ArrayCombinationTest {

    @Test
    void testNBeingZeroOrLess() {
        List<TreeSet<Integer>> zeroResult = ArrayCombination.combination(0, 1);
        List<TreeSet<Integer>> negativeResult = ArrayCombination.combination(-1, 1);
        assertNull(zeroResult);
        assertNull(negativeResult);
    }

    @Test
    void testLengthOne() {
        List<TreeSet<Integer>> result = ArrayCombination.combination(2, 1);
        assert result != null;
        assertEquals(1, result.get(0).iterator().next());
        assertEquals(2, result.get(1).iterator().next());
    }

    @Test
    void testLengthFive() {
        List<TreeSet<Integer>> result = ArrayCombination.combination(10, 5);
        assert result != null;
        Integer[] arr = result.get(0).toArray(new Integer[5]);
        assertEquals(1, arr[0]);
        assertEquals(5, arr[4]);
    }
}
```

After making sure everything was working fine, I decided to open a Pull Request and I'm currently waiting on approval so it merges!

------------------------------------------------------------------------------------------
<blockquote> <p> How to contribute: </p> </blockquote> 

1. Look for a new Issue
    * The first step to contributing to TheAlgorithms/Java is to choose a contribution. This can be a new feature, a bug fix, documentation, or testing.
2. Fork the project
    * Start by forking the project on GitHub. This will create a copy of the project in your own GitHub account.
3. Clone the forked project
    * Clone the forked project to your local machine using Git. This will create a copy of the project on your local machine.
5. Make Changes and Test
    * Make the necessary changes to the codebase and test them locally. This will help you catch any bugs or errors and ensure that your changes work as intended.
6. Commit Changes
    * After testing the changes, commit them to the branch with an appropriate commit message. The commit message should be descriptive and should explain the changes made.
7. Push Changes and Create a Pull Request
    * Push the changes to the forked repository and create a pull request. The pull request should include a description of the changes made, any relevant documentation, and any other details that are necessary.
8. Address Feedback
    * TThe project maintainers may provide feedback on your changes. Address any feedback and make the necessary changes to your code.
9. Merge the Pull Request
    * Once your changes have been approved, they will be merged into the original project.

With the solution added, I just followed the guide instructions explained above to fully contribute to the project, it is now waiting on approval and with that, I will succesfully contribute to my fourth open-source project!! See you next time!

[algo]: https://github.com/TheAlgorithms
[cj-dor]: https://github.com/TheAlgorithms/Java/issues/3912