---
layout: post
title: Moon+ Reader
subtitle: "The definitive Android e-reader?"
date_started: 2022-02-03
first_published: 2022-02-05
date_modified:
  - 2022-02-03
  - 2022-02-04
---

<section>

I'm always on the lookout for a good e-reading app.
I primarily read on Android and I've used the Kindle for Android app in the past.
My current favorite is [Moon+ Reader][Moon+ Reader].
Let's walk through why and how I use it.

</section>

## Reader View & My Setup

Apart from supporting a wide variety of formats^[EPUB, MOBI, AZW, CHM, you name it.],
the reading interface is very customizable.
The options are too many to list
but there is enough flexibility built in to be on par with the best.
My go to changes for a pleasant reading interface are pretty close to the Kindle app's defaults, to be honest.

<figure>
<center>
  ![My Moon+ Reader theme](/images/moon-reader/Screenshot_20220203-173154.png)
</center>
</figure>

I use [Bookerly][Bookerly], since I seem to love nice thick serifs on a mobile screen.^[I'm also quite partial to [Source Serif Pro][Source Serif Pro].]
Light grey text feels more comfortable than white
since I often read close to bedtime.
My background is a solid black.^[This is quite nice on an OLED screen,
I might add.]
You can save this as a theme in case you want to switch quickly between different visual settings.
I also keep the status information to a bare minimum;
remaining time in the chapter
along with the overall time remaining in the book are all I need.
I also quite enjoy the page curl animation, which is set to Apple Books style.^[I don't know why it's called so.
The Kindle app has a nigh identical animation.]
An odd thing, I know, but I find it quite pleasurable.[^page-flip-video]
I also use a generous margin on the sides that may be off putting to some
and quite dislike hyphenation of text on such a small screen,
which is why it's only left aligned and not justified.

[^page-flip-video]:
  {-} ![Page Flip Animation on Moon+ Reader](/images/moon-reader/screen-20220205-182421~2.mp4)

## Annotations

The beauty of Moon+ Reader lies in the elegance of its annotation interface.
For converts from the Kindle app like myself,
the touch and drag of text creates a highlight.
This can then be modified to the correct color/annotation type.^[I'm looking for a more precise word/phrase that encompasses
highlights, underlines, strikethroughs, etc.
but this will have to do for now, it seems.]
Color choices are quite flexible as well.
In fact, it allows defining custom colors across the RGB spectrum with adjustable alpha values,
giving one a theoretical ceiling of 16^8^ colours.^[`#FFFFFFFF`-`#00000000` is the allowed range.]
Of course, you'd probably want to stick to a trusty few that you're accustomed to.

<figure>
<center>
![Highlight Interface](/images/moon-reader/Screenshot_20220204-150027.png)
</center>
</figure>

In my case, it's blue for anecdotes or disagreements with the author,
yellow for new words I want to add to my vocabulary,
orange for references to other texts or potential avenues of research I want to chase down,
red for particularly good quotes that I want to use in the future,
and gray for something I want to convert to a flashcard.
You'll notice that these are the same colors
that we have on the Kindle app, except gray.

Now, this may seem overly elaborate
but just because the option exists doesn't mean you're forced to use it.
I've simply found this to be optimal for my reading flow.
I should also point out that underlines, strike throughs, and other annotations
are also supported and that the interface is rather seamless.

It allows for overlapping highlights, so I can put a yellow one inside a red highlight.
Annotation is also more precise compared to Kindle's annotation interface
as the em dash (—)^[[Some reading][Em Dash] in case you've forgotten what those are.]
no longer sticks automatically to the previous word.
There is also a high precision mode where you can first highlight a word
and then drag the selection handles across to highlight a specific piece of text
that you found tricky or to create the aforementioned nested highlights.
This can also be triggered by using the "Text Selection" option under the More sub menu.

<figure>
<center>
![Yellow highlight nested in red](/images/moon-reader/Screenshot_20220204-150121.png)
</center>
</figure>

## Exports

Another important feature that I use is the note export.
Sometimes, I want to chase down some references
and other times, I want to make flashcards.
Therefore, getting these notes and highlights out of Moon+ Reader
and into plain text to use with my notes system is of utmost importance.^[I'm aware that Moon+ Reader can hook into [Readwise][Readwise]
but I'd rather not pay to extract my own annotations from my own books, 
caveats about content ownership and DRM aside.
I completely understand the value that other users derive from it, however,
and I may change my mind in the future as well.
Meanwhile, my objective is to hijack the Readwise API call from the app.]
I use the share button on the bookmarks page and export to a file.
I do this often and I'd like to automate this if possible.

### Aside: How I Use Exports

Moon+ Reader exports annotations from a book in `.mrexpt` format.
Moon+ Reader's export schema is decent to work with and has only a few minor annoyances,
chief of them being sparse^[Read: non-existent.] documentation.
This export goes to my note taking app of choice, [Obsidian][Obsidian],
and is parsed by some JavaScript.^[To be specific,
the parsing is done inside a script that runs inside a JS environment from a plugin named Templater,
but that's a bit much to get into right now.
JavaScript is also weirdly fun.
[Here's][Moon Reader Templater Script] a link to my script.]
The script extracts only the gray highlights
so that I can add flashcards to my queue.^[Here,
I diverge from philosophy of using the right tool for the job.
Instead of using [Anki][Anki], [Mnemosyne][Mnemosyne] or [Mochi][Mochi],
I keep my cards in Obsidian while they're still "in development".
I plan to export them to Anki when I feel they're "stable"
but I haven't quite reached that point yet.]

This lets me keep in touch with a book's core ideas
and reinforce my understanding as I'm going through it,
provided I revisit my flashcards as I'm reading through the book.
It does take extra effort
but if it pays dividends by providing better long term understanding and retention,
it is quite worthwhile.^[See: Michael Nielsen's [essay on long-term memory][Augmenting Long-term Memory].]

## Miscellaneous

Moon+ Reader also handles footnotes quite well.
You get a nice yellow pop-up, similar to a note, that can be scrolled through.
Often, you can also jump to the footnotes location
and later jump back to your original reading position.
Like other features, the footnote color, popup styles, etc. can also be customized.

Reading positions can also be synced over Google Cloud, WebDAV, and Dropbox
and you might find this useful if you have an Android tablet, for example.^[I actually wish
there was a standard way to sync reading positions which are not tied (coupled) to the app.]
You can back your books and highlights up to those sources as well.
It has features to pull books from several online libraries
such as [Overdrive][Overdrive]
, [Project Gutenberg], [Open Library],
and it can also download covers for your books.
Reading time tracking is good but not as granular as I'd like.^[It's actually quite good.
I'm just overly demanding and like having chapter wise statistics.
I get around this by using bookmarks and then later parsing bookmark positions.
Quite obtuse, I'm aware.]

Integrated dictionaries are available but not as seamless as Kindle,
where the dictionary is in-app.
Instead, it opens up a separate app depending on what you've configured.
It also doesn't seem to properly interface with an on device dictionary such as Merriam Webster.
If you try to share to it, it doesn't receive the input
and most dictionary apps appear to contain ads anyway.
I get around this by passing the selected text to a web search query in my browser,
which more often than not does the trick.^[This is my setting,
for the curious: `http://www.merriam-webster.com/dictionary/%s`.
The `%s` is replaced by the selected text, which redirects me to the correct page.]

<figure>
<center>
![My dictionary tweak](/images/moon-reader/screen-20220204-153111~2.mp4)
</center>
</figure>

As an aside, I've disabled ads by using custom DNS
and I ensure my data is private by blocking it off from the internet using [Netguard][Netguard].
With my privacy taken care of,
I can read comfortably without any apprehension of my data being collected.^["Wait, if you're privacy conscious, why do you use the Play Store?"
Yes, I'm aware of the fallacy here.
Privacy is on a spectrum and I haven't had the time to get into custom ROMs
or extensive de-googling.
I do use [F-Droid][F-Droid] though,
and there isn't an equivalent for Moon+ Reader that suits my needs.
Please don't spam my inbox with "But, muh [Calibre Web][Calibre Web]! Self hosted web readers!"
You know who you are. \rant]
This was the main reason for switching away from the Kindle app,
if I may indulge myself here for a little bit.

## Criticisms

The dictionary is definitely a weak point.
An in-app copy of the Oxford Dictionary would go a long way.
I suspect there may be licensing issues or something of the sort that get in the way.
I also don't think it can open a different file while reading.^[This isn't directly possible in the Kindle app either, to be fair, but that's how it behaves.
You should also be able to select the dictionary
when using the search bar in the Kindle app,
as further evidence of it being a separate book.]

I've also had some issues with vertical scrolling.
With page turn animations enabled,
tapping any area outside a small-ish central region results in the app turning pages.
It seems to work perfectly fine if page turn animations are disabled, however,
using the full width of the screen for scrolling.
It's been a mildly annoying problem so far but hasn't stopped me from reading.
Maybe I should just disable animations at some point if it grates me further.
Most books I read on the Kindle app didn't have page turn animations enabled anyway.

I've also noticed that PDF annotation exports are garbage.
Can't be a wizard at everything, I suppose.

## Final Thoughts

There are plenty of wonderful features,
many of which I haven't even touched on^[A few good shoutouts would be
auto-scrolling, day-night switching, and overriding book styles with custom CSS.],
and it is truly astounding that we get so much for free.
In my opinion, Moon+ Reader is easily the best and maybe only e-reading app
that fits my pattern of usage.
I suspect it to be so for many others as well.
As a closing note, if you feel there are better alternatives
something that I haven't touched on that's worth a mention,
or anything else even, feel free to [message me](/contact-me.html)!

[Moon+ Reader]: http://moondownload.com/
[Source Serif Pro]: https://fonts.adobe.com/fonts/source-serif
[Bookerly]: https://en.wikipedia.org/wiki/Bookerly
[Augmenting Long-Term Memory]: http://augmentingcognition.com/ltm.html
[Em Dash]: https://www.thepunctuationguide.com/em-dash.html
[Readwise]: https://readwise.io/
[Obsidian]: https://obsidian.md
[Anki]: https://apps.ankiweb.net/
[Mnemosyne]: https://mnemosyne-proj.org/
[Mochi]: https://mochi.cards/
[Overdrive]: https://www.overdrive.com/
[Open Library]: https://openlibrary.org/
[Project Gutenberg]: https://www.gutenberg.org/
[Netguard]: https://netguard.me/
[Calibre Web]: https://github.com/janeczku/calibre-web
[F-Droid]: https://f-droid.org/
[Moon Reader Templater Script]: https://gist.github.com/AB1908/3d9ff5a328ce7749411dcb8e72d81283
