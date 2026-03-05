# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
- List at least two concrete bugs you noticed at the start  
  (for example: "the secret number kept changing" or "the hints were backwards").
  1. The hints provided after making a guess were random. I was making guesses that are smaller than the target secret, but the hints provided were sometimes "Go higher" and sometimes "Go lower". For one instance, I typed 1 as my guess, but the hint told me to go lower, which is impossible for a number guessing game within range 1~100.
  2. The "New Game" button did not work as expected. I tried to use the button to reset the game after I made a correct guess for the current game, but upon clicking the button nothing happened. I checked with information folded in "Developer Debug Info" and saw that the contents were still about the current game, meaning that the button does not work.
  3. The secret generated could be outside of the range provided by Difficulty description. I chose the difficulty "Hard" and refresh the game with the "New Game" button. It has a range of 1 to 50, but the secret shown in "Developer Debug Info" was 69.

---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
  I used Copilot on this project.
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
  Suggestion: the game was giving the wrong directional messgae. I checked n "check_guess" method in app.py, under the TypeError expection, that indeed the hint was given in the opposite direction, that it says "go higher" when the guess is larger than the secret, and vice versa when it says "go lower".

- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).
  When I asked Copilot to generate test cases for the check_guess function, the result it generated, like "Win !", to be compared with the original results, like "Win", "🎉 Correct!", are not the same, even though they are essentially the same. I verified this by checking the code it wrote, and ran the code for which I got all test cases failed to due this issue.

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
  I tried to run the game and test the function which original has bugs with some typical values that would result in different hints, and saw that all of my testing values work as expected.
- Describe at least one test you ran (manual or using pytest)  
   and what it showed you about your code.
  I ran a couple tests using pytest. One of the tests is to test the winning case. The test case is comparing 50 with 50 and the case passed.
- Did AI help you design or understand any tests? How?
  I did received help from AI on designing test cases, as I found it hard to think and write test cases from scratch. With AI generating the cases, I need no worry on this part. Instead I would just need to verify if the test case is correct and makes sense.

---

## 4. What did you learn about Streamlit and state?

- In your own words, explain why the secret number kept changing in the original app.
  The original code keeps alternating the secret number as with every second try the number was converted into a string.
- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
  Basically, Streamlit's "session state" keeps the information about the current game, and "rerun()" function clears the session state and reset this cache for the next, brand new game.
- What change did you make that finally gave the game a stable secret number?
  I changed the code in app.py and made the game produce a stable secret number by deleting the if statement that executes if st.session_state.attempts % 2 == 0.

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
    I would like to have AI to generate some starter test cases first, before I diving deeper for more complex cases, since it is really useful to have some starter ideas before the real work.
- What is one thing you would do differently next time you work with AI on a coding task?
  Instead of using the agent mode to modify code directly, I would like to ask the AI on how and why the fix it suggests should be working.
- In one or two sentences, describe how this project changed the way you think about AI generated code.
  The AI feature of refactoring code is very convenient, as it keeps the whole project clean and organized with ease.
