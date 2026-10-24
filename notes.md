# HTTP observations (Lab 4, Task 1)
 
| Question | My answer |
|----------|-----------|
| Request method for index.html | ... |
| Status code with Disable cache ticked | ... |
| Status code on a normal reload | ... |
| Status code for /nothing-here.html | ... |
| Value of the Content-Type response header | ... |
| Remote Address (IP and port) | ... |
| Protocol in the address bar (http or https) | ... |
 
## Why is this address http and not https?
HTTPS secures the information that is sent over a network so that no one else can read it. My localhost address (127.0.0.1) is my own computer. So the data never leaves my computer and there is nothing to protect on the way.

## Storage and security (Lab 4,Task 3, Step 3.6)

localStorage keeps the orders as plain JSON text, so anyone with access to the browser can read and change it. It is not secure. My page shows names with textContent, so a name like `<b>Test</b>` appears as plain text.

If the code used innerHTML, an attacker could type HTML or script code as the name, and the browser would run it as real code on the page. This attack is called XSS (cross-site scripting). textContent prevents it.

## Specificity experiment (Lab4, Task 4, Step 4.8)

When I added #main p { color: red; }, the white paragraph in the hero turned red even though .hero p came earlier in the file. An id selector (1,0,1) beats a class plus an element (0,1,1), so specificity decides the winner, not the order in the file.

## Selectors I used (Lab 4, Task 4, Step 4.9)
| Selector kind | Example from my CSS |
|---------------|---------------------|
| Element | body |
| Class | .hero |
| ID | #main |
| Grouping (comma) | h1, h2, h3 |
| Descendant (space) | .nav-list a |
| Child (>) | main > section |
| Adjacent sibling (+) | h1 + p |
| Compound (no space, such as a.active) | .nav-list a.active |
| Attribute | a[href^="http"] |
| Pseudo-class | a:hover |
| Pseudo-element | .menu-group h2::before |

## Bug log (Lab 4, Task 6)

| # | What was wrong (file and line) | Which tool showed it | My fix and why |
|---|--------------------------------|----------------------|----------------|
| 1 | bugs.html line 7: link pointed to style.css, but the file is bugs.css | Network tab (red 404 row) | Changed href to bugs.css. The names must match exactly, or no CSS loads. |
| 2 | bugs.html line 2: html tag had no lang | Lighthouse and W3C validator | Changed it to html lang="en". Screen readers use it to pronounce words correctly. |
| 3 | bugs.html line 17: heading jumped from h1 to h4 | Accessibility tree and Lighthouse | Changed h4 to h2. Headings should go in order so the page makes sense to screen reader users. |
| 4 | bugs.html line 10: menu was a div, so no navigation landmark | Accessibility tree | Changed div to nav with aria-label="Main". Screen reader users jump between landmarks, and a div is not one. |
| 5 | bugs.html line 18: img had no alt text | Lighthouse and W3C validator | Added alt="Campus Café logo: a coffee cup with steam". Blind users need it to know what the image shows. |
| 6 | bugs.html line 21: label for="mail" did not match input id="email" | Lighthouse and label click test | Changed it to for="email". Now clicking the label puts the cursor in the field. |
| 7 | bugs.css line 14: property was spelled colour | Styles pane (crossed-out line) | Changed it to color. CSS only knows the American spelling, so the button text was not white. |
| 8 | bugs.css line 21: .btn:hover had no semicolon after #0b1f3a | Styles pane (invalid value) | Added the semicolon. Without it, the hover color and pointer cursor both failed. |
| 9 | bugs.css line 25: selector was .notes, but the HTML class is note | Styles pane (no rule on the paragraph) | Changed .notes to .note. The names must match exactly, so the rule never applied before. |
| 10 | bugs.css line 27: grey text #999999 on white was too light | Lighthouse (contrast audit, only after fixing bug 9) | Changed it to #666666. Darker text is easier to read. It stayed hidden until bug 9 was fixed because the rule never applied. |