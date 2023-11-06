# Quiz App (JoelHalkey_hw5TH_csi3150_fs2023)

Quiz App Demo is a computer science based quiz app that allows for timed testing of different computer science terms and topics, each question being given **15 seconds** to be answered. Currently there are **5 questions** available.

_Disclaimer: This README file is written with the assumption that the reader is familiar with CSS, JavaScript, and HTML._

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

### Brief Code Overview

### CSS

#### Main Box Styling
This styling found in `style.css` is used on all the different boxes of the page, the start, the info, question boxes, and the result box.
```css
.start_btn,
.info_box,
.quiz_box,
.result_box {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}
```

#### Answer Option Styling
This styling is used to style the content within each of the answer options, including the text and icon.
```css
section .option_list .option .icon {
  height: 26px;
  width: 26px;
  border: 2px solid transparent;
  border-radius: 50%;
  text-align: center;
  font-size: 13px;
  pointer-events: none;
  transition: all 0.3s ease;
  line-height: 24px;
}
```
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

This is the functionality for starting the timer when the next question is entered.
```javascript
function startTimer(time) {
  counter = setInterval(timer, 1000);
  function timer() {
    timeCount.textContent = time;              //change the value of timeCount with time value
    time--;                                    //decrement the time value
    if (time < 9) {                            //if timer is less than 9
                    
      let addZero = timeCount.textContent;
      timeCount.textContent = "0" + addZero;   //add a 0 before time value
    }
    if (time < 0) {                            //if timer is less than 0
                        
      clearInterval(counter);                                                     //clear counter
      timeText.textContent = "Time Off";                                          //change the time text to time off
      const allOptions = option_list.children.length;                             //get all option items
      let correcAns = questions[que_count].answer;                                //get correct answer from array
      for (i = 0; i < allOptions; i++) {
        if (option_list.children[i].textContent == correcAns) {                   //if there is an option which is matched to an array answer
          option_list.children[i].setAttribute("class", "option correct");        //add green color to matched option
          option_list.children[i].insertAdjacentHTML("beforeend", tickIconTag);   //add tick icon to matched option
          console.log("Time Off: Auto selected correct answer.");
        }
      }
      for (i = 0; i < allOptions; i++) {
        option_list.children[i].classList.add("disabled");                        //once user select an option then disabled all options
      }
      next_btn.classList.add("show");                                             //show the next button if user selected any option
    }
  }
}
```

The functionality of starting and updating the timer line for each question.
```javascript
function startTimerLine(time) {             // Shows a progress bar mirroring timer value left
  counterLine = setInterval(timer, 29);
  function timer() {
    time += 1;                              //upgrading time value with 1
    time_line.style.width = time + "px";    //increasing width of time_line with px by time value
    if (time > 549) {                       // Shows a progress bar mirroring timer value left
        
      clearInterval(counterLine);           //clear counterLine
    }
  }
}
```

<hr>

### HTML

#### Information and Start Section
`info_box` is the starting section after the start button that lists the rules and contains continue and exit buttons.
```html
<div class="info_box">
    ... <!-- Rules -->
    <div class="buttons">
        <button class="quit">Exit Quiz</button>
        <button class="restart">Continue</button>
    </div>
</div>
```

#### Question Section

`quiz_box` is where you insert questions and answer options, as well adjust the time initially present for the timer.
```html
<div class="quiz_box">
    <header>
        <div class="title">Demo Quiz App in JavaScript</div>
         <div class="timer">
            <div class="time_left_txt">Time Left</div>
            <div class="timer_sec">15</div>
          </div>
        <div class="time_line"></div>
     </header>
     <section>
         <div class="que_text">
             ... <!-- Insert questions from ./js/questions.js -->
         </div>
         <div class="option_list">
             ... <!-- Insert options to questions from ./js/questions.js -->
         </div>
     </section>                 
     <footer>
         ... <!-- Footer of quiz box: Contains next question button-->
     </footer>
 </div>
```
#### Finishing and Result Section
`result_box` is where the results of your quiz are given, and options where you can restart the quiz or quit.
```html
<div class="result_box">
    ... <!-- Icon -->
    <div class="complete_text">You've completed the Quiz!</div>
    <div class="score_text">
        <!-- Insert dynamic user score as Result from JavaScript -->
    </div>
    <div class="buttons">
        <button class="restart">Replay Quiz</button>
        <button class="quit">Quit Quiz</button>
    </div>
</div>
```


####
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
  



