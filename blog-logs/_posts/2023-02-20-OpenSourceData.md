---
layout: post
title:  "Implement Sort-Colors in Java TechLog"
date:   2023-02-20 12:18:25 -0000
category: Log
---
## Sort Colors in Data Structures and algorithms

------------------------------------------------------------------------------------------
<blockquote> <p> Overview: </p> </blockquote> 

Data structures and algorithms open source project is oriented about creating multiple coding challenges with the goal of implementing data structures and algorithms to create an efficient and effective program that can process large amounts of data quickly and accurately.

------------------------------------------------------------------------------------------
<blockquote> <p> Context: </p> </blockquote> 

[Sort Colors][cj-dor1] challenge:

Given an array nums with n objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white, and blue.
We will use the integers 0, 1, and 2 to represent the color red, white, and blue, respectively.
You must solve this problem without using the library's sort function.

Example 1:
* Input: nums = [2,0,2,1,1,0]
* Output: [0,0,1,1,2,2]

Example 2:
* Input: nums = [2,0,1]
* Output: [0,1,2]
 
Constraints:
* n == nu*ms.length
* 1 <= n <= 300
* nums[i] is either 0, 1, or 2.

------------------------------------------------------------------------------------------
<blockquote> <p> Solution: </p> </blockquote> 

The first challenge was to understand how the project I was going to contribute worked, after that, I needed to see the contributing guide so I can follow it, making sure to follow
GitHub's code of conduct for open-source projects, which stipulates that everyone must be gracious, respectful and professional.

In order to contribute, you need to follow these steps:

* Pick an issue and read the description to see if you can work on it.
* Comment on the issue (Example: "Can you assing me this issue please.") so you get that issue assigned.
* Once assigned, fork repository to create a copy in your account.
* Clone the forked repository to your local machine using the git clone command.
* Add question on top of the file you will add.
* Add sample input and output.
* Explain approach with comments.
* Take care of readability.
* Add and Commit changes, don't forget push them too.
* Make sure you are up to date with main project, if not, sync it first. 
* Send a Pull Request against main branch, explain everything on it.

For this, I worked on the `SortColors` class of the program where I solve the challent, my approach was the following:

1. Take 3 Pointers low = 0, mid = 0 and high = nums.length -1;
2. Use loop to iterate the array with condition mid <= high.(Since we only need to check middle elements of low and high).
3. If element is 0 swap with low and low++, mid++.
4. If element is 1 then mid++.
5. If element is 2 then swap with high and high--.

{% highlight java %}
class Solution {
    public void sortColors(int[] nums) {
        int low = 0, mid = 0, high = nums.length-1;

        while(mid <= high){
            if(nums[mid] == 0 ){
                //swap with left
                swap(nums,low, mid );
                low++;
                mid++;
            }else if(nums[mid] == 2){
                swap(nums, mid, high);
                high--;
            }else{
                mid++;
            }
        }
        System.out.println(nums);
    }

    public static void swap(int[] nums, int i, int j){
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
{% endhighlight %}

With the solution added, I just followed the guide instructions explained above to fully contribute to the project, waited for my pull request to be approved and merged and with that, I succesfully contributed for my first time to an open-source project!!

[cj-dor1]: https://leetcode.com/problems/sort-colors/