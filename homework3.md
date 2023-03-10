---
layout: default
title: Homework 3
nav_order: 9
permalink: \homework3
---

# **Homework 3: Penn Course Re(cycler)view**

## **Introduction & App Overview**

In this assignment, you will implement what we covered in the last two modules on **App Architecture** and **RecyclerView**, through Penn Course Re(cycler)view.

**Note: You will work on developing this application throughout HW3 and HW4** 

Penn Course Re(cycler)view allows users to: 

1. Retrieve a list of all _CIS_ classes offered at Penn by section. This includes lectures and recitations. For example,  CIS-160-001 (LEC), CIS-160-201 (REC), etc. This list will be retrieved through the public Penn Labs API (for homework 3 checkpoint, we will use hardcoded data).
2. Scroll through the list of classes using a recyclerview. 
2. View important section information
    * Course Code
    * Course Title
    * Meeting Times
    * Status (Open or Closed)
3. Click on a course to view section-specific information
    * Section Quality
    * Instructor Quality
    * Difficulty
    * Workload

Note: the previous outline is for the full app after HW4 is done. Below is a breakdown of the timeline, explaining which features belong to HW3 and HW4 respectively.

## **Development Timeline**

As mentioned above, you will work on developing Penn Course Re(cycler)view throughout HW3 and HW4. Here is a breakdown of the timeline:

**HW3**
1. Create the RecyclerView to scroll through the list of sections, following the livecoding notes from Lecture 7 - RecyclerView. 
2. Create an XML layout file to hold a course item
3. Create a model data class for a "Section"
4. Follow MVVM architecture by creating a ViewModel an omitting any data form the UI Controller (`MainActivity.kt`)
4. ViewModel holds a fake, hard-coded list of sections to use in the RecyclerView (provided to you below)
5. Implement an onClickListener for RecyclerView items. For now, it will only display a toast.

**HW4**
1. Connect the application to the internet
2. Retrieve a list of sections using Penn Labs API
3. Replace the old hardcoded list with the retrieved list from the API
4. Configure the onClickListener to view section-specific information on click, handled through yet ANOTHER API CALL!

But more on HW4 details later in the HW4 writeup. For now, let's dive into implementing HW3.

## **Instructions**

We recommend following the [livecoding notes](https://github.com/cis1950android/recycler-view-livecoding/blob/main/README.md) from the RecyclerView lecture. You will need to make some modifications, though:

### **Specifications of the Model Data Class**

This app will have **two** model data classes. One will be used for general section info (which appear on the RV list item), and one for specific section details that you typically find on PennCourseReview (which will appear on item click in our app).

For the purposes of this homework assignment, _we will only be creating and focusing on the first model data class_. More on the other one in HW4!

The design of the classes and their arguments is based on the [Penn Labs API](https://penncoursereview.com/api/documentation/#tag/PCx-Section) endpoints for fetching course section data, which we will be using in HW4. 

While it may not make sense to you now why we have two data classes, it will make a lot more sense when we fetch the data from the API. For now, believe it will work and use fake data!

First class - `Section`. Arguments:
- `sectionId : String` (unique id for each section, e.g. "CIS-1200-001")
- `status : String` ("O" for Open, "C" for Closed, "X" for Canceled) Note that this one-letter format is the one used in the API endpoint response, so that's just why we stick to it here to make the transition to HW4 easier.

        WARNING: DO NOT DISPLAY THE LETTER CODE ON SCREEN. YOU HAVE TO MAP IT TO ITS CORRESPONDING CATEGORY AND DISPLAY THE CATEGORY NAME INSTEAD
- `courseTitle : String` (e.g. "Programming Languages and Techniques")
- `semester : String` (The semester of the course (of the form YYYYx where x is A [for spring], B [summer], or C [fall]), e.g. `"2019C"` for fall 2019.)

    |       |  |
    | ----------- | ----------- |
    | `"A"`      | Spring      |
    | `"B"`   | Summer  |
    | `"C"`      | Fall      |

        WARNING: DO NOT DISPLAY THE LETTER CODE ON SCREEN. YOU HAVE TO MAP IT TO ITS CORRESPONDING CATEGORY AND DISPLAY THE CATEGORY NAME INSTEAD

- `activity : String` - a three-letter string that indicates the type of class whether it's a lecture, seminar, recitation, etc. Here is a full list of possible activity values:


    |       |  |
    | ----------- | ----------- |
    | `"CLN"`      | Clinic      |
    | `"DIS"`   | Dissertation  |
    | `"IND"`      | Independent Study      |
    | `"LAB"`   | Lab  |
    | `"LEC"`      | Lecture      |
    | `"MST"`   | Masters Thesis  |
    | `"REC"`      | Recitation      |
    | `"SEM"`   | Seminar  |
    | `"SRT"`      | Senior Thesis      |
    | `"STU"`   | Studio  |
    | `"***"` | Undefined
 
    Although we will typically encounter `"LEC"` and `"REC"` more than other types, your app should handle all different types to avoid visual errors. This is also based on the API mentioned before which we will be using in the next HW, so it's good practice to start developing with fake data that is identical to fetched data for ease of transition.

        WARNING: DO NOT DISPLAY THE THREE-LETTER CODE ON SCREEN. YOU HAVE TO MAP IT TO ITS CORRESPONDING CATEGORY AND DISPLAY THE CATEGORY NAME INSTEAD

### **Specifications of the Section Item XML**

The xml layout for a RecyclerView item representing a section should contain the following data, which will be retrieved directly from fields in class `Section` defined above:
- Section Code - (e.g. "CIS-1100-001)
- Title - (e.g. "Intro to Comp Prog)
- Status - ("Open", "Closed", or "Canceled")
- Semester - (e.g. Spring 2022)
- Activity Type - (e.g. "Lecture")
- `ImageView` that indicates the **course numbering level and changes dynamically**. For example, a specific image for courses within level `1xxx` (CIS 1600, CIS 1200, etc.), another for level `2xxx` (CIS 2400, CIS 2620, etc.), etc. You should have enough images/icons to handle levels up to and including `9xxx`. The choice of image is up to you, as long as there is a different image for each level.


### **Fake Data Source**

Use this fake data in a `MutableList` in your `ViewModel` to populate the recyclerview: 

```kotlin
Section("CIS-1100-001", "O", "Intro to Comp Prog", "Spring 2023", "LEC")

Section("CIS-1100-201", "C", "Intro to Comp Prog", "Spring 2023", "REC")

Section("CIS-2400-001", "C", "Intro to Comp Systems", "Fall 2022", "LEC")

Section("CIS-3200-001", "X", "Intro to Algorithms", "Spring 2021", "LEC")

Section("CIS-4600-001", "C", "Intractive Comp Graphics", "Spring 2023", "LEC")

Section("CIS-5500-001", "O", "Database & Info Systems", "Spring 2023", "LEC")

Section("CIS-6600-001", "C", "Adv Tpcs in Comp Graphics", "Spring 2023", "SEM")

Section("CIS-7980-401", "O", "Explaining Explanation", "Spring 2023", "LEC")

Section("CIS-8990-076", "C", "PhD Independent Study", "Spring 2023", "IND")

Section("CIS-9950-001", "O", "Dissertation", "Spring 2023", "DIS")
```
Please use this fake list and avoid creating your own. Feel free to try and add other data to it, but do not modify the given data, as it has been curated to be used for grading to cover all test cases.

### **Notes on Code Design & Architecture**

- Make sure you use **ViewBinding** and limit the use of `findViewById()` (ask on Ed when unsure)
- You must implement the app using the MVVM (Model-View-ViewModel) architecture. If your code is not modular, e.g. contains data in the UI controller, you will lose a lot of points.. and more importantly you will have written bad code :( 
- Feel free to implement the RecyclerView directly into `MainActivity` without using fragments. You might have to switch the design a bit in HW4, but that's not to worry about for now.

## **Extra Credit: RV Item Design**
 A huge part of a good looking RecyclerView is good item design. So, on Thursday March 30th, the lecture after this homework is due, we will have an in-class voting on each of your `xml` designs for your RecyclerView item. The top design will get `10 pts` extra, second place gets `7 pts`, and third gets `5 pts`. 

 Here are some tips on creating a visually-appealing design for a RecyclerView item:

 - Use custom fonts! Don't resort to default fonts. They are boring, and more importantly make your app look like any other. Let your own touch shine!
 - Use `CardView` to wrap your item's `xml`! Check the [official docs](https://developer.android.com/develop/ui/views/layout/cardview) and this [tutorial](https://www.geeksforgeeks.org/cardview-in-android-with-example/). It's pretty easy, and makes all the difference!
 - Use icons! Instead of viewing the course status as "Open" or "Closed", you can have an icon that turns green and red accordingly, for instance. Visual elements make the experience a lot smoother and easy on the eye.
 - Use [typographic hierarchy](https://www.techopedia.com/definition/31854/typographic-hierarchy#:~:text=A%20typographic%20hierarchy%20is%20a,in%20a%20set%20of%20data.)! This basically means to have text elements take on different font size and color based on their importance. So in our case, the course code may be the most important so it's black, bold, and large. On the other hand, the course title can have a hint of gray and be a little smaller so it's not the main focus of your item, etc. Play around and have fun with it!

## **Submission**

1. Export the project into a .zip file and submit to [Canvas](https://canvas.upenn.edu/courses/1703225/assignments/11092509) by **Friday 24th of March, 11:59 pm**
