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
| 1    |The heading reads Looking to break 
out of your pizza routine?|pass| 
| 2    |Max Calories per Slice, Min Number of Toppings, Max Number of Topping, Excluded 
tools, Must be vegetarian and 
Custom Pizza Name appear|fail| 
| 3    |The fields show these values|pass| 
| 4    |The answer shows the pizza name, dough, ingredients, a 
tool other than Knife, and 600 or 
fewer calories per slice |fail| 
| 5    |The page says Please log in first.|pass| 
| 6    |The page shows Latest pizza 
recommendations|pass| 
| 7    |The line shows the pizza name with 
the same tool as in step 4|pass| 
  
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
- Step 4.8, run 2, result, duration and pizza name: 
  
## Part B 
1. 
2. 
3. 
4. 
6. 
7. 
