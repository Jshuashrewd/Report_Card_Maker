# Student Report Card App: live teaching guide

**How to teach with this:** the student types, you guide. Start with an empty `script.js`. Each step below says what to say, what to type, what to predict, what can go wrong, and how to test. The `checkpoints/` folder holds the code as it should look at the end of Steps 4A, 4B and 4C, for when you need to catch up. Do not show the finished `script.js` until the challenges.

**Grade scale:** A 70–100 · B 60–69 · C 50–59 · D 45–49 · F 0–44.
**Colours (the CSS is ready-made):** A green · B blue · C yellow · D and F red.

| Step | What                                            | Min |
| ---- | ----------------------------------------------- | --- |
| 1    | Data model (array of objects)                   | 8   |
| 2    | HTML structure                                  | 6   |
| 3    | CSS                                             | 4   |
| 4A   | `addSubject()`                                  | 10  |
| 4B   | `renderSubjectList()`                           | 10  |
| 4C   | `generateReport()`                              | 12  |
| 5    | Challenges (colours, print, customise, rebuild) | 10+ |

---

## Step 1: The data model

**Say:** "A report card is a list of subjects. Each subject has two facts: a name and a score."
**New words:** _array_ = a list in order. _object_ = a box of facts with labels. _property_ = one fact (a label and a value).

```text
subjects  (an array)
 [0] → { name: "Mathematics", score: 85 }
 [1] → { name: "English",     score: 72 }
 [2] → { name: "Science",     score: 48 }
```

Open the browser console (F12). The student types:

```js
const subjects = [
  { name: "Mathematics", score: 85 },
  { name: "English", score: 72 },
];
```

**Predict, then test:** `subjects.length` (2) · `subjects[1].name` ("English") · `subjects[0].score` (85).
**Add a card:** `subjects.push({ name: "Science", score: 48 })`, then type `subjects` again.
**Why `const`?** The name always points at the same list. We use `let` for a value that changes, like a running total later.
**Common mistakes:** counting from 1 (arrays start at 0); forgetting a comma between objects; putting quotes around the score (it becomes text, not a number).
**Then in `script.js`:** type the `student` object (`name`, `className` and a method `getTitle`) and `const subjects = [];`. Explain `this` as "this student" and `${ }` as "put a value here".

## Step 2: HTML structure

Open `index.html` and walk through it section by section, asking what each part is for: student information, subject name and score inputs, Add subject button, subject list, Make report card button, report card area, Print button.
**Say:** "Every important element has an id, like a name tag. JavaScript finds them by those names."
**Test:** open the page. It is plain for now.
**Common mistake:** misspelling an id. JavaScript then gets `null` and says it cannot read properties of null.

## Step 3: CSS

The CSS is ready-made so class time goes into JavaScript. Show it, then change one colour at the top (`--navy` or `--accent`) and refresh, so the student sees the power of CSS variables.
**Test:** the page now looks like a school dashboard. Resize the window to see the mobile layout.

## Step 4A: `addSubject()`

**Say:** "This function does four jobs: read, check, store, tidy up."
Type (checkpoint: `checkpoints/step-4a-addSubject.js`):

1. The `const ... = document.getElementById(...)` lines ("find it on the page and give it a short name").
2. `showMessage(text)`.
3. `addSubject()` line by line. Explain `.trim()` (removes extra spaces), `Number()` (turns typed text into a number), `isNaN` ("is not a number"), `return` (stops the function early) and `push`.
4. `addBtn.addEventListener('click', addSubject);`. Explain: no `()` after `addSubject`, because we hand over the function and the click runs it later.

**Predict:** "We add Maths 85. What will the console show?" (an array with one object).
**Test:** add 2 subjects and look at the console. Then try to break it: empty name, score 150, empty score. Each shows the red message and adds nothing.
**Common mistakes:** `addSubject()` with brackets in the listener (it runs at once); forgetting `return` after the message; reading `subjectScoreInput` without `.value`.

## Step 4B: `renderSubjectList()`

**Say:** "The page is only a picture of our array. Whenever the array changes, we clear the picture and draw it again."
First type `getGrade(score)` (if / else if: JavaScript stops at the first true test). **Test in the console:** `getGrade(85)`, `getGrade(45)`, `getGrade(44)`.
**Predict:** `getGrade(70)`? (A, because `>=` includes 70.) `getGrade(59)`? (C.)
Then type `makeSpan(text, className)` (two parameters: the "ingredients" the function needs) and `renderSubjectList()`: clear the list, loop with `for`, `createElement`, `append`.
Finally add `renderSubjectList();` at the end of `addSubject` and one call when the page loads (checkpoint: `checkpoints/step-4b-renderSubjectList.js`).
**Test:** add subjects and watch them appear with grade letters. The colours come later, as a challenge.
**Common mistakes:** forgetting `subjectList.innerHTML = ''` (items repeat); forgetting `let i` in the loop; using `li` before it is created.

## Step 4C: `generateReport()`

**Say:** "Now the finale: the maths, then build the card."
Type, one part at a time:

1. `calculateTotal()`: a piggy-bank loop. `let total = 0`, then add each score. (`let` is needed because `total` changes.)
2. `calculateAverage()`: total divided by the number of subjects. Ask why we divide by `subjects.length`.
3. `getRemark(grade)`.
4. `generateReport()`: check for no subjects, save name and class in `student`, do the maths, build the table rows with a loop, then build the whole card in one **template literal** (a string between backticks where `${ }` drops values in).

**Predict:** "Scores 80 and 60: total? average? grade?" (140, 70, A.)
**Test (checkpoint: `checkpoints/step-4c-generateReport.js`):** with `85, 65, 52, 47, 30` you should see Total 279 / 500, Average 55.8, Overall C. Press Make report card with no subjects too: a message appears.
**Common mistakes:** single quotes instead of backticks for the template; forgetting the `$` before `{`; getting joined-up numbers like "8565" because scores were text (that is why we use `Number()`).

---

## Step 5: Student challenges

Give them one at a time, hints first (`CHALLENGES.md`). Solutions are in `SOLUTIONS.md`: open only if the student is truly stuck.

1. **Grade colours:** A green, B blue, C yellow, D/F red.
2. **Print button:** use `window.print()`.
3. **Customise:** the student enters their own real subjects and class and makes their own report card.
4. **Rebuild from memory:** delete `script.js` and rebuild without looking.

## Final checks (all tested)

Student details can be entered · subjects and scores can be added · the list displays correctly · grades are right at every boundary (44 F, 45 D, 49 D, 50 C, 59 C, 60 B, 69 B, 70 A) · total and average are right · the report card shows everything · grade colours work · Print shows only the report card · empty inputs, letters and scores below 0 or above 100 show a message.

**Notes:** After adding or removing subjects, press Make report card again. The report uses `innerHTML` with template literals, which is fine for a class project on your own computer; a public website would need extra safety checks (a later topic). In the print window, tick "Background graphics" so the colours print.
