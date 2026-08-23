# Lab 3 — Error Log
**Student Name:** Ben Chapuma
**Student ID:** BECE/20/SS/003
**Date:** 08/23/2026
**Lab Session:** 1:30AM - 4:00AM

## Testing out CSS rules

**Rules being tested:**
​```css
.intro{
    color: blue;
}

#hero{
    color: red;
}
​```

**Element with conflicting rules:**
```html
<p class="intro" id="hero">Paragraph with BOTH</p>
```
**Prediction:** 
The #hero rule is going to win. Elements without conflicting rules will take their specified colors.

**Reasoning:**
- This rule represents an id.
- An 'id' is more specific than a class, so the 'id' wins by rules of specificity.
- The 'p' element will adopt the color 'red'.

**Actual result:**
- The first paragraph has black text
- The second has blue
- The third has red
- The fourth also has red

**Correct?**
Yes

**Notes:**
The fourth paragraph adopted the color 'red' which was specified by the 'id' rule
since it is more specific that the 'class' rule.

**Screenshot location:** 
images/textcolor.png


## Error 1
**Task I was working on:** Task 1
**What I was trying to do:**
I was trying to push my local changes to the remote repository
**The exact error or problem I saw:**
An error telling me that I was trying to merge and push my changes before pulling the current state of remote main.
It also refused to merge the two unrelated histories. Check '/images/merge_error.png'
**Steps I took to fix it:**
1.Added allow unrelated histories command
2.Run the prompt again
3.The changes were succesfully pulled from remote and it was time to try and commit the local changes to the remote repository
4.Logged the error first
**What I learned from this:**
It is always good to perform a git pull first before trying to push local changes to main - avoids merge issues!

---
## Session Reflection
**The concept I found hardest to understand today:**
**The moment it clicked (if it did):**