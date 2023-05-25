# MOB 1.2

<!-- ## [Slides](https://make-school-courses.github.io/MOB-1.2-Introduction-to-iOS-Development/Slides/00-Swift-Review/README.html ':ignore') -->

<!-- > -->

## Agenda

- Introduction to the course
- Swift Review

<!-- > -->

## Learning Objectives

By the end of this lesson, students should be able to:

1. Identify the purpose of the course, evaluation criteria and become familiar with navigating the content
1. Complete the practice problems to review Swift

<!-- > -->

## MOB 1.2

- 🤓 Course Description
- 💻 Course Delivery
- 🧠 Course Learning Outcomes
- 🗓 Schedule
- 📓 Assignments & Gradescope
- 💯 Evaluation

<!-- > -->

## Swift Review Pt.1

### Variables and Constants

```
//1. Declare a variable named color of type String, use type annotation.

//2. Assign the value of "purple" to color

//3. Change the value to "red"

//4. Declare a constant named font of type String, use type annotation.

//5. Assign the value of "Helvetica" to font

//6. Change the value to "Arial"

/*
What's the difference between var and let?
How would this exercise look if you used type inference instead of type annotation?
*/
```

### Functions

```
//1. Write a function that takes in a color (String) and prints out "My favorite color is _____"

//2. Call the function

//3. Write a function that takes in a color (String) and *returns* "My favorite color is _____"

//4. Call the function, can you see the result? 

//5. Write a function that takes in a color (String) and a name (String) and returns "_____'s favorite color is _____"

//6. Call the function, can you see the result? 

/*
Did you use internal and external parameter names? If not, try it :)
*/
```

### Conditionals

```
//Write a function called "isEven" that takes in a number and returns a boolean to specify if the input is an even number.

```


### Optionals

```
//Declare a variable called "color" of type optional String

//What values can color store?
//color = "lilac"


//How would you print out the value of "color"?


/*
Review:
- force unwrapping
- optional binding
- guard 
*/
```
### Arrays

```
//1. Define an array called "fruits" and add fruit names.

//2. Print how many elements are stored in the array

//3. Print the second element in the array

//4. Remove the first element in the array

//5. Add another element to the array

//6. Define an Empty array named veggies of type String

/*
Look into:
- Creating an empty array
- Built in methods (like sort)
*/
```


<!-- > -->

**10 min Break** 😌

<!-- > -->

## Swift Review Pt.2

### Dictionaries

```
//1. Define a dictionary called "fruits", the name of the fruit will be the key and the associated emoji will be the value.

//2. Print how many elements are stored in the dictionary

//3. Print the value of an element in the dictionary.

//4. Remove an element from the dictionary

//5. Add another element to the dictionary

```
### For loop

```
//Write a function that takes an Array of Strings as an input and returns a String. The returned String should be all of the items in the input String with a space between each.

/*
For example:
let str = arraytoString(array: ["Swift", "is", "fun!"])
arraytoString(str) // "Swift is fun!"
*/

```

### Enums

```
//1. Create an enum to represent the cardinal directions

//2. Create an instance of the enum and print it to console

//3. Add N, S, E, W as the raw values for each case. Then print the raw 

/*
- Review associated values
*/
```

### Structs & Classes

```
//1. Create a struct to represent a course at Make School
/*
- name
- instructor
- track
- number of students
- term
*/

//2. Create an instance of the struct

//3. Create a class to represent a course at Make School
/*
- name
- instructor
- track
- number of students
- term
*/

//4. Create an instance of the class

/*
Review value vs reference types.
*/
```

<!-- > -->

## What we didn't cover today

- Closure syntax
- OOP

For more practice: [Unwrap App](https://apps.apple.com/us/app/unwrap/id1440611372)

<!-- > -->

## After class

- [Tip Calculator Tutorial](https://makeschool.org/mediabook/oa/tutorials/build-a-tip-calculator-in-swift-4/intro-tip-calculator/)
- [OOP RPG](https://github.com/Tech-at-DU/oop-rpg)
