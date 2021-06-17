# The problem
With magit enabled in .doom.d/init.el and having been use magit by SPC g g for successfully for a long time, 
suddenly SPC g g no longer work with error message of "SPC g g is undefined".

# Attempetd receipt to fix

The fix can be using a different .doom.d configurations.

Re-install the Doom/Emacs with doom sync executed
but still got the same error

ls -lt .emacs.d/.local/straight/repos/ | grep magit 
yields nothing.

ls -lt .emacs.d/.local/straight/build-27.1 | grep magit
yields nothing.

# Other attempted fix

- doom sync
- doom upgrade
- doom build

Debugging with running 
emacs --init-debug 
did not show any clue.



