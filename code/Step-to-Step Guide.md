# Step-by-Step Guide: Building the Multi-Screen Quiz App in MIT App Inventor

This guide provides instructions on how to construct the Multi-Screen Quiz application using MIT App Inventor, based on the provided screenshots and inferred component usage across multiple screens.

This app requires multiple screens. You will start with `Screen1` and add new screens as needed.

## Screen 1: Main Menu (Designer View)

This screen serves as the navigation hub.

1.  Go to the MIT App Inventor website (appinventor.mit.edu) and start a new project named `MultiScreenQuizApp`. `Screen1` is created automatically.
2.  **Upload Media:** Upload any image files you want to use for the main menu header (`question.png` or similar), and for correct/incorrect feedback (`Correct.png`, `Incorrect.png`).
3.  **Add Image:**
    * From **Palette** > **User Interface**, drag an **`Image`** component onto the Viewer.
    * Select the `Image`. In **Properties**, set **`Picture`** to your main menu header image. Adjust size properties (**`Height`**, **`Width`**) as desired.
    * *Optional:* Rename to `MainMenuImage`.
4.  **Add Buttons:**
    * From **Palette** > **User Interface**, drag three **`Button`** components onto the Viewer, placed vertically below the Image.
    * **Button 1 (Take Quiz):**
        * Select the first `Button`. Set **`Text`** to `Take Quiz`. Set **`Width`** to `Fill parent`.
        * *Optional:* Rename to `ButtonTakeQuiz`.
    * **Button 2 (Populate Quiz):**
        * Select the second `Button`. Set **`Text`** to `Populate Quiz`. Set **`Width`** to `Fill parent`.
        * *Optional:* Rename to `ButtonPopulateQuiz`.
    * **Button 3 (Leaderboard):**
        * Select the third `Button`. Set **`Text`** to `Leaderboard`. Set **`Width`** to `Fill parent`.
        * *Optional:* Rename to `ButtonLeaderboard`.

## Screen 1: Main Menu (Blocks Editor)

Switch to the Blocks Editor for `Screen1`.

1.  **Navigation Blocks:**
    * Click on `ButtonTakeQuiz`. Drag out **`when ButtonTakeQuiz.Click do`**. Inside, use **Built-in** > **Control** > **`open another screen screenName`**. Type `MainMenu` (or the name of the screen you will use for the actual quiz taking) in a **`text`** block for `screenName`.
    * Click on `ButtonPopulateQuiz`. Drag out **`when ButtonPopulateQuiz.Click do`**. Inside, use **`open another screen screenName`**. Type `Populate` in a **`text`** block for `screenName`.
    * Click on `ButtonLeaderboard`. Drag out **`when ButtonLeaderboard.Click do`**. Inside, use **`open another screen screenName`**. Type `LeadBoard` in a **`text`** block for `screenName`.

## Screen: Populate (Designer View)

This screen is for adding questions and answers.

1.  Click **Add Screen...** in the top menu. Name the new screen `Populate`. Click **OK**.
2.  **Add Labels:**
    * From **Palette** > **User Interface**, drag a **`Label`** onto the Viewer. Set **`Text`** to `Question:`. Set **`FontBold`** to `true`.
    * From **Palette** > **User Interface**, drag a **`Label`** onto the Viewer. Set **`Text`** to `Answer:`. Set **`FontBold`** to `true`.
3.  **Add Text Boxes:**
    * From **Palette** > **User Interface**, drag a **`TextBox`** onto the Viewer below the "Question:" label. Set **`Width`** to `Fill parent`.
    * *Optional:* Rename to `QuestionTextBox`.
    * From **Palette** > **User Interface**, drag a **`TextBox`** onto the Viewer below the "Answer:" label. Set **`Width`** to `Fill parent`.
    * *Optional:* Rename to `AnswerTextBox`.
4.  **Add Buttons:**
    * From **Palette** > **User Interface**, drag a **`Button`** onto the Viewer below the TextBoxes. Set **`Text`** to `Submit`. Set **`Width`** to `Fill parent`.
    * *Optional:* Rename to `SubmitButton`.
    * From **Palette** > **User Interface**, drag a **`Button`** onto the Viewer below the Submit button. Set **`Text`** to `Done`. Set **`Width`** to `Fill parent`.
    * *Optional:* Rename to `DoneButton`.
5.  **Add TinyDB Components:**
    * From **Palette** > **Storage**, drag two **`TinyDB`** components onto the Viewer. They will appear in the "Non-visible components" area.
    * *Optional:* Rename one to `Db_QuestionAnswer` (for Q&A) and the other to `Db_Parameters` (for storing total questions).

## Screen: Populate (Blocks Editor)

Switch to the Blocks Editor for the `Populate` screen.

1.  **Initialize Global Counter:**
    * Click on **Built-in** > **Variables**. Drag out **`initialize global name to`**.
    * Rename `name` to `question_counter`.
    * Click on **Built-in** > **Math**. Drag out a **`number`** block (with `0`) and snap it in.

2.  **Submit Button Logic:**
    * Click on `SubmitButton`. Drag out **`when SubmitButton.Click do`**.
    * Inside:
        * Store Question:
            * Click on `Db_QuestionAnswer` (or your renamed Q&A TinyDB). Drag out **`call Db_QuestionAnswer.StoreValue tag valueToStore`**.
            * For `tag`: Click **Built-in** > **Text**. Drag out **`join`**. Drag a **`text`** block (`"Q"`) into the first socket. Click **Built-in** > **Variables**. Drag out **`get global question_counter`** and snap it into the second socket.
            * For `valueToStore`: Click on `QuestionTextBox`. Drag out **`QuestionTextBox.Text`**. Snap the `join` block into `tag` and the `QuestionTextBox.Text` into `valueToStore`.
        * Store Answer:
            * Click on `Db_QuestionAnswer`. Drag out **`call Db_QuestionAnswer.StoreValue tag valueToStore`**.
            * For `tag`: Click **Built-in** > **Text**. Drag out **`join`**. Drag a **`text`** block (`"A"`) into the first socket. Click **Built-in** > **Variables**. Drag out **`get global question_counter`** and snap it into the second socket.
            * For `valueToStore`: Click on `AnswerTextBox`. Drag out **`AnswerTextBox.Text`**. Snap the `join` block into `tag` and the `AnswerTextBox.Text` into `valueToStore`.
        * Increment Counter:
            * Click on **Built-in** > **Variables**. Drag out **`set global question_counter to`**.
            * Click on **Built-in** > **Math**. Drag out **`+`**. Get **`get global question_counter`** and a **`number`** block (`1`). Snap them into `+`. Snap `+` into `set global question_counter`.
        * Clear Text Boxes:
            * Click on `QuestionTextBox`. Drag out **`set QuestionTextBox.Text to`**. Use an empty **`text`** block (`""`).
            * Click on `AnswerTextBox`. Drag out **`set AnswerTextBox.Text to`**. Use an empty **`text`** block (`""`).

3.  **Done Button Logic:**
    * Click on `DoneButton`. Drag out **`when DoneButton.Click do`**.
    * Inside:
        * Store Total Questions:
            * Click on `Db_Parameters` (or your renamed parameters TinyDB). Drag out **`call Db_Parameters.StoreValue tag valueToStore`**.
            * For `tag`: Use a **`text`** block (`"NoQs"`).
            * For `valueToStore`: Click on **Built-in** > **Variables**. Drag out **`get global question_counter`**. Snap the blocks into `StoreValue`.
        * Go back to Main Menu:
            * Click on **Built-in** > **Control**. Drag out **`open another screen screenName`**. Type `Screen1` in a **`text`** block for `screenName`.

## Screen: LeadBoard (Designer View)

This screen displays the last quiz score.

1.  Click **Add Screen...** Name it `LeadBoard`. Click **OK**.
2.  **Add Title Label:**
    * From **Palette** > **User Interface**, drag a **`Label`** onto the Viewer. Set **`Text`** to `Leader Board`. Set **`TextAlignment`** to `Center`. Set **`FontBold`** to `true`. Set **`BackgroundColor`** to `Green` (optional, based on screenshot). Set **`Width`** to `Fill parent`.
    * *Optional:* Rename to `LeaderboardTitleLabel`.
3.  **Add Score Display Labels:**
    * From **Palette** > **User Interface**, drag two **`Label`** components onto the Viewer below the title.
    * **Label 1 (Person Text):**
        * Select the first Label. Set **`Text`** to `Person:`. Set **`FontBold`** to `true`.
        * *Optional:* Rename to `LabelPerson`.
    * **Label 2 (Score Value):**
        * Select the second Label. Set **`Text`** to `Score Value`. Set **`FontBold`** to `true`. Set **`Width`** to `Fill parent`.
        * *Optional:* Rename to `LabelScoreValue`.
4.  **Add Back Button:**
    * From **Palette** > **User Interface**, drag a **`Button`** onto the Viewer below the labels. Set **`Text`** to `<<Back`. Set **`Width`** to `Fill parent`.
    * *Optional:* Rename to `BackButton`.
5.  **Add TinyDB Component:**
    * From **Palette** > **Storage**, drag a **`TinyDB`** component onto the Viewer. This should be the same instance used to store the score (`Db_Parameters` if you followed the naming suggestion).

## Screen: LeadBoard (Blocks Editor)

Switch to the Blocks Editor for the `LeadBoard` screen.

1.  **Screen Initialization:**
    * Click on `LeadBoard` (or your screen name). Drag out **`when LeadBoard.Initialize do`**.
    * Inside:
        * Set Person Label (based on screenshot, it just says "Person:"):
            * Click on `LabelPerson`. Drag out **`set LabelPerson.Text to`**. Use a **`text`** block (`"Person:"`).
        * Get and Set Score Label:
            * Click on `LabelScoreValue`. Drag out **`set LabelScoreValue.Text to`**.
            * Click on `Db_Parameters` (or your renamed TinyDB). Drag out **`call Db_Parameters.GetValue tag valueIfTagNotThere`**.
            * For `tag`: Use a **`text`** block (`"score"`).
            * For `valueIfTagNotThere`: Use a **`text`** block (`""`) or a **`number`** block (`0`) for a default value if no score is found. Snap the `GetValue` block into the `set LabelScoreValue.Text` socket.

2.  **Back Button Logic:**
    * Click on `BackButton`. Drag out **`when BackButton.Click do`**.
    * Inside, use **Built-in** > **Control** > **`close screen`**.

## Screen: Take Quiz (Based on the screenshots, this seems to be the MainMenu screen itself, or a screen that uses the name MainMenu in the Blocks)

Let's assume the "Take Quiz" logic is implemented on the `MainMenu` screen itself (which might have been renamed from `Screen1` in the blocks shown). If you created a separate screen for the quiz, adjust component names and screen initialization accordingly. Based on the provided blocks, the screen handling the quiz logic is named `MainMenu`.

**If you are using `Screen1` for the quiz:** Go back to the `Screen1` Blocks Editor. The `MainMenu.Initialize` block shown in the screenshot will be `Screen1.Initialize`.

**If you created a separate screen named `MainMenu` for the quiz:**
1.  Click **Add Screen...** Name it `MainMenu`. Click **OK**.
2.  Go to the `MainMenu` Designer view.

**Screen: Take Quiz (Designer View)**

1.  **Add Labels:**
    * From **Palette** > **User Interface**, drag a **`Label`** onto the Viewer. Set **`Text`** to `Question:`. Set **`FontBold`** to `true`.
    * From **Palette** > **User Interface**, drag another **`Label`** below the "Question:" label. Set its initial **`Text`** to something like "..." or leave empty. Set **`Width`** to `Fill parent`.
    * *Optional:* Rename to `QuestionTextLabel`.
2.  **Add Answer Input:**
    * From **Palette** > **User Interface**, drag a **`TextBox`** onto the Viewer below the question text label. Set **`Width`** to `Fill parent`. Set **`Hint`** to `Enter your answer here`.
    * *Optional:* Rename to `AnswerTextBox`.
3.  **Add Submit and Next Buttons:**
    * From **Palette** > **Layout**, drag a **`HorizontalArrangement`** below the TextBox. Set **`Width`** to `Fill parent`. Set **`AlignHorizontal`** to `Center`.
    * From **Palette** > **User Interface**, drag two **`Button`** components into the `HorizontalArrangement`.
    * **Button 1 (Submit):** Set **`Text`** to `Submit`. *Optional:* Rename to `SubmitButton`.
    * **Button 2 (Next):** Set **`Text`** to `Next`. Set **`Visible`** to `false` initially. *Optional:* Rename to `NextButton`.
4.  **Add Image for Feedback:**
    * From **Palette** > **User Interface**, drag an **`Image`** component onto the Viewer below the HorizontalArrangement. You will set its picture in the blocks. Adjust size as needed.
    * *Optional:* Rename to `FeedbackImage`.
5.  **Add Quit Button:**
    * From **Palette** > **User Interface**, drag a **`Button`** onto the Viewer below the Feedback Image. Set **`Text`** to `Quit Quiz`. Set **`Width`** to `Fill parent`.
    * *Optional:* Rename to `QuitButton`.
6.  **Add TinyDB and Notifier Components:**
    * From **Palette** > **Storage**, drag two **`TinyDB`** components onto the Viewer. These should be the instances you used for Q&A (`Db_QuestionAnswer`) and Parameters (`Db_Parameters`).
    * From **Palette** > **User Interface**, drag a **`Notifier`** component onto the Viewer.

## Screen: Take Quiz (Blocks Editor - `MainMenu` or `Screen1`)

Switch to the Blocks Editor for the screen you are using for the quiz (`MainMenu` or `Screen1`).

1.  **Initialize Global Variables:**
    * Click on **Built-in** > **Variables**. Drag out three **`initialize global name to`** blocks.
    * **Score:** Rename to `Score`. Initialize to `0` using a **`number`** block.
    * **Question Number (for retrieval/checking):** Rename to `question_No` (or `global question_No` as in the screenshot). Initialize to `0` using a **`number`** block.
    * **Another Question Variable (Confusing, but in screenshot):** Rename to `question_question` (as in screenshot). Initialize to `0` using a **`number`** block. *Note: The purpose of this variable is unclear from the blocks shown, but include it to match the screenshot.*

2.  **Procedure to Display Question:**
    * Click on **Built-in** > **Procedures**. Drag out **`to name do`**.
    * Rename `name` to `display_Question`.
    * Inside the `display_Question` procedure block:
        * Get total questions:
            * Click on `Db_Parameters`. Drag out **`call Db_Parameters.GetValue tag valueIfTagNotThere`**. Use `text` block `"NoQs"` for `tag` and a `number` block `0` for `valueIfTagNotThere`.
        * Pick a random question number:
            * Click on **Built-in** > **Variables**. Drag out **`set global question_No to`**.
            * Click on **Built-in** > **Math**. Drag out **`random integer from 1 to`**.
            * Snap the `GetValue` block (that gets `NoQs`) into the `to` socket of `random integer`.
            * Snap the `random integer` block into the `set global question_No to` socket.
        * Display the question text:
            * Click on `QuestionTextLabel`. Drag out **`set QuestionTextLabel.Text to`**.
            * Click on `Db_QuestionAnswer`. Drag out **`call Db_QuestionAnswer.GetValue tag valueIfTagNotThere`**.
            * For `tag`: Click **Built-in** > **Text**. Drag out **`join`**. Drag a **`text`** block (`"Q"`) into the first socket. Get **`get global question_No`** and snap into the second.
            * For `valueIfTagNotThere`: Use a **`text`** block (`"Error: Question not found"`). Snap the `GetValue` block into the `set QuestionTextLabel.Text` socket.
        * Reset Image:
            * Click on `FeedbackImage`. Drag out **`set FeedbackImage.Picture to`**. Use an empty **`text`** block (`""`).
        * Clear Answer TextBox:
            * Click on `AnswerTextBox`. Drag out **`set AnswerTextBox.Text to`**. Use an empty **`text`** block (`""`).

3.  **Screen Initialization (`MainMenu.Initialize` or `Screen1.Initialize`):**
    * Click on your screen (e.g., `MainMenu`). Drag out **`when MainMenu.Initialize do`**.
    * Inside:
        * Get total questions (`NoQs`):
            * Click on `Db_Parameters`. Drag out **`call Db_Parameters.GetValue tag valueIfTagNotThere`**. Use `text` block `"NoQs"` for `tag` and a `number` block `0` for `valueIfTagNotThere`.
        * Check if questions exist:
            * Click on **Built-in** > **Control**. Drag out **`if then else`**.
            * Click on **Built-in** > **Logic**. Drag out the **`=`** comparison block.
            * Snap the `GetValue` block (for `NoQs`) into the first socket of `=`.
            * Click on **Built-in** > **Math**. Drag out a **`number`** block (with `0`) and snap into the second socket of `=`. Snap the `=` block into the `if` condition.
        * If no questions:
            * Inside the `then` part:
                * Click on `Notifier1`. Drag out **`call Notifier1.ShowMessageDialog message title buttonText`**.
                * For `message`: Use a `text` block (`"THERE ARE NO QUESTIONS SET GO TO POPULATE SECTI..."`).
                * For `title`: Use a `text` block (`"ERROR"`).
                * For `buttonText`: Use a `text` block (`"OK"`).
        * If questions exist:
            * Inside the `else` part:
                * Click on **Built-in** > **Procedures**. Drag out **`call display_Question`**.

4.  **Quit Button Logic:**
    * Click on `QuitButton`. Drag out **`when QuitButton.Click do`**.
    * Inside, use **Built-in** > **Control** > **`close screen`**.

5.  **Submit Button Logic:**
    * Click on `SubmitButton`. Drag out **`when SubmitButton.Click do`**.
    * Inside:
        * Hide Keyboard:
            * Click on `AnswerTextBox`. Drag out **`call AnswerTextBox.HideKeyboard`**.
        * Get the correct answer:
            * Click on `Db_QuestionAnswer`. Drag out **`call Db_QuestionAnswer.GetValue tag valueIfTagNotThere`**.
            * For `tag`: Click **Built-in** > **Text**. Drag out **`join`**. Drag a **`text`** block (`"A"`) into the first socket. Get **`get global question_No`** and snap into the second.
            * For `valueIfTagNotThere`: Use a **`text`** block (`""`).
        * Compare Answer (Case Insensitive):
            * Click on **Built-in** > **Control**. Drag out **`if then else`**.
            * Click on **Built-in** > **Text**. Drag out **`compare texts piece1 piece2`**.
            * For `piece1`: Click on **Built-in** > **Text**. Drag out **`upcase text`**. Click on `AnswerTextBox`. Drag out **`AnswerTextBox.Text`** and snap into the `text` socket of `upcase`.
            * For `piece2`: Click on **Built-in** > **Text**. Drag out **`upcase text`**. Snap the `GetValue` block (for the answer) into the `text` socket of `upcase`.
            * Set the comparison operator dropdown to `=`. Snap the entire `compare texts` block into the `if` condition.
        * If Correct:
            * Inside the `then` part:
                * Click on **Built-in** > **Variables**. Drag out **`set global Score to`**.
                * Click on **Built-in** > **Math**. Drag out **`+`**. Get **`get global Score`** and a **`number`** block (`1`). Snap them into `+`. Snap `+` into `set global Score`.
                * Click on `FeedbackImage`. Drag out **`set FeedbackImage.Picture to`**. Use a **`text`** block (`"Correct.png"`).
        * If Incorrect:
            * Inside the `else` part:
                * Click on `FeedbackImage`. Drag out **`set FeedbackImage.Picture to`**. Use a **`text`** block (`"Incorrect.png"`).
        * Hide Submit and Show Next:
            * Click on `SubmitButton`. Drag out **`set SubmitButton.Visible to`**. Use **Built-in** > **Logic** > **`false`**.
            * Click on `NextButton`. Drag out **`set NextButton.Visible to`**. Use **Built-in** > **Logic** > **`true`**.

6.  **Next Button Logic:**
    * Click on `NextButton`. Drag out **`when NextButton.Click do`**.
    * Inside:
        * Get total questions (`NoQs`):
            * Click on `Db_Parameters`. Drag out **`call Db_Parameters.GetValue tag valueIfTagNotThere`**. Use `text` block `"NoQs"` for `tag` and a `number` block `0` for `valueIfTagNotThere`.
        * Increment Question Number (for sequential progression *after* the first random one, based on screenshot logic):
            * Click on **Built-in** > **Variables**. Drag out **`set global question_No to`**.
            * Click on **Built-in** > **Math**. Drag out **`+`**. Get **`get global question_No`** and a **`number`** block (`1`). Snap them into `+`. Snap `+` into `set global question_No`.
        * Check if all questions answered:
            * Click on **Built-in** > **Control**. Drag out **`if then else`**.
            * Click on **Built-in** > **Math**. Drag out the **`>`** comparison block.
            * Click on **Built-in** > **Variables**. Drag out **`get global question_No`** and snap into the first socket of `>`.
            * Snap the `GetValue` block (for `NoQs`) into the second socket of `>`. Snap the `>` block into the `if` condition.
        * If quiz finished (`global question_No` > `NoQs`):
            * Inside the `then` part:
                * Show Finished Dialog with Score:
                    * Click on `Notifier1`. Drag out **`call Notifier1.ShowMessageDialog message title buttonText`**.
                    * For `message`: Click **Built-in** > **Text**. Drag out **`join`**. Add more sockets by clicking the gear. Add text blocks and the score: `"You have finished all the question and answer\nYour Score is "`, **`get global Score`**, `" out of "`, the `GetValue` block for `NoQs`.
                    * For `title`: Use a `text` block (`"Finished Quiz"`).
                    * For `buttonText`: Use a `text` block (`"Done"`).
                * Store the final score:
                    * Click on `Db_Parameters`. Drag out **`call Db_Parameters.StoreValue tag valueToStore`**.
                    * For `tag`: Use a **`text`** block (`"score"`).
                    * For `valueToStore`: Get **`get global Score`**. Snap the blocks into `StoreValue`.
                * Close the quiz screen:
                    * Click on **Built-in** > **Control**. Drag out **`close screen`**.
        * If more questions remain:
            * Inside the `else` part:
                * Show Submit and Hide Next:
                    * Click on `SubmitButton`. Drag out **`set SubmitButton.Visible to`**. Use **`true`**.
                    * Click on `NextButton`. Drag out **`set NextButton.Visible to`**. Use **`false`**.
                * Display the next question:
                    * Click on **Built-in** > **Procedures**. Drag out **`call display_Question`**. *Note: Based on the blocks, `display_Question` picks a random question. The sequential increment of `global question_No` in the Next button logic combined with calling `display_Question` afterwards seems inconsistent with purely random or purely sequential. This implementation appears to increment the counter and then display a random question, which might lead to repeating questions or skipping some. However, the screenshot shows it calling `display_Question` here, so we'll include it as shown.* *Correction based on re-reading code 3:* The `display_Question` procedure *initially* gets a random question number and sets `global question_No`. The `Next.Click` block *increments* `global question_No` and then calls `display_Question`. Inside `display_Question`, it *again* gets a *random* integer based on the *total* number of questions. This means clicking "Next" doesn't necessarily go to the *next* sequential question after the initial random one; it just increments the counter and then picks *another* random question (or potentially the same one). The logic for ending the quiz is based on this incremented `global question_No` exceeding the total number of questions. This block logic is unusual for a standard quiz flow. A more typical flow would be to either always pick random questions without incrementing a counter, or to increment a counter and select questions sequentially. Let's stick to describing what the blocks *do* as shown: increment a counter, then call a procedure that picks a new random question. The quiz ends when the counter exceeds the total number of questions, which might happen unpredictably depending on the random numbers picked. *Further Correction:* Looking *very* closely at the blocks in code 3, the `display_Question` procedure *sets* `global question_No` to a random integer. The `Next.Click` block *increments* `global question_No` *before* calling `display_Question`. This means the `global question_No` used to retrieve the question in `display_Question` is the *new random number* generated within `display_Question`, not the incremented value from the `Next.Click` block. The incremented value is *only* used to check if the quiz is over. This is indeed a very unusual logic flow.

Let's try to interpret the `Next.Click` and `display_Question` relationship again.
- `MainMenu.Initialize`: Calls `display_Question`. `display_Question` gets `NoQs`, picks random number `r` from 1 to `NoQs`, sets `global question_No = r`, and displays question `r`.
- `Next.Click`: Increments `global question_No`. If `global question_No > NoQs`, quiz ends. Else, show Submit/Hide Next, *call display_Question*. When `display_Question` is called *again*, it *again* gets `NoQs`, picks *another* random number `r2` from 1 to `NoQs`, sets `global question_No = r2`, and displays question `r2`.

So, the quiz flow is:
1. Start: Display a random question.
2. Next: Increment a counter (`global question_No`, which *also* holds the *currently displayed random question index* from the previous step). Check if this incremented counter exceeds the total number of questions. If yes, end quiz. If no, display *another* random question, overwriting the previous `global question_No`.

This logic means the quiz doesn't progress through questions sequentially after the first random one, and the `global question_No` variable is overloaded, holding both a counter for quiz completion and the index of the currently displayed random question. The quiz ends after a number of "Next" clicks equal to `NoQs`, regardless of which questions were actually displayed.

Let's simplify the description in the guide to reflect this unusual behavior accurately but clearly. The quiz progresses by showing random questions, and the end condition is based on the number of times "Next" has been clicked.

## Step 4: Testing the Application

1.  In the App Inventor web interface, click **Connect** in the top menu.
2.  Choose either "AI Companion" or "Emulator".
3.  First, go to the **Populate Quiz** screen and add some questions and answers. Tap **Done**.
4.  Go to the **Take Quiz** screen. The first question (randomly selected) should appear.
5.  Type an answer and tap **Submit**. Verify the feedback image appears.
6.  Tap **Next**. A new random question will appear. Repeat submitting answers and tapping next.
7.  After tapping "Next" approximately `NoQs` times, the quiz finished dialog should appear with your score.
8.  Go to the **Leaderboard** screen and verify your score is displayed.

You have successfully built the Multi-Screen Quiz application with data persistence!
