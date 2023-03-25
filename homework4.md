---
layout: default
title: Homework 4
nav_order: 10
permalink: \homework4
---
# **Homework 4: Penn Course Re(cycler)view Pt.2**

## **Introduction & App Overview**

In this assignment, you will complete the work you did in HW3 by replacing the fake data with real Penn CIS course data, fetched from a public API.



## **Development Timeline**

Here is the list of changes you need to make to achieve this:

1. Connect the application to the internet
2. Retrieve a list of sections using Penn Labs API
3. Replace the old hardcoded list with the retrieved list from the API
4. **[Extra Credit]** Configure the onClickListener to view section-specific information on click, handled through yet ANOTHER API CALL!

## **Instructions**

We recommend following the [livecoding notes](https://github.com/cis1950android/livecoding-notes/blob/main/README.md) from the "Connect to the Internet" lecture.

### **Getting familiar with the API**

The API we are using is Penn Labs' public API on PennCourseReview, used to retrieve course and section-specific data. 

Note: a couple of hours before releasing this writeup, the host server for the API docs, found [here](https://penncoursereview.com/api/documentation/), is down. Very unfortunate, but I will include some details on the specific API calls we will be using.

Here are the details for the API call we will be using to fetch a list of CIS courses by section (to replace the fake data used in HW3)

* Base URL: `https://penncoursereview.com/api/base/current/`
* Query parameters (for the purposes of this homework, consider this to be the rest of the URL that you include in the `interface` within `ApiService.kt`): "`search/sections/?search=CIS`"
(Note that typically there is a better method to include query parameters in `Retrofit` which you can find a tutorial for [here](https://howtodoinjava.com/retrofit2/query-path-parameters/) or [here](https://square.github.io/retrofit/2.x/retrofit/index.html?retrofit2/http/Query.html), but feel free to hardcode it like we did with `random_ten` in the livecoding notes, as we are only using "CIS" as a value for "search")
* HTTP Method: `GET`
* Response: `JSON` on the following form:

    ```JSON
        [
            {
                "section_id": "CIS-5200-001",
                "status": "O",
                "activity": "LEC",
                "meeting_times": "[\"MW 1:45 PM - 3:14 PM\"]",
                "instructors": [
                    {
                        "id": 14822,
                        "name": "Jacob R. Gardner"
                    }
                ],
                "course_code": "CIS-5200",
                "course_title": "Machine Learning",
                "semester": "2023C",
                "registration_volume": 0
            }
            .
            .
        ]
    ```
    **Important Note:** notice that the response has more fields than your `Section` class. This is fine as Moshi will only assign fields that have a corresponding variable in the `Section` class and automatically ignore the rest.

### **Model Class Modifications**

You will need to modify your data class `Section` so that it can be used by the Moshi converter to store the server response. We do so by adding an `@Json` annotation for every field in the class. This essentially tells the converter what field of the JSON response should be used to fill the corresponding field in the data class.

* Example: adding `@Json(name = "section_id")` before `val sectionId: String` in `Section.kt`. Notice that we use the name `section_id` from the JSON response description above. 

Your job is to **add similar Json annotations for the rest of the fields** in `Section.kt`. Make sure they are identical to the names used in the JSON response.

And again, you do not need to add any extra fields to `Section.kt`, just use the ones from HW3.

### **Networking Architecture/Code Design**

Follow the architecture included in the livecoding notes for the lecture "Connecting to the internet". This can be summaarized as:

- Create an Api Service class that instantiates a `retrofit` interface & object
- Create a function in your ViewModel that uses the retrofit object to make API calls
- Store the data in a LiveData field in the ViewModel
- Observe the data from the UI controller to display it in the RV through the adapter

And don't forget to add the internet permission in `AndroidManifest.xml`!

## **Extra Credit (20%): Adding onItemClick Behavior**

For the extra credit, the goal is to implement behavior for clicking on a section in the list. The goal is to display more details about the course that this section belongs to in a separate fragment (that will need some architecture modifications if you have only used `MainActivity` with no fragments in HW3) or, much easier, in an Alert Dialog. 

Here is an overview of what to expect implmeneting this:

1. Add another API call that fetch course details to your `Api Service` and `ViewModel` (API Call details below)
2. Add support for onClickListener (follow RV livecoding notes)
3. Create a Model class to store the course details based on the JSON response (more details below)
4. When a click is detected, retrieve the section id of the clicked section, and make a call to the function in the view model that triggers the API call for section-specific details, passing in the section id as a variable. (this will be a little tricky!)
5. Populate the section-specific data class with the data retrieved through the API call
6. Display an AlertDialog (example [here](https://stackoverflow.com/questions/2115758/how-do-i-display-an-alert-dialog-on-android)) or navigate to a new fragment, and display the data from the Model class.

**Note: the data we care about the most is the numerical stats on quality and difficulty, feel free to leave the rest without displaying them**

Here is the API call that fetches the additional information:

* Base URL: same as above
* Sub URL: `search/courses/` (this is the one that replaces `random_ten` from the livecoding notes)
* Query Parameter: `search`, which takes on **only the value of the course number from** `section_id`. Note that you will have to support query parameters in `Retrofit` which you can find a tutorial for [here](https://howtodoinjava.com/retrofit2/query-path-parameters/) or [here](https://square.github.io/retrofit/2.x/retrofit/index.html?retrofit2/http/Query.html), since this parameter cannot be hardcoded but instead varies per request based on the section id
* HTTP Method: `GET`
* Response: `JSON` on the following form:

```JSON
[
    {
        "id": "CIS-1100",
        "title": "Intro To Comp Prog",
        "description": "Introduction to Computer Programming is the first course in our series introducing students to computer science. In this class you will learn the fundamentals of computer programming in Java, with emphasis on applications in science and engineering. You will also learn about the broader field of computer science and algorithmic thinking, the fundamental approach that computer scientists take to solving problems.",
        "semester": "2023C",
        "num_sections": 20,
        "course_quality": 2.701,
        "instructor_quality": 2.704,
        "difficulty": 3.149,
        "work_required": 3.381,
        "recommendation_score": null
    }
]
```
Example: if the section clicked is `CIS-1100-001` then you would only use `CIS-1100` for the second API call (truncate the string) to make the following call: `https://penncoursereview.com/api/base/current/search/courses/?search=CIS-1100`


It is highly encouraged to go to office hours to get help on implementing the extra credit, as it can be tricky and contains many moving parts.

## **Submission**

1. Export the project into a .zip file and submit to [Canvas](https://canvas.upenn.edu/courses/1703225/assignments/11122045) (include a submission comment to indicate if you did the extra credit) by **Friday 7th of April, 11:59 pm**



