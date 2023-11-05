# Quiz App (JoelHalkey_hw5TH_csi3150_fs2023)

Quiz App Demo is a computer science based quiz app that allows for timed testing of different computer science terms, each question being given 15 seconds to be answered. Currently there are only 5 questions available.

## Table of Contents
- **[Project Features](#Project-Features)**
- **[Project Structure](#Project-Structure)**
- **[Code Explanation](#Code-Explanation)**
    - CSS
    - JavaScript
    - HTML
<hr>

### App Features
- **Computer Science Topic Quizzing**
- **Timed Quizzing**

<hr>

### Project Structor
<hr>

### Code Explanation

#### CSS
#### JavaScript

``` javascript
restart_quiz.addEventListener("click", (e) => {
  quiz_box.classList.add("activeQuiz"); //show quiz box
  result_box.classList.remove("activeResult"); //hide result box
  timeValue = 15;
  que_count = 0;
  que_numb = 1;
  userScore = 0;
  widthValue = 0;
  showQuetions(que_count); //calling showQestions function
  queCounter(que_numb); //passing que_numb value to queCounter
  clearInterval(counter); //clear counter
  clearInterval(counterLine); //clear counterLine
  startTimer(timeValue); //calling startTimer function
  startTimerLine(widthValue); //calling startTimerLine function
  timeText.textContent = "Time Left"; //change the text of timeText to Time Left
  next_btn.classList.remove("show"); //hide the next button
});
```
#### HTML

<hr>



![ ](https://github.com/JoelHalkey/JoelHalkey_hw5TH_csi3150_fs2023/blob/main/readme_assets/project_structure.png "project structure")