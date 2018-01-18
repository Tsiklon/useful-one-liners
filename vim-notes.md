# vim notes
## Replacing Text
- Replace Foo with Bar on one line -   ``` :s/Foo/Bar/g ```
- Replace Foo with Bar on all lines - ``` :%s/Foo/Bar/g ```
- Replace Foo with Bar on one line with  confirmation - ``` :s/Foo/Bar/gc ```
- Replace Foo with Bar on all lines with confirmation - ``` :%s/Foo/Bar/gc ```
- Replace Foo with Bar on All lines between 5 and 12 - ``` :5,12s/Foo/Bar/g ```

## Searching
- Search Forward for foo - ``` /foo```
- Search Backwards for foo - ``` ?foo ```

## General Text Editing
- Yank Line - ``` y_ \| yy \| dd P ```
- Cut line - ``` dd ```
- paste yanked/cut text - ``` p ```
- cut all text from cursor to mark a - ``` d`a ``` - "Cut, Return to Mark A, complete"
- cut an entire paragraph of text - ``` {d} ``` - "Move to Paragraph beginning, Cut to end of paragraph"
- yank all text from cursor to mark a - ``` y`a ``` - "Yank, Return to Mark A, complete"
- yank all text in an entire paragraph - ``` {y} ``` - "Move to Paragraph Beginning, yank, to end of Paragraph"
- cut all text from cursor to the next instance foo - ``` d/foo ```
- cut all text from cursor to the next previous foo - ``` d?foo ```
- yank all text from cursor to the next instance foo - ``` y/foo ```
- yank all text from cursor to the next previous foo - ``` y?foo ```
- delete/cut all lines matching foo - ``` :g/foo/d ```
- Join line below to this line - ``` J ```

## Visually Marking Text
- Visual select - ``` v ```
- Line Select - ``` V ```
- Block Select - ``` ctrl+v ``` 

## Marking
- Mark point - ``` ma ```   ( or any other letter a-z)
- Return to Mark a - ``` `a ```
- Return to beginning of Line with Mark a - ``` 'a ```

## Moving around
- Move to bottom of the page - ``` G ```
- Move to the top of the page - ``` gg ``` 
- Move to line - ``` :[num] ```
- Move to Beginning of Paragraph - ``` { ```
- Move to End of Paragraph - ``` } ```
- Move down half a page - ``` ctrl+d ``` 
- Move up half a page - ``` ctrl+u ```

## Quality of Life
- Clear search highlighting - ``` :noh ```
- New Tab - ``` :tabe ```
- Next Tab - ``` gt ```
- previous Tab - ``` gT ```
- split window - ``` :vsp ```
- move between windows - ``` ctrl+ww ```
