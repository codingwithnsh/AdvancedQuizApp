# Multi-Screen Quiz App

A comprehensive quiz application developed using MIT App Inventor. This app features multiple screens for adding quiz content, taking quizzes, and viewing the last recorded score.

## Overview

The Multi-Screen Quiz App is designed to be flexible, allowing users to create their own quiz content via a dedicated "Populate" screen. The quiz itself presents questions, checks answers, and keeps track of the user's score, which is then displayed on a "Leaderboard" screen.

## Features

* **Multi-Screen Navigation:** Separate screens for the main menu, populating the quiz, taking the quiz, and viewing the leaderboard.
* **Quiz Population:** Add custom questions and answers via a dedicated input screen, storing them locally using TinyDB.
* **Take Quiz:** Presents questions to the user.
* **Answer Checking:** Compares the user's text input to the stored correct answer (case-insensitive).
* **Score Tracking:** Keeps a running score during the quiz.
* **Visual Feedback:** Displays images indicating correct or incorrect answers.
* **Leaderboard:** Displays the score from the most recently completed quiz.
* **Persistent Data:** Questions, answers, and the last score are stored locally using TinyDB components.

## Requirements

To build and run this application, you will need:

* An account on the MIT App Inventor website (appinventor.mit.edu).
* A computer with internet access.
* An Android device or emulator for testing the application.
* Image files for correct (`Correct.png`) and incorrect (`Incorrect.png`) answer feedback, plus any image for the main menu header (`image_a945fc.png` shows one, possibly `Question.png` based on blocks although not explicitly named). Upload these files to the Media section in the Designer.

## Building the Application

Refer to the `step-to-step_guide.md` file for detailed instructions on how to recreate this application in MIT App Inventor. Note that this involves creating and linking multiple screens.

## How to Use

1.  Launch the application on your Android device.
2.  **Populate the Quiz:**
    * Tap **Populate Quiz** from the main menu.
    * On the Populate screen, enter a question in the "Question:" field and the corresponding answer in the "Answer:" field.
    * Tap **Submit** to save the question and answer. The fields will clear, allowing you to add another.
    * Repeat for all your desired questions.
    * Tap **Done** when finished adding questions. This saves the total number of questions and returns to the main menu.
3.  **Take the Quiz:**
    * Tap **Take Quiz** from the main menu.
    * If questions have been populated, the first question will appear (initially random, then sequential).
    * Read the question and type your answer into the input field.
    * Tap **Submit** to check your answer. Feedback (Correct/Incorrect image) will be shown.
    * Tap **Next** to move to the next question.
    * Continue until all questions are answered.
    * At the end, a "Finished Quiz" message will show your score, and your score will be saved.
    * Tap **Quit Quiz** at any time to exit the quiz screen.
4.  **View Leaderboard:**
    * Tap **Leaderboard** from the main menu.
    * This screen will display the score from the last completed quiz.
    * Tap **<<Back** to return to the main menu.

## Credits

This application was built using the MIT App Inventor platform (appinventor.mit.edu) and utilizes TinyDB components for data persistence.
