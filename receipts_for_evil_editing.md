# Introduction
While the documentation of [evil-surround](https://github.com/emacs-evil/evil-surround) is reasonably clear after one studies it and much implicitly assumped understanding of vi, etc.,
it's hard for the uninitiated to figure out the assumptions of the details.

Here are bite-size operational receipts that one can follow to achieve the desired outcome, without guessing or digging the assumped knowledeg.
I hope that it helps a hurry user of evil-surround with the receipts to execute text edits quickly and go back to what he's focusing.

# How to change enclosing brackets?

Based on [Change surrounding](https://github.com/emacs-evil/evil-surround#change-surrounding), here is the steps:
In the following instruction, '|' indicates the position of the editing cursor.
Supposed one wants to change '[' and ']' to '{' and '}' in "[ "some text"]"
1. Put the cursor _inside_ the brackets to be changed, for example, [| "some text"] for changing '[' and ']'
2. Change the mode to be normal
3. press key cs
4. press '[' (the one be changed)
5. press '{' (to change to)




