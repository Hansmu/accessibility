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

### ARIA
A set of attributes that make the HTML elements more accessible. Makes them more
understandable to screen readers. The basic syntax is `aria-*`, where `*` defines
a specific property. 

`aria-expanded="false"` to define whether a sidebar is open or not.

An example of `aria-label` would be adding a descriptive label to a link with an icon.
So social media links at the like. If you have `aria-label` on an interactive
element, then `aria-label` is prioritized over the text of that element. E.g.
`<button aria-label="Shop now">Shop</button>` results in "Shop now" from the
screenreader, instead of "Shop now, Shop".

`aria-labelledby` to avoid copy pasting text. If there's a paragraph text that describes the image, that's 
usually visible, then in order to avoid copy pasting that text into an image `alt`
property, then you could instead use `aria-labelledby` to refer to the ID of the 
paragraph text and the screenreaders would understand that the image is described
by that paragraph tag.

`role` doesn't have an aria prefix, but it's used to describe an element if it
isn't doing what it's semantically supposed to. So a div that acts as a button.
Remember to always add a `tabindex="0"` if you're defining such an element, so
that it could be focused with the tab.

### Accessible images
If you don't have an `alt` attribute on your image, then the screenreader is going
to read the filename of the image, so the entire URL. If you have a background
image described via CSS background, then it doesn't matter, the screenreader
will skip it, but if it's an image tag, then it won't. There's no point in adding
"Image of ..." or something like that into alt, because then the screenreader will
say something like "image Image of...". If you have multiple sentences in an alt, then
use punctuation marks. However, if you have a caption for the image, then it's 
best to keep the `alt` as empty, so that it wouldn't read the image src and then
have an `aria-labelledby` pointing to the caption.

One common mistake that people make is describing what is on an image, when it 
actually has a functional feature. E.g. a company image that leads you back to
the homepage. So in case you have a link with an image inside it, you'd say
in the alt property `Homepage` or something like that, instead of `Company logo`.

### Outline
When you focus an element, then you get an outline. A lot of pages disable it
because of some idea of visuals. However, this is a huge blow to accessibility.
Without the outline, you wouldn't know what you have selected when using a tab to 
focus. Browsers have a different outline. It's suggested that you have a custom
outline, because the default outline can be very thin, based on the browser, so
it can be barely visible. So two things to keep in mind when defining the outline
for your application - have the outline thick enough to notice and have it use
a color that is the complete opposite your usual color. So if your webpage is red,
go with a green outline. Maximize contrast.

```
*:focus: {
    outline: 4px solid lime;
}
```

Button elements often have their outline disabled by a component library. The
best idea when dealing with buttons is to add the same styles to focus as you have
with hover. Generally hovering darkens a button or something like that, so make
sure that the visual feedback style is also triggered on focus, so that the user
could understand what is focused without having an outline. However, if it is
very subtle, then you'd probably want to still add an outline.

### Tabindex
Tabindex allows the user to use their keyboard to focus an element. Interactable
elements can a tab index by default. However, if you're adding custom elements
and want them to be focusable, then add a `tabindex="0"` property to it. If you
have `display: none` or the `hidden` attribute, then tabindex is removed, so the
user wouldn't focus on a hidden element. If you define `tabindex="-1"`, then 
the user won't be able to focus the element using a tab. However, you'd still
be able to focus the element using Javascript. Add a `tabindex="-1"` to default
interactive elements is a bad idea, though, and that means that you probably
want to use a different component for what you are doing. The value that you set
to tabindex is the priority they get when tabbing. However, this can make interactions
really confusing, if you're using values other than 0 and -1. The user would be
jumping back and forth in an order they might not be expecting. So when using
things tabbable, just use 0 or -1.


### Bypass blocks
If someone comes to your page and wants to make an appointment and the make
an appointment link is at the very bottom, then the user has to tab through
the entire page to get to the appointment block. When you press tab, then
a link appears that allows you to skip to the main content of the page. They're
generally at the top of the page, but if you have a lot of repeated content, then
you can add them in the middle as well. Skip links only appear when you're
using the site. An example of a skip link would be if you have a filter and the
user wants to avoid tabbing through that to get to the desired content, so you
can add a skip link to the top of the filter.

In order to add a skip link you can add an element with an anchor element inside
it that references another element on the site by ID. So the HTML of the skip link
looks like
```
.skip-link {
    transform: translateY(-100%);
}

.skip-link:focus {
    transform: translateY(0%);
}

<a class="skip-link" href="#content">Skip to main content</a>
```
where #content is the ID of the main content area. Initial style is there to 
hide the content. When it gets focused, then bring it back into view.

### Accessible video and audio
Good idea to provide captions and transcripts for audio/video as it'll help
disabled people, but also allows indexing by search engines. Closed and open
captions are used. Closed are the ones you can toggle on/off, so you'll get
the ability to give multiple language supports. Open means that they are baked
into the video, and you cannot remove them without editing the video. If you have
closed captions, then it might be a good idea to include it in the video description
as well so people'd know to search for it. E.g. `The Biscuit Killer [Closed Captions]`.

Quality captions include:
* Correct grammar & punctuation
* All on-screen text. E.g. if the speaker is showing text and doesn't describe it.
* Audio description. E.g. `monitor beeping erratically`
* Placing the captions so that they don't block anything important

Audio description is a voice clip that describes what is happening in the video.
If you cannot provide it, then make sure that the transcript and/or the captions 
are descriptive.

Same for presentations. When giving one, try to accurately describe the charts 
and what not instead of just saying something like "According to the chart, the
profits have doubled". Explain exactly the numbers.

```
My rule of thumb is, anytime I am lecturing and I am tempted to say the 
words "as you can see" means I must change the way I say it.
```

Additional note - using carousels are bad. Should avoid them altogether on your
website.

When choosing a media playback software for accessibility, then keep in mind to check
that they support:

* Displaying captions
* Button for audio descriptions
* Full screen option
* Keyboard accessible
* As Cross Browser Compatible as possible (toss it if it doesn't run on the most popular browsers)
* Support for interactive transcript

```
Captions, transcript, audio description, non-seizure/migraine inducing 
content, keyboard functions, accessible player - it all ties together to 
create an incredible experience for abled and disabled users.
```