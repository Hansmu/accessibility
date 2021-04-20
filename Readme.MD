# Accessibility

https://developers.google.com/web/fundamentals/accessibility

### Semantic HTML
https://developer.mozilla.org/en-US/docs/Glossary/Semantics#semantics_in_html

One of the most important ways of achieving accessibility is using semantic HTML.
That means that you should use the appropriate elements for the content that you'd
like to display. So a button is a button, not a div with all sorts of other interesting
properties.

With headings - they should appear in the order that you expect. So starts off with
H1, which is then followed by H2 and so on. A lot of people make the mistake of using
header elements for styling. For example, they want something to be bigger inside
of a paragraph tag, but this causes problems in relations to accessibility. Some
people with screen readers navigate using headers. So if a header is in the middle
of a paragraph, then there'd be a problem.

Another misused element is an anchor. It's often used to replace a button. When you
remove the href tag from the anchor element, then it's as if it's nothing, just
a div. If you add an icon into an anchor element, then the screen reader would
not even announce it, or it might announce something strange.

If you truly have to use an anchor in that kind of context, then give it a role
attribute. E.g. `role="button"`. This will make the anchor behave like a button.
The role tag lets you describe unsemantic elements as semantic elements. Another
tag that you'll need is `tabindex="0"`, which makes the element focusable.

Styling forms is cool and all, but if you remove form elements and use divs instead
for styling, then you're using a lot of accessibility options, as you won't be
able to control and navigate the form as you would in a properly defined form.

### Color accessibility
Colorblind people cannot see certain colors. A lot of designers design their pages 
in grayscale, because if it looks good in grayscale, then it'll look good for
colorblind people. The colors need to be kept in high contrast between the text
and its background, because that'll ensure that colorblind people will be able
to read them regardless of their colorblindness. What's more, do not rely solely
on color to transfer meaning, because colorblindness means that all colors will 
not be picked up by the users. E.g. if you have an error, don't just rely on the red
color, but add a warning icon or something like that. One of the worst examples
would be to have color swatches on a website without accompanying color texts.
Perhaps a colorblind person is making a purchase for someone else and they won't
be able to tell what color they are picking.

Field errors should also have an accompanying icon, instead of simply having the
red color, because in grayscale, you'll have a difficult time distinguishing between
regular labels and the errors.

In regards to color contrast, run your colors through a color contrast checker to make
sure that the text would be readable on a specific background. Sometimes when
enlarging the font of a text, then it'll be made accessible. A contrast checker
can note if that is a possibility.

https://webaim.org/resources/contrastchecker/

A good idea is to first design the page in grayscale. Then check if all of the page
interactions are obvious. After that is certain, then you can start adding color.
Color should be used only as a secondary pointer of importance, not the primary.