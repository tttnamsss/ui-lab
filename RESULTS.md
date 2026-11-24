# UI lab results 
  
Tool parts that I chose: 
  
## Part 0 
- Step 0.1, Chrome version: 158.0.8127.37 (รุ่นที่เป็นทางการ) (64 บิต) (cohort: Early Adopters) 
- Step 0.3, ChromeDriver version: 158.0.8127.36 (14d6f648e8cd7ad750a4044200ce94d3321be260-refs/branch-heads/8127@{#1691})
- Step 0.4, locator of Pizza, Please!: $x("//button[normalize-space()='Pizza, Please!']")
- Step 0.4, locator of Excluded tools: $$("select option").map(o => o.textContent.trim())
- Step 0.4, locator of Must be vegetarian: $$("#default-checkbox")
- Step 0.4, locator of Custom Pizza Name: $$("#pizza-name")
- Step 0.5, pizza name, tool and calories of the run by hand: 
  
| Step | Actual result | Pass or fail | 
|------|---------------|--------------| 
| 1    |The heading reads Looking to break out of your pizza routine?|pass| 
| 2    |Max Calories per Slice, Min Number of Toppings, Max Number of Topping, Excluded tools, Must be vegetarian and Custom Pizza Name appear|fail| 
| 3    |The fields show these values|pass| 
| 4    |The answer shows the pizza name, dough, ingredients, a tool other than Knife, and 600 or fewer calories per slice |fail| 
| 5    |The page says Please log in first.|pass| 
| 6    |The page shows Latest pizza recommendations|pass| 
| 7    |The line shows the pizza name with the same tool as in step 4|pass| 
  
## Part 3: Robot Framework 
- robot --version: Robot Framework 7.5.1 (Python 3.12.3 on win32) 
- Step 3.2, failure message for the wrong title: Title should have been 'Web Form' but was 'Web form'.
- Step 3.8, run 1, result, elapsed time and pizza name: 
    - result: 1 test total, 1 passed, 0 failed, 0 skipped
    - Elapsed: 00:00:09.968
    - pizza name = Lab Pizza 20261124-203610
- Step 3.8, run 2, result, elapsed time and pizza name: 
    - result: 1 test total, 1 passed, 0 failed, 0 skipped
    - Elapsed: 00:00:10.078
    - pizza name = Lab Pizza 20261124-204300
  
## Part 4: Cypress 
- node --version, npm --version and npx cypress version: 
    - node --version: v22.14.0
    - npm --version: 10.9.2
    - npx cypress version: 16.2.1
- Step 4.3, failure message for the wrong title: 
```
 1) Web form
       fills in the fields and sends the form:

      Timed out retrying after 10000ms
      + expected - actual

      -'Web form'
      +'Web Form'

```
- Step 4.6, tool and calories in the answer of POST /api/pizza: 
    - Knife
    - 650
- Step 4.7, the line of the admin list that shows your pizza: Lab Pizza 20261124-215228 (tool=Scissors, ingredients_number=6) (newest)

- Step 4.8, run 1, result, duration and pizza name: 
    - result: 1 passing
    - duration: 10 seconds  
    - pizza name: Lab Pizza 20261124-215939
- Step 4.8, run 2, result, duration and pizza name: 
    - result: 1 passing
    - duration: 10 seconds  
    - pizza name: Lab Pizza 20261124-220340

## Part B 
1. Explain why the tests locate Max Calories per Slice through its label instead of its id. Propose a change to the page that would let a test use an id, and state why that change helps a tester.
</br><b><u>Answer</u></b>
The input does not expose a stable id for the test to use, so the test finds it through the visible “Max Calories per Slice” label. The page could give the input an id such as `max-calories-per-slice` and associate the label with it using `for`. A test could then target that stable, unique id directly, without depending on the label text or the input’s position in the DOM.

2. Step 7 of QP-01 compares the tool in the admin list with the tool in the recommendation. Identify the kind of test oracle that this check is, and describe one fault in QuickPizza that it would catch.
</br><b><u>Answer</u></b>
This is a consistency (cross-view) oracle: it checks that the same pizza has the same tool in two views. It would catch a fault where QuickPizza recommends one tool but saves or displays a different tool in the admin list.

3. QP-01 never checks that the pizza is vegetarian. Propose a check that would, and state what the test would need from the page or from another source.
</br><b><u>Answer</u></b>
After requesting a vegetarian pizza, check that its returned ingredients are all vegetarian. The page or API would need to expose the ingredients, and the test would need a trusted source that classifies them (or the API could return a verified vegetarian flag). Checking only that the vegetarian checkbox was selected would not prove the result is vegetarian.

4. Compare the two tools that you used. Describe how each one waited for QuickPizza, how quickly you could write QP-01 with it, and how readable its report, log or video was.
</br><b><u>Answer</u></b>
Robot Framework used SeleniumLibrary's explicit wait keywords, such as waiting for an element or page text, with a 10-second timeout. Cypress automatically retried queries and assertions for up to 10 seconds; I also explicitly waited for the pizza API request with `cy.wait('@pizza')`. I found Cypress quicker to write because its JavaScript commands map directly to the browser actions, while Robot took more setup to define reusable keywords and locators in the resource file. Robot's HTML log is detailed and easy to follow by keyword; Cypress's assertion errors and screenshots/video are useful, though the video is less searchable than a text log.

5. Choose the tool that you would use for the automated UI tests of Project 2, and justify the choice with two reasons from this lab.
</br><b><u>Answer</u></b>
I would use Cypress. Its automatic retrying made the UI checks wait for the page without adding many explicit waits, and its network interception let QP-01 verify the pizza response as well as what appeared in the UI. Its screenshots and recorded video also make failures easier to investigate.

6.  For Part 3, explain where you would change the locator of the calories box if QuickPizza changed it, and how the resource file keeps that change out of the test file.
</br><b><u>Answer</u></b>
I would update the `${MAX CALORIES}` locator variable in `robot/resources/quickpizza.resource`. The test case calls keywords from that resource rather than containing the locator itself, so changing the variable updates the shared keyword behavior without editing `pizza_scenario.robot`.

7.  For Part 4, explain why QP-01 has to be a single test in Cypress, which clears the cookies before each test, and what would go wrong if steps 6 and 7 were a second test.
</br><b><u>Answer</u></b>
Cypress clears cookies before each test to isolate tests. QP-01 therefore keeps the admin login (step 6) and checking the admin list (step 7) in the same test. If step 7 were a second test, the login cookie from step 6 would be cleared before it ran, so the admin page could require logging in again or deny access to the list.
