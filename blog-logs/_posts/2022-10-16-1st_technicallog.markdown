---
layout: post
title:  "1st Technical Log"
date:   2022-10-23 10:18:25 -0700
category: Log
---
## Double or One Thing

# `Overview`

Double or One Thing is a problem that deals with String manipulation, where depending on the word that you get, you need to output the one that appears first in alphabetical order. In this case, I decided to give it an approach in Kotlin language, as I challenged myself to continue working with Kotlin on the individual problem to continue practicing it.

In summary, the program receives a set of Strings wich you need to manipulate in order to print the one needed.

For example, these strings are in alphabetical order: 

1. CODE
2. HELLO
3. HI
4. HIM
5. HOME
6. JAM

# `Context`

[Double or One Thing][cj-dor1] problem challenge:

You are given a string of uppercase English letters. You can highlight any number of the letters (possibly all or none of them). The highlighted letters do not need to be consecutive. Then, a new string is produced by processing the letters from left to right: non-highlighted letters are appended once to the new string, while highlighted letters are appended twice. Similarly, if you highlight nothing, you obtain HELLOWORLD, and if you highlight all of the letters, you obtain HHEELLLLOOWWOORRLLDD. Notice how each occurrence of the same letter can be highlighted independently.

Given a string, there are multiple strings that can be obtained as a result of this process, depending on the highlighting choices. Among all of those strings, output the one that appears first in alphabetical (also known as lexicographical) order.

For more info, feel free to follow the hyperlink on `Double or One Thing`.

# `Solution`

The first challenge was to understand how CodeJam was giving the inputs, as they test your answer with 100 cases, in this case, they start giving you the 100 cases so you then test them and output in the order that they gave.

For this, I worked on the `main` function of the program where I first read the total number of cases, depending on that, I created a mutable List to fill with all the cases with a for loop. On the last part, I need to print the cases in order, so I made another for loop to iterate through all the cases and called a function named doubleOrOne to work on the answer for the case in moment.

{% highlight kotlin %}
fun main(args: Array<String>) {
    //input cases
    val cases = readln().toInt();
    //inputing an Array of all the cases
    val casesArray: MutableList<String> = mutableListOf();
    for (i in 0 until cases) {
        val temp = readLine().toString();
        casesArray.add(temp);
    }
    //Print cases
    var case: Int;
    for (i in 0 until cases) {
        case = i + 1;
        print("Case #$case: ");
        //Calling method with the array of cases
        doubleOrOne(casesArray[i]); 
    }
}
{% endhighlight %}



{% highlight kotlin %}
fun doubleOrOne(word: String) {
    //Making 2 arrays, one for the letter and one for the number of times each letter appears to double it later
    val letter: MutableList<String> = mutableListOf();
    val count: MutableList<Int> = mutableListOf();
    //Counter to know how much times a letter is in the string (next to)
    var counter = 1;
    //Making a new variable for the String received as val cant be changed and var can. 
    //Adding a char that is bigger than all the letters so it can iterate tru all the String as I need to check for i+1
    var firstWord: String = word.plus("·");
    for (i in 0 until firstWord.length - 1) {
        if (firstWord[i] == firstWord[i+1]) {
            counter++;    //counter++ if 2 letters are the same next to each other
        }
        else {
            letter.add(firstWord[i].toString()); //adding the letter
            count.add(counter);                  //adding the counter
            counter = 1;                         //reset counter
        }
    }
    
    //new word that is gonna be created with all the double chars
    var newWord: String = "";
    //iterate tru all the letter variables saved
    for (i in 0 until letter.size - 1) {
        if (letter[i] < letter [i + 1]) {   //if the letter is lower repeat it by the times on count * 2
            repeat(count[i] * 2) { 
                newWord = newWord.plus(letter[i]);
            }
        } else {                            //else just add the count, w/o * 2
            repeat(count[i]) {
                newWord = newWord.plus(letter[i]);
            }
        }
    }
    //as the for is on size - 1 add last letter by the number of times on count
    newWord = newWord.plus(letter[letter.size - 1].repeat(count[count.size - 1]));
    //print final word
    print("$newWord\n");
}
{% endhighlight %}

[cj-dor1]: https://codingcompetitions.withgoogle.com/codejam/round/0000000000877ba5/0000000000aa8e9c