---
layout: post
title: "Why I hate Kindle's exports"
subtitle: "A medium-length rant with no conclusion."
date_started: 2022-02-05
first_published: 2022-02-08
date_modified:
  - 2022-02-06
  - 2022-02-07
  - 2022-02-09
---

<section>
Let me preface this by saying that the [Kindle][Amazon Kindle] is actually a nice device
and the [mobile app][Kindle for Android] is also a very good e-reader^[The reader will likely point out that
that's a low bar to clear for a trillion dollar company.
To that I say, touché.]
but the note exports have ranged from mildly unpleasant to the downright maddening.
Why, you ask?
Let's take a moment to build up some background.

Whenever one makes a highlight and adds a note, or to put it succinctly, annotates text,
the relationship between the note and the highlight is of as much importance as the note and highlight itself.
This parent child relationship gives important context to a note when reviewing it later,
separate from the book itself.
Take the example of a word highlight that you may want to add to your vocabulary:

![Example of highlighting an unfamiliar word](/images/kindle-exports/kindle-word-highlight.png)

If you were to, say, convert this into a flashcard,
the relationship is of utmost importance.
What good would this note do to you without its corresponding highlight?

Let us take the case of an amusing anecdote as an annotation.
Separate from the highlight, the note is merely a fragment of memory,
a blossoming flower split off from the stem that anchors it to the world,
slowly withering away.
Upon the next visit, it is nigh impossible to breathe in the aroma that was once familiar to us.^[Do pardon the overly, _ahem_, flowery language.
I promise that this pun wasn't the original intention.]

Without this semantic information,
it is somewhat painful to decipher which note belongs to which highlight.
Why re-engage with the text to piece together the complete meaning of what you, the reader, wrote earlier?
Surely, that's absurd?
The only reason to do so would be if you were forced to do so.

You'd normally expect that the notes have a sort of nested structure. We could perhaps demonstrate this with a bit of markdown

```markdown
> This text is highlighted
  * And this is a comment
  * This is another comment under the same highlight
* This is a standalone note
> Standalone highlight
```

Let us remove the semantic information.

```markdown
> This text is highlighted
* And this is a comment
* This is another comment under the same highlight
* This is a standalone note
> Standalone highlight
```

Voilá!
Satan has arrived!
I present to you, Kindle's exports.
Who knows what parent the third comment belongs to?
How do we even figure out if it's a standalone note?
Without additional semantic information, this is indeed impossible to parse correctly.
However, the Kindle exports give us just enough to think we _may_ have a chance.
Let us look an actual Kindle export this time.

```html
<div class="noteHeading">
Highlight (<span class="highlight_pink">pink</span>) - PREFACE TO THE CHARLES DICKENS EDITION >  Location 103
</div>
<div class="noteText">
But, like many fond parents, I have in my heart of hearts a favourite child. And his name is DAVID COPPERFIELD.
</div>
<div class="noteHeading">
Note - PREFACE TO THE CHARLES DICKENS EDITION >  Location 103
</div>
<div class="noteText">
This is a note that is actually part of the highlight.
</div>
<div class="noteHeading">
Note - PREFACE TO THE CHARLES DICKENS EDITION >  Location 115
</div>
<div class="noteText">
This is note is outside the highlight and is actually standalone.
</div>
```

The astute reader may conjure up a few ideas to parse the notes correctly.
They are:

- Set an arbitrary count of notes belonging to a highlight.

	This works if your behavior is consistent as you're essentially offloading the parsing logic onto the user instead.
	This is typically a bad idea but perhaps exposing it as a parameter might help.
	It won't be 100% accurate but it will indeed have a reasonable degree of accuracy.
	Manually fixing the errors may turn out to be difficult depending on your output template.
	
- Use the `Location` information from the `noteHeading` div 
  and calculate where it ends using the highlight length.

	If you thought of this, I tip my hat to you.
	Unfortunately, the location doesn't seem to be calculated by any known rules
	and seems to be entirely arbitrary.
	If you do know, feel free to [reach out](/contact-me.html).
	Meanwhile, I've actually hardcoded a location difference
	and plan to expose this as a parameter.
	This works reasonably well and has more accuracy than the former.

- Ask the user to add this information manually.
  Possibly present a GUI to "arrange" highlights.
	
	No.

Here's where things get spicier.
The location seems to be exported only if we use custom books.
In our example, we're using the [Project Gutenberg edition of _David Copperfield_][Project Gutenberg - David Copperfield].

Books purchased from the Kindle store export page numbers instead.

```html
</div>
<div class="noteHeading">
Highlight (<span class="highlight_pink">pink</span>) -  Page 1
</div>
<div class="noteText">
His Last Bow An Epilogue of Sherlock Holmes
</div>
<div class="noteHeading">
Note -  Page 1
</div>
<div class="noteText">
This is a sample note.
</div>
<div class="noteHeading">
Note -  Page 1
</div>
<div class="noteText">
Another note.
</div>
<div class="noteHeading">
Note -  Page 1
</div>
<div class="noteText">
Note highlighting the full title
</div>
```

Let's take a look at what the highlight is actually like.

![Kindle Highlights for _His Last Bow_](/images/kindle-exports/kindle-mobile-example.png)

If you're familiar with notes on the Kindle app,
you'll note that when creating a note in tandem with a highlight,
it'll usually be at the very end of the highlight.
In our case, the heading has three notes:

- the first is "This is a sample note."
- the second is "Another note."
- the third and actual highlight tied to the note is "Note highlighting the full title"

Let's also use a markdown like representation for looking at our HTML to compare.
We'll use [Pandoc markdown][Pandoc markdown] to look at the divs:

```md
::: noteHeading
Highlight ([pink]{.highlight_pink}) - Page 1
:::

::: noteText
His Last Bow An Epilogue of Sherlock Holmes
:::

::: noteHeading
Note - Page 1
:::

::: noteText
This is a sample note.
:::

::: noteHeading
Note - Page 1
:::

::: noteText
Another note.
:::

::: noteHeading
Note - Page 1
:::

::: noteText
Note highlighting the full title
:::
```

There is legitimately no way at all to extract the correct structure,
especially once you note that the internal storage is incorrect as well.

![Kindle Highlights Notebook](/images/kindle-exports/kindle-app-internal.png)

We may as well just give up at this point.
I know I have.

</section>

[Amazon Kindle]: https://en.wikipedia.org/wiki/Amazon_Kindle
[Kindle for Android]: https://play.google.com/store/apps/details?id=com.amazon.kindle
[Project Gutenberg - David Copperfield]: https://www.gutenberg.org/files/766/766-h/766-h.htm
[Pandoc markdown]: https://pandoc.org/MANUAL.html
