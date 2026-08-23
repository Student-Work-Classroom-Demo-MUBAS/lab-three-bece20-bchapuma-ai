# Lab 3 — Error Log
**Student Name:** Ben Chapuma
**Student ID:** BECE/20/SS/003
**Date:** 08/23/2026
**Lab Session:** 1:30AM - 3:00AM

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

