# freefonts
Free fonts hosted for convenience.

These are fonts that I bundle in software, so I include only fonts that have licenses that allow that with no restrictions.

I like to store them in the source tree along with notes about where I got them from along with licenses and attribution. This repo stores them along with that info, so that all I have to do is copy them out of this source tree into whichever project is using them.

I like to use pyftsubset (pip install fonttolls; https://fonttools.readthedocs.io/en/latest/subset/index.html) to reduce the size of fonts when packaging them for distribution. This lets you get rid of extra font layout features you're not using, and if you're really aggressive you can get rid of most of the glyphs in the font as well, especially if your application doesn't allow the user to enter text.

Below I summarize what I remember and have pieced together from the docs about how to subset files. I haven't done it in a while and I haven't tested these examples, so there might be mistakes.

For example, something like this will discard all features and all glyphs above 0xFF (thus keeping more or less the Latin-1 character set):

    pyftsubset source_font.ttf --output-file=shrunken_font.ttf --unicodes="20-7E,A1-FF" --layout-features='' --name-IDs=''

You can also put the Unicode glyphs list in a file and then do this:

    pyftsubset source_font.ttf --output-file=shrunken_font.ttf --unicodes-file=/path/to/unicodes/file --layout-features='' --name-IDs=''

I've been using SDL_ttf for fonts, which doesn't have a lot of features so much of what's in a font file will probably be useless anyway. If you wanted to use FreeType (https://freetype.org/) then it could probably do more. In particular, FreType supports WOFF and WOFF2 fonts, which would probably be useful if you're trying to keep font size down.

Documentation on what font features mean:

https://developer.apple.com/fonts/TrueType-Reference-Manual/RM06/Chap6.html
https://docs.microsoft.com/en-us/typography/opentype/spec/featuretags

