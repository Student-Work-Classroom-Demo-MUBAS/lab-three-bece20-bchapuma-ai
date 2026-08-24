# Reflection

## 7. box-sizing: border-box

Adding `box-sizing: border-box` at the top of a CSS file is best practice because it makes the numbers written match the numbers actually seen on screen.

**(a) With `border-box`:** The rendered width stays exactly 200px. This is because border-box tells the browser that the width I declared already includes the padding and border. So the browser squeezes the content area down to make room for the 20px of padding on each side, and the total box still ends up being 200px wide. Nothing grows past what I declared.

**(b) Without `border-box` (the default, content-box):** The rendered width becomes 240px. This is because in the default box model, width only describes the content area, and padding gets added on top of that. So the math is 200px content + 20px left padding + 20px right padding = 240px total rendered width.

## 8. Removing position: relative from the card

If I remove `position: relative` from `.card`, the badge would no longer be positioned relative to the card. Instead, .badge (which still has position: absolute) would look further up the DOM tree for the next ancestor that has a position value other than static. If nothing else in the page has positioning set, it would eventually reach the `<html>` element (the initial containing block), and the badge would jump to the top-right corner of the entire page instead of the top-right corner of the card.

This happens because `position: absolute` doesn't care about where an element sits in the normal HTML flow — it only cares about the nearest positioned ancestor (any ancestor with position: relative, absolute, fixed, or sticky). Since `.card` was the only thing standing between the badge and the page root, removing that position: relative breaks the "anchor" and the badge escapes the card entirely.

## 9. The Cascade and specificity

Given these three rules:
```css
h2 { color: red; }
.title { color: blue; }
h2.title { color: green; }
```
and the element `<h2 class="title">`, the text would render **green**.

This is because of CSS specificity, which is a point system the browser uses to decide which rule wins when more than one rule matches the same element. Specificity is usually written as a tuple of (ID selectors, class selectors, element selectors):

- `h2` is a single element selector → specificity = (0, 0, 1)
- `.title` is a single class selector → specificity = (0, 1, 0)
- `h2.title` combines one element selector and one class selector → specificity = (0, 1, 1)

Comparing them: (0,1,1) beats (0,1,0), and (0,1,0) beats (0,0,1). So `h2.title` has the highest specificity of the three rules, and its declaration (`color: green`) wins, regardless of the order the rules were written in.

## 10. CSS position values in real websites and apps

- **static:** This is the default position for basically every element, including something as ordinary as a paragraph of body text on a Wikipedia article. It just sits in the normal document flow, top to bottom, left to right, with no special offset behaviour. Most of any webpage is `static` — it's the "do nothing special" position.

- **relative:** On Instagram's post layout, the small "..." (more options) icon in the corner of a post is nudged slightly from where it would normally sit using `position: relative`, without pulling it out of the flow or affecting the elements around it. It's also commonly used just as an anchor, like on a product card on Amazon, where the card itself is `position: relative` purely so a "Best Seller" badge inside it can be positioned absolutely against that card instead of the whole page.

- **absolute:** The notification count bubble on a messaging app icon (like the red circle with a number on WhatsApp's app icon, or the notification dot on a bell icon in Gmail's web interface) is a good example — it's pulled out of the normal flow and pinned to a specific corner of its parent icon, regardless of how much text or content surrounds it.

- **fixed:** The navigation bar at the top of YouTube (with the logo, search bar, and account icon) stays fixed to the top of the browser window even as I scroll down through a long list of video results. It never scrolls away because it's removed from the page's normal flow and pinned relative to the browser viewport itself.

- **sticky:** On Gmail, the row of category tabs (Primary, Social, Promotions) scrolls normally with the page until it reaches the top of the window, and then it "sticks" there while I keep scrolling through my inbox below it. That's the hybrid behaviour of `sticky` — it acts like `relative` until a scroll threshold is hit, then switches to acting like `fixed`.