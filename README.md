# filter-subtitles
Filter `.srt` files to remove SDH (Deaf or Hard-of-Hearing) entries and other tags.

## Installation
```
pip install filter-subtitles
```

## Usage
`filter-subtitles` can be used either as a script or a module.

By default, this module filters the following (in order):

1. Removes font tags e.g. `<font color="#DF01D7">(GUN COCKS)\</font>`.
2. Removes Subtitle entries containing asterisks: `*`.
3. Removes Music tags `♪` and text contained within two music tags.
4. Removes Sound effects: text contained with and including parenthesis `(BANG)` and brackets `[boom]`.
5. Replaces capitalized names with dashes, e.g. `GARY: Hey` to `- Hey`.
6. Removes author tags such as `XoXo Subtitles by PwnedDude967 XoXo`.

### Script Usage
Bring up the help display:
```bash
filter-subtitles.py -h
```

Filter a subtitle in place (overwrites original subtitle) with default options.
```bash
filter-subtitles.py -s /path/to/sub.srt
```

Instead of saving to disk, print the output.
```bash
filter-subtitles.py -s /path/to/sub.srt -p
```

Save the output to a different filepath.
```bash
filter-subtitles.py -s /path/to/sub.srt -p -o /path/to/outsub.srt
```

Custom filter flags.
```
--keep-fonts          Do not remove font tags from subtitles.
--keep-ast            Do not remove subtitles containing asterisks: (*).
--keep-music          Do not remove "♪" symbols and text contained within
                        two "♪" symbols.
--keep-effects        Do not remove text between and including parenthesis
                        () or brackets []
--keep-names          Do not replace names in CAPITALS with "-" tags
--keep-author         Do not remove author tags, eg. Subtitles by some guy.
```

### Module Usage
Filter a subtitle in place (overw.rites original subtitle) with default options
```python
from subtitle_filter.lib.subtitle import Subtitles

subs = Subtitles('/path/to/sub.srt')
subs.filter()
subs.save()
```
Instead of saving to disk, print the output.
```python
subs.print()
```
Save the output to a different filepath.
```python
subs.save('/path/to/newsub.srt')
```

Use custom filter flags.
```python
subs.filter(
    rm_fonts=True,
    rm_ast=False,
    rm_music=True,
    rm_effects=True,
    rm_names=False,
    rm_author=False,
)
```