# Quiz App (JoelHalkey_hw5TH_csi3150_fs2023)

Quiz App Demo is a computer science based quiz app that allows for timed testing of different computer science terms, each question being given **15 seconds** to be answered. Currently there are **5 questions** available.

## Table of Contents
- **[Project Features](#App-Features)**
- **[Project Structure](#Project-Folder-Structure)**
- **[Code Explanation](#Code-Explanation)**
    - [CSS](#css)
    - [JavaScript](#javascript)
    - [HTML](#html)
<hr>

### App Features
- **Computer Science Quizzing**
- **Learn Computer Science Topics**
- **Timed Questions**

<hr>

### Project Folder Structure
![ ](https://github.com/JoelHalkey/JoelHalkey_hw5TH_csi3150_fs2023/blob/main/readme_assets/project_structure.png "project structure") <br>

The entry point of the app is `index.html`, which uses `style.css` for styling, `quizApp.js` to be able to start, continue through, and restart or quit the quiz. `questions.js` is used by `quizApp.js` and contains the questions for the app, including the question, question number, correct answer, and answer options.
<hr>

### Code Explanation

### CSS
<hr>

### JavaScript



#### <u>Start Functionality</u>

The start button that leads into the information portion of the app
```javascript
start_btn.addEventListener("click", (e) => {
  info_box.classList.add("activeInfo");         //show info box
});
```
The information and starting portion of the app
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



#### <u>Restart Functionality</u>

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
<hr>

### HTML

<hr>



