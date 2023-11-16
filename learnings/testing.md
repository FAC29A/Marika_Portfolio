# Week 7 -9
Learn how to make sure your code works correctly by creating automated tests. Examples are based on the project <a href=https://fac29a.github.io/marika-daniel-project/> ToDue </a>

## 1. Check that passing a given input into our tests returns the expected output
Ensuring the reliability and accuracy of our tests is crucial for maintaining the quality of the ToDue application. We achieve this by employing assertion functions like `equal` and `notEqual` from `test.helper.js`. These functions help us verify that the actual outcomes of our code match the expected results, which is a cornerstone of effective software testing.
For instance, in the test case for adding a new task, we simulate the user's action of entering a task and triggering the task addition. We then use `equal` to assert that the task is added correctly - both in terms of the task content and the updated length of the `todoList` array.

```javascript
// Test to check if a new task is added correctly
test('should add a new task object to the todoList array', () => {
    taskInput.value = 'Test task'; // Simulate user input
    addTask(); 
    const newTaskTitle = todoList[0]["title"];
    equal(newTaskTitle, 'Test task', 'Title should be equal');
    equal(todoList.length, 1, "Length should be 1");
});
```


## 2. Write tests to mimic the behaviour of a user performing different actions
To ensure our application reacts appropriately to user interactions, we can write tests that mimic these actions. A key area for such testing in our ToDue project is the event listener for the 'Add' button. This listener responds to user clicks, validating input, and updating the task list and DOM accordingly.

```javascript
addButton.addEventListener('click', () => {

    if (taskInput.value.trim().length > 0) {
        const inputValue = taskInput.value.trim().toLowerCase();

        if (todoList.some((task) => task.title.toLowerCase() === inputValue)) {
            alert("You already have this task");
        } else {
            addTask();
        }

        notStartedContainer.innerHTML = '';
        inProgressContainer.innerHTML = '';
        completeContainer.innerHTML = '';
        upDateDom();
    }
});
```

## 3. Write testable, modular functions
Each function is focused on a single responsibility, making them easy to test and maintain. 
An example of such a modular function is `menuOptions`, which manages the interactive elements within each task.

```javascript
// Function to manage menu options for each task
function menuOptions(target1, target2, target3, target4, target5) {
    // Code to handle various interactive elements like start, in-progress, complete, delete options
    // Target for 'completing' a task

    target3.addEventListener("click", (e) => {
        const textSpan = e.target.closest('.task-tile').querySelector('#text-field');
        
        console.log(textSpan.textContent);
    
        const clickIndex = todoList.findIndex(item => item.title === textSpan.textContent);
        todoList[clickIndex]["state"] = "completed"

        notStartedContainer.innerHTML = '';
        inProgressContainer.innerHTML = '';
        completeContainer.innerHTML = '';
        upDateDom()
    });

    target3.addEventListener("keypress", (e) => {
        if (e.key === "Enter") {
            target3.click()
        }
   
        //other code...
    });
```

## 4. Write functions that add, remove or modify DOM nodes
The ToDue application features several functions that dynamically interact with the DOM. This interaction includes adding new tasks to the list, updating their status, and removing them as needed.

```javascript
// Function to update the DOM elements based on the todoList's state
function upDateDom() {
    // Filtering and appending tasks to 'not-started', 'in-progress', and 'completed' sections
    // ...
}
```
## 5. Apply event listeners to HTML form elements
Event listeners are attached to form elements such as buttons and input fields to manage tasks and respond to user actions.

```javascript
// Event listener for the 'Add' button, handling task addition
addButton.addEventListener('click', () => {
    if (taskInput.value.trim().length > 0) {
        // Logic to add a task and update the DOM
        // ...
        upDateDom();
    }
});
```

## 6. Use scope to control what variables are accessible inside functions and blocks
ToDue application utilises the concept of scope effectively to ensure variables are accessible only where needed, preventing accidental interference with the global scope or other functions.

```javascript
// Function to add a new task, illustrating local scope
function addTask() {
    // 'newTask' is a local variable within 'addTask'
    const newTask = new Object();
    newTask.title = taskInput.value;
    newTask.state = "not-started";
    // Pushing newTask to the global todoList array
    todoList.push(newTask);
    // Clearing the input field
    taskInput.value = "";
}
```
