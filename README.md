# Quiz App (JoelHalkey_hw5TH_csi3150_fs2023)

Quiz App Demo is a computer science based quiz app that allows for timed testing of different computer science terms, each question being given **15 seconds** to be answered. Currently there are **5 questions** available.

_Disclaimer: This README file is written with the assumption that the reader is familiar with HTML, CSS, and JavaScript._

## Table of Contents
- **[App Features](#App-Features)**
- **[App Folder Structure](#Project-Folder-Structure)**
- **[Code Overview](#Code-Overview)**
    - [CSS](#css)
    - [JavaScript](#javascript)
    - [HTML](#html)
- **[Individual Implementation](#Individual-Implementation)**
<hr>

### App Features
- **Computer Science Quizzing**
- **Learn Correct Answers**
- **Timed Questions**
<hr>

### Project Folder Structure
![ ](https://github.com/JoelHalkey/JoelHalkey_hw5TH_csi3150_fs2023/blob/main/readme_assets/project_structure.png "project structure") <br>

The entry point of the app is `index.html`, which uses `style.css` for styling, `quizApp.js` to be able to start, continue through, and restart or quit the quiz. `questions.js` is used by `quizApp.js` and contains the questions for the app, including the question, question number, correct answer, and answer options.
<hr>

### Code Overview

### CSS
<hr>

### JavaScript



#### Start Functionality

The start button that leads into the information portion of the app.
```javascript
start_btn.addEventListener("click", (e) => {
  info_box.classList.add("activeInfo");         //show info box
});
```
The information and starting portion of the app.
``` javascript
continue_btn.addEventListener("click", (e) => {
  info_box.classList.remove("activeInfo");      //hide info box
  quiz_box.classList.add("activeQuiz");         //show quiz box
  showQuetions(0);                              //calling showQestions function
  queCounter(1);                                //passing 1 parameter to queCounter
  startTimer(15);                               //calling startTimer function
  startTimerLine(0);                            //calling startTimerLine function
});
```

#### Next Question Functionality
``` javascript
next_btn.addEventListener("click", (e) => {
  if (que_count < questions.length - 1) {       //check if it does not exceed max questions
    que_count++;                                //increment the que_count value
    que_numb++;                                 //increment the que_numb value
    showQuetions(que_count);                    //calling showQestions function
    queCounter(que_numb);                       //passing que_numb value to queCounter
    clearInterval(counter);                     //clear counter
    clearInterval(counterLine);                 //clear counterLine
    startTimer(timeValue);                      //calling startTimer function
    startTimerLine(widthValue);                 //calling startTimerLine function
    timeText.textContent = "Time Left";         //change the timeText to Time Left
    next_btn.classList.remove("show");          //hide the next button
  } else {
    clearInterval(counter);                     //clear counter
    clearInterval(counterLine);                 //clear counterLine
    showResult();                               //calling showResult function
  }
});
```



#### Restart Functionality

The ending portion of the application where the results are shown, and restart and quit options are available.
``` javascript
restart_quiz.addEventListener("click", (e) => {
  quiz_box.classList.add("activeQuiz");         //show quiz box
  result_box.classList.remove("activeResult");  //hide result box
  timeValue = 15;
  que_count = 0;
  que_numb = 1;
  userScore = 0;
  widthValue = 0;
  showQuetions(que_count);                      //calling showQestions function
  queCounter(que_numb);                         //passing que_numb value to queCounter
  clearInterval(counter);                       //clear counter
  clearInterval(counterLine);                   //clear counterLine
  startTimer(timeValue);                        //calling startTimer function
  startTimerLine(widthValue);                   //calling startTimerLine function
  timeText.textContent = "Time Left";           //change the text of timeText to Time Left
  next_btn.classList.remove("show");            //hide the next button
});
```

#### Quit Functionality

The functionality of the quit button, which reloads the window and starts back at the beginning.
```javascript
quit_quiz.addEventListener("click", (e) => {
  window.location.reload();                     //reload the current window
});
```

#### Timer Functionality

<hr>

### HTML

<hr>

### Individual Implementation

While implementing your own version of this, if you want to keep similar functionality, here are ways that you can add to:
- **The number of questions:**<br>
  `To be able to change the number of questions, you can simply just add to the questions in the questions.js file.`
  ```javascript
    let questions = [
  {
    numb: 1,
    question: "What does HTML stand for?",
    answer: "Hyper Text Markup Language",
    options: [
      "Hyper Text Preprocessor",
      "Hyper Text Markup Language",
      "Hyper Text Multiple Language",
      "Hyper Tool Multi Language",
    ],
  },
  ...
  ```
- **The timer**<br>
  `To be able to change the amount of time given for each question, you can just change the timer variable in quizApp.js`
  ```javascript
    let timeValue = 15;                         // Change this value you to your desired time.
  ```
- **The order of the answer options:**<br>
  `To be able to change the order of the answer options, consider loading the different options into an array, shuffling it, then loading the options via the indexes of that array.`
  



