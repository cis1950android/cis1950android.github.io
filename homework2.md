---
layout: default
title: Homework 2
nav_order: 8
permalink: \homework2
---

# **Homework 2: Food Ordering**

## **Introduction & App Overview**

In this homework, you will get to practice with Navigation and Fragments through implementing a simple Food Ordering app.

Note: for the remainder of this writeup, we will assume the cuisine of the app is Cupcakes, but feel free to implement whatever food item you prefer.

The app you create will allow users to: 

1. Select a certain quantity of cupcakes to order
2. Select cupcake flavor
3. Select pickup date
4. View order summary (quantity, flavor, pickup date, and total price)
5. Share order (export order details in text form and share them using Android implicit intents)

## **Instructions & Sample Walkthrough**

This app consists of **Four** screens, each represented by a fragment. The first screen let's you choose the quantity of cupcakes to order. The second screen is for flavor choice. The third screen is for pickup date. The fourth is for order summary, and contains a way for the user to share their order details (like a button or so). The app design is, as covered in class, Single-Activity Multi-Fragment.

Here is a walkthrough of the app:

![App Walkthrough](https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExMTAxYWVjMDgyMzkxMzJlNzIxYzM1MDY1NGM1YWUzYTk0YWUxYzBjMSZjdD1n/ORBnkKEizYDh0TCiCb/giphy.gif)
 

## **Getting Started**

Complete the following components **IN ORDER:**

### **Home Screen**

The home screen should be the _starting destination_ of your navigation graph. It contains (at least) the following elements:

- an image that represents the cuisine (e.g. cute cupcake)
- three (or more) buttons for each quantity (You can also let the user pick a custom quantity through an EditText, if you like). All buttons navigate to the next screen: Flavor Screen.

Note that you will have to pass the quantity of cupcakes from Home Screen to Flavor Screen in order to determine the total price (hint: Safe Args!).

### **Flavor Screen**

The flavor screen contains the following elements:
 
- a radio button group that allow users to pick _one_ flavor for their cupcakes (4-5 options).
- a TextView that displays the total price of the order. The total price is just the price of one cupcake multiplied by the quantity. The choice of price is up to you.
- a button to cancel the order, which should navigate to Home Screen
- a button to continue the order, which navigates to the next screen: Date Screen.

Note that the displayed price _MUST_ depend on the quantity selected at the Home Screen. If the total price is fixed and does not dynamically change with respect to quantity, you will lose points!

Also note that you will find it helpful to use Safe Args to pass the selected flavor, along with quantity, to the next screen, since all these information need to be available for the last screen for Order Summary.

### **Date Screen**

The date screen allows user to pick the pickup date for their order. It contains the following elements:

- a radio button group for the pickup date. The first pickup date should cost more, meaning that if the user chooses the closest date, the displayed price should be higher than other dates. It is okay to hard-code the options for the dates, and we will assume that the first radio button is the closest date with the higher price. You will be given the option to make it dynamic as an extra credit.
- a button to cancel the order, which should navigate to Home Screen
- a button to continue the order, which navigates to the next screen: Order Summary Screen.

Again, make sure to pass the necessary information to the next screen using Safe Args: flavor, quantity, and date.

### **Order Summary Screen**

The order summary screen displays all the choices that the user made so far: quantity of cupcakes, flavor, pickup date, and total price. In addition, there should be a cancel button that takes you back to Home Screen, and a share button that uses implicit intents to share the total order as a text form. You may find it useful to check the live coding from Lecture 5 - App Navigation Pt.2 to get a refresh on how to use implicit intents.

## **Extra Credit (10 pts)** 

In the Date Screen, instead of hardcoding the dates, let the app use the phone system's date to retrieve today's date (and the following 2-3 days) and use them dynamically in the radio button group. That way your app is updated and easy to use any day of the year!

## **Submission**

1. Create a .txt/.md file in the project and indicate if you have implemented the extra credit.
2. Export the project into a .zip file and submit to [canvas](https://canvas.upenn.edu/courses/1703225/assignments/11051538) by **Friday 3rd of March, 11:59 pm**
