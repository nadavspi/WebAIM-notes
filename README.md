# Why we do it
## Affects people
8.5% of US population has a disability that affects computer use (including
cognitive/learning disabilities, color blindness, etc.) 
- 2000 US Census

## Market share
For some people with disabilities, the web is where they do all of their
commerce: they can't do it in person. Whoever creates accessible options wins.
E.g., big shift to iPhone once it became accessible.

## Search engine benefits
Making things more machine-readable for AT also helps search engine agents.
Google is blind and deaf and can't use a mouse.

---

Providing adequate accessibility makes disability transparent. E.g., people
with vision issues don't consider themselves disabled once they have glasses.
Their experience of the world isn't different. Imagine if some websites didn't
work with contacts or glasses.

---

# WCAG

## Principles
- Perceivable (content can be perceived)
- Operable (users can interact with it)
- Understandable
- Robust (technology compatibility - AT)

## Levels of conformance
- A: without this, experience will be hindered.
- AA: without this, experience will be more difficult.
- AAA: additional enhancements that go beyond what's necessary. Very few
websites are fully AAA compliant.

## Accessibility vs. compliance
Some technically compliant experiences can still be inaccessible (and provide poor UX). E.g., having to hit tab
hunderds of times to pass a big flyout menu. Some things affect all users
(e.g., tiny text) rather than just disabled users, and as such aren't covered
by WCAG. If it's bad for everyone, then it's not discrimination.

# Disabilities
## Auditory
1. Provide captions for video & live audio.
2. Provide descriptive text transcripts for audio content. If you can't hear
   the audio, you get all of the same information from the transcript: identify
   speaker, include sound effects, include visual-only information.

## Low vision
Vision that can't be adequately corrected using glasses. Blurry, obscured visual
field, difficulty in perceiving contrast, things might move/flutter.

Chrome extension: NoCoffee Vision Simulator. Not for testing, but for getting
a feel for different visual experiences.

1. Support enlarged/magnified content. People typically use magnification software such as ZoomText. In
  WebAIM survey: one third zoomed 200%, another third 400%.
  (One reason for not embedding text in images.)
2. Provide sufficient color contrast. WCAG doesn't cover gradients, borders,
   drop shadows, text over images, hover/focus/visited states etc. In some cases, colors that pass WCAG
   contrast are still hard to read. Use common sense.

## Color blindness
8% of men in US, 2% of women. Red & green deficiencies are most common.

1. Don't rely on color alone. WCAG says you can't rely on color (or any single "sensory characteristic" - e.g., just bold) as the *only* way to convey something.

### Requirements for non-underlined links
1. 3:1 contrast ratio between link text and non-link text. 
2. Link must present a "non-color designator" (e.g., underline) on mouse hover
   AND keyboard focus. 

We now have three contrast requirements: text/background, link/background, text/link.
Users that disable colors won't see links at all. 

Best to use underline or other visual designator to avoid that and color contrast complications.

## Blindness

For screen readers, semantic markup is key. Most/many screen reader users have some
vision and may use a screen reader and a screen magnifier at the same time.
Some have full vision.

### Semantics

Not just for screen reader users; semantic markup improves usability for all
users.

#### Headings

In WebAIM surveys, 65% of screen reader users navigate using headings. Majority
use heading levels too. Looking at headings alone should basically show a table of contents for the page.
WCAG doesn't require proper heading structure until AAA, but it's very important.

One of the top things to do to improve accessibility.

Guidelines:

1. Usually one `<h1>` per page as the document title.
2. Don't skip heading levels (e.g., `<h2>` to `<h4>`). Skipping backwards is
   fine (`<h4>` to `<h2>`).
3. Headings should never be empty.

It's OK to style headings visually to maintain semantics within the design (`<h2 class="h4">`).

#### Forms

- Use labels for inputs, text areas, select menus, checkboxes, radio buttons.
- Never use `<label`> for anything else - it'll be ignored by screen readers.
- Explicit labeling (`<label for="thing"><input id="thing" />`) is a little more robust
than implicit labeling (`<label><input /></label>`).

##### Hidden labels

- A visually hidden label is OK.
- If there's no `<label>`, `title` on the input is interpreted as the label by
  screen readers. Equivalent to a visually hidden label but adds the tooltip
  for mouse users. `<input title="Search Terms" type="search" />`
- A screen reader will treat `<label>`, `title`, and `aria-label` identically.

##### Placeholder

- Can be used for advisory information.
- Do not use placeholder as the only mechanism for labeling a control. Most screen readers tend to read it if there isn't a label, but you shouldn't rely on it.
- Low contrast. Increasing the contrast can make it look like a value instead
  of a placeholder.
- Disappears once filled in. Can be a problem for validation, e.g., "MM/YY" as
  placeholder, "Enter a valid expiration date" in validation.

##### Other form issues

- Avoid JavaScript "jump" menus (select menus that go to a different page on
  change).
- Avoid `multiple` select menus. Usability issues and mostly inaccessible to
  keyboard users.
- Be very careful with `autofocus`.
- Be very careful with "Reset" buttons. (You probably don't need it.)
- `<input type="image">` must have alternative text.
- You'll never be able to re-create all of the accessibility of a `<select>`.

##### Limitations with `<label>`

1:1 relationship between `<label>` and a form control.
- <label> can't apply to more than one control.
- Control can't have more than one <label>.

See: [`aria-labelledby`](#aria-labelledby).


#### Tables

1. Caption: if there is one, it should be a `<caption>`.
2. Use `<th>` table headers.
3. Specify scope for table headers (`<th scope="row">`).
4. Avoid empty `<th>`. If you have an empty heading cell in the corner, make it
   a `<td>`.
5. `<thead>`, `<tfoot>`, and `<tbody>` have no accessibility impact. Screen
   readers will follow the document order.
6. Don't use table `summary` (dropped in HTML 5).

#### Alternative text

- Read by screen readers and search engines.
- Alternative to images when images are disabled or not supported.
- Provides semantic meaning and description to images. 
- Difficult because it's so subjective.

Equivalent alternative text provides the content and/or function of an image,
very rarely a description of the image. Probably `<img alt="John Smith">` rather than
`<img alt="Tall man with brown hair">`.

Ask yourself: if you couldn't use a picture, what text would you put in its
place?

Alternative text can be presented in:
1. The `alt` attribute of `<img>`.
2. The context or surroundings of the image itself (e.g., a caption).

Alternative text should:
1. Be accurate and equivalent. Usually any text in the image should be
represented in the alt text.
2. Be succint. In most cases, a few words should be sufficient. If it's
   multiple sentences, there's probably a better of way of presenting the
   content.
3. Not be redundant.
4. Not use the phrases "image of ..." or "graphic of ..." to describe the
   image.

 Use empty `alt` tag to indicate that:
 1. The image is decorative and doesn't convey content or,
 2. The content of the image is declared elsewhere.

 For complex images (charts and graphs):
 1. Provide alternative in context or a link to a longer description.
 2. Main image should still have some alt text ("Pie chart representing...").

### Meaningful link text

Make links descriptive when possible. "Learn more" requires a screen reader
user to work harder to understand the context.

"Click here" is probably a sign of poor visual design (it doesn't look like
a link) or poor link text (it should just say "Login").

#### Page title (`<title>`)

- Often the first thing read by a screen reader.
- Should be succint and descriptive.
- Should usually match or be similar to the `<h1>`.

#### iframe 

- Screen readers read iframes seamlessly as if they were a part of the page.
- Optionally identify content and functionality with a `title`: `<iframe src="http://youtube.com/abc" title="Intro to Web Accessibility video">`.
- If you look at the page and can't visually tell that the iframe is distinct,
  you probably don't need a title. Despite what some tools say, `title` is not
  *required* for iframes.

## Cognitive/learning disabilities

The largest disability group - larger than all the others put together - but so varied that it's hard to make general recommendations.

- Be careful with movement and other distractions.
- Use good organization (headings, lists, etc.)
- Focus on important content.
- Simplify.
- Avoid really small text.
- Avoid long line lengths.
- Be consistent.

## Photosensitive epilepsy

Be careful with flashing/strobing content.

Risk of causing a seizure:
- 3 times per second or greater
- Size, brightness, and red threshold

Rule of thumb: if it's annoying, probably don't do it.

## Motor disabilities

- Difficulty with fine motor control and use of a mouse.
- Repetition and fatigue.
- Control over timing or moving elements.
- Various ATs that simulate keyboard or mouse, or voice control.

### Links

- Meaningful link text helps with voice control (e.g., 17 "Learn More" links
  aren't helpful).
- Ensure click targets are large enough
- Make sure clickable items look clickable and vice versa.
- Underline should typically be reserved for links. 
- If you have to refer to the hover state to know whether something is clickable, it's probably not clear enough.
- Provide enough space between clickable items.

### Keyboard navigation

- There many users that use the keyboard for navigation, few that use *only* the
keyboard for navigation.
- Most screen readers will primarily use the keyboard to navigate. 
- Don't ignore keyboard navigation for small viewports; many users use external keyboards on their phones.
- On Mac, enable Full Keyboard Access -> All controls in keyboard settings.
- [Flying Focus](https://github.com/NV/flying-focus): JavaScript for adding
transitions between focus states. Also available as a Chrome extension (useful
for testing).

#### Links
- Don't remove keyboard focus indicator (`outline`) from links. (WCAG AA
  requirement. Treat it as an A requirement because it works by default and is so important.)
- You can enhance/style the default focus indicators. Non-underlined links must
  become underlined on hover and focus.
- You can usually apply the same styles to :hover and :focus.

#### Skip links

A link to "skip to main content" from the beginning of the document.

- Primarily benefit sighted keyboard users (because screen reader users have many
other ways of navigating).
- A bit of a hack, but recommended until browsers allow navigation by
  headings/landmarks.
- It's fine to visually hide it to avoid disrupting design/usability for users that
  don't need it. (Don't use `display: none` though - that's hidden from screen
  reader and keyboard users altogether.)
- Should be visually distinctive to make it apparent (think of a low vision
  user with motor disabilities)

#### Standard keystrokes

- Tab/shift-tab to navigate links, form control, etc.
- Link: enter
- Button: enter or spacebar
- Checkbox: spacebar
- Radio buttons: up/down or left/right arrows
- Select menu: up down, letters, spacebar to expand
- Tree/application menu: up/down, left/right to expand/collapse
- Tabs: hit `tab` once to enter the group of tabs, up/down or left/right to select individual
  tabs

#### Accesskey

`<a href="search" accesskey="s">`

Don't do it.

- Activation of accesskey varies by browser.
- There is no standard set of keys.
- Difficult to avoid conflicts with UA shortcuts (browser add-ons, screen
  readers, etc.)

### Timed activities

- If a time constraint (e.g., session timeout) is necessary, make sure the
  users have enough time.
- Make sure the users knows what the time constraints are.
- Maybe prompt the user before time is up and allow them to extend.

# Strategy / principles

Think about an entire process or workflow. If you signal that the purchase
workflow is accessible but the last submit button is inaccessible, that's
probably worse than no accessibility from the start (like having an accessible traffic signal
but no curved sidewalk on the other side).

A separate accessible or text-only version of the site is probably a bad idea.
- Might be considered discrimination: "separate", "unequal", "untimely".
- More overhead in maintaning two sites, risk of them getting out of sync.
- In WebAIM surveys, most users don't use separate accessible or text-only
  versions, assuming they'll be out of date.
- Thinking about accessibility & semantic markup for your website improves the
  experience for everyone.

# Odds & ends

- Whether or not your site should work without JavaScript is more of a usability
question than an accessibility question. In WebAIM surveys, 98%+ of users had
JavaScript enabled, which is the same as the general population.
- Remember that we are web experts and our experience of the web is very
  different than our users's experience (especially on things that we built).
- Many users with disabilities have multiple disabilities.

## Acronyms & abbreviations

- Expand unknown acronyms/abbreviations at first instance. E.g., "Per the Web
  Content Accessibility Guidelines (WCAG)..."
- Don't worry about pronunciation for screen readers or try to modify it for
  them (e.g., N.A.S.A. instead of NASA). It varies by screen reader, user settings, etc. Screen reader users
  become accustomed to idiosyncratic pronunciations.
- Optionally use `<abbr>` on one instance if you want. Probably only accessible for mouse 
  users. (But if your abbrevation requires explanation, it might make sense to
  define it in text.)

## Fonts

- Font size units (px, em, rem, etc.) don't have an accessibility impact.
- Web fonts are fine.
- Choose good, legible fonts.
- Be careful with ALL CAPS. Use `text-transform`. (Most screen readers don't
  distinguish ALL CAPS and `text-transform` now, but hopefully in the future.)

## Language

For the page: `<html lang="en">`
For a page part in a different language: `<div lang="fr">`

- Very important for screen reader users that are set up to read in multiple languages. 
- If you have a language switcher, make sure to mark up the language link for
  that language. `<a lang="ja">日本語</a>`

## Visually hiding content

- `display: none` and `visibility: hidden` hide from everyone.
- Avoid 0 pixels, setting same color as background, etc. Behavior is
  inconsistent.
- Use off-screen absolute positioning or `clip` with CSS for screen readers.
- Use judiciously. Typically just use for brief cues or indicators that are
  useful for screen reader users. E.g., "You are here:" before breadcrumbs.
- Make sure to keep visually hidden content up to date.
- Visually hidden content is indexed by Google.

## Title attribute

- Use for advisory information only. Not essential (in which case put it in the content) or
  rendundant.
- Often ignored by screen readers except for:
  1. Form elements that don't have labels
  2. iframes
  3. `<abbr>` depending on SR settings.
- Not accessible to keyboard users, touch screen users, etc.

## CSS generated content (::before, ::after)

May or may not be read by screen readers. Assume the worst.

# ARIA (Accessible Rich Internet Applications)

A specification that allows enhancements to accessibility.

- Foundational rule of ARIA: if you can do it with HTML (rather than ARIA), you
  must.

## `aria-label`
`aria-label` can be used instead of (and will override) content. E.g., `<a
aria-label="Facebook"><span class="icon-facebook" aria-hidden="true"></span></a>`.

## `aria-labelledby`

`aria-labelledby` can be used to link multiple inputs to one label and vice
versa.
`<input aria-labelledby="cyndi officenum"`> for Cyndi's office number.
Any element can be the target for `aria-labelledby`. E.g., use an input to
label another:

```html
<input id="name">
<span id="phone">Phone number</span>
<input aria-labelledby="name phone">
```

If `name`'s value is Cindy, the second input should be read "Cindy phone
number, edit".
