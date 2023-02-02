---
layout: default
title: Homework 1
nav_order: 7
permalink: \homework1
---

# **Homework 1: Tip Calculator**

## **Introduction & App Overview**

In this homework, you will get to practice with Android UI Design through implementing a simple Tip Calculator.

The app you make will allow users to: 

1. Enter the cost of service
2. Choose tip percentage based on quality of service
3. Calculate the tip based on the cost and percentage
4. Round-up the tip

## **Instructions**

There are **Four** components of this homework. Lucky for you, **three** of which will be done through following official Android Codelabs (walkthrough) that will help you create a functioning app and walk you through layout design and the _very_ simple logic in Kotlin. The **fourth** component will require you to complete an extension to the app you created in the first three steps.

## **_Very Important Note_**

The first three components contain solution codes at the end that you can copy/paste and get most of the homework over with. If you choose to do that, please understand and realize that you are not learning _anything_. This class is not a requirement you are trying to hack, but rather a learning journey that you freely signed up for. There will be office hours, extensions, and all different kinds of accomodations that help you learn and succeed. There is no reason for you to copy/paste without learning.

Note that using the solution code is not considered plagiarism _just for this homework_, since following the instructions in the codelabs will likely result in very similar/almost identical code to the one provided. 

## **Getting Started**

Complete the following component **IN ORDER:**

### **Component 1**

The first component will walk you through creating the layout of the app. There is no Kotlin code in that part. Just getting started with the layout and constraints to make the app look.. cool. You can access it [here](https://developer.android.com/codelabs/basic-android-kotlin-training-xml-layouts). It will walk you through the layout from the very starting point of creating a new project. Follow carefully and make sure to read the documentation without jumping to the code!

### **Component 2**

The second component adds Kotlin code to the layout from component 1 to make the app functional. You can access it [here](https://developer.android.com/codelabs/basic-android-kotlin-training-tip-calculator)

### **Component 3**

The third component enhances the UI by adding icons and modifying the constraints a bit. You can access it [here](https://developer.android.com/codelabs/basic-android-kotlin-training-polished-user-experience). **Note:** _only step 4 (icons) of the codelab is required._

You may notice the color scheme is different from what you left off in component 2. This is normal since we are not completing the entirety of component 3, in which they change the theme and colors as well.

### **Component 4**

In this component, no more Android Codelabs. You are on your own. 

Choose _at least one_ of the following extensions to implement as an addition to the app:

- add another EditText above "Cost of Service" to allow users to enter a budget. Use this budget to set a limit to the total amount paid. That is, ensure that: (cost of service + tip <= budget). If the total cost (cost of service + tip) is greater than the allocated budget, set the color of "Tip Amount: $x" to red, and show a Toast message to warn the user of overspending.

- add a feature to split the tip on a number of people, if that option is on, show the tip amount for every person

- create a custom layout in a new xml in the "res" directory and add it to main_activity.xml at the bottom of the screen, centered horizontally. It should contain:

         recommended tip (use any hardcoded number, assuming that it's a user preference)

        emoji/image that changes based on whether the selected tip is greater than, less than, or equal to the recommended tip. (Recommendation: you might want to you use smile/frowning emojis)

- if you have an idea for another extension of your choice, **you have to talk to Ali** first and check if the level of complexity matches the homework difficulty.


## **Submission**

1. Create a .txt file in the project and write a quick description of the extension that you chose to implement.
2. Export the project into a .zip file and submit to [canvas](https://canvas.upenn.edu/courses/1703225/assignments/11011199) by **Friday 17th of February, 11:59 pm**