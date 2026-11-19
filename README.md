# CISP360 Final Project — Student GPA Tracker

A console-based student GPA roster written in C++ for CISP360.
Records persist to a plain-text file between runs.

## Purpose

Keeping track of a class roster by hand is tedious: names and grades live in a
notebook or a spreadsheet, re-sorting means rewriting the list, and finding one
student means scanning every row.

This program replaces that with a small menu-driven tool. It holds a roster of
students and their GPAs, and it **remembers the roster after you close it** —
you type a student in once, and they're still there next time the program runs.
From the menu you can look at the whole roster, add someone new, sort everyone
from highest GPA to lowest, look a single student up by name, swap two students'
positions, or remove someone who has left the class.

It's built for up to 50 students and uses no databases or outside libraries —
just the C++ standard library and one text file sitting next to the program.

## How it works in simple terms

**The roster is two lists that stay lined up.** One list holds names, the other
holds GPAs. The first name goes with the first GPA, the second with the second,
and so on. A separate counter remembers how many students are actually in the
roster, so the program never reads empty slots. Because the two lists are
matched up by position, every operation has to move a name and its GPA
together — that's the rule the whole program is built around.

**Startup — the roster is read back in.** Before the menu ever appears, the
program opens `students.txt` and reads the saved students into memory. If the
file doesn't exist yet (the very first run), it just starts with an empty
roster instead of complaining.

**The menu repeats until you quit.** You get a numbered list of options and type
a number. If you type something that isn't a number, the program throws the bad
input away and asks again rather than crashing or looping forever. Your choice
is matched against the menu and the matching task runs; then the menu comes
back, ready for the next thing.

**Each option is its own small job:**

- *View* walks the roster from the first student to the last and prints each
  name with its GPA in neat columns.
- *Add* asks for a name and a GPA and puts them in the next free slot, then
  bumps the counter up by one. If the roster is already full at 50, it says so
  instead.
- *Sort* compares students against each other and reorders them from the
  highest GPA down to the lowest, carrying each name along with its GPA.
- *Search* asks for a name and checks the roster one student at a time until it
  finds a match, then prints that student's GPA — or reports that nobody by
  that name is on the roster.
- *Swap* asks for two names, finds where each one sits, and trades their
  positions, GPAs included.
- *Remove* asks for a name, finds that student, and slides everyone after them
  one position forward to close the gap, then drops the counter by one.

**Quitting saves your work.** Choosing *Save and Exit* writes the whole roster
back out to `students.txt`, overwriting the old copy, so the next run picks up
exactly where you left off. Nothing is written to disk until then, which means
the saved file always holds a complete roster rather than a half-finished one.

## Features

| # | Menu option | Status |
|---|-------------|--------|
| 1 | View students | not yet implemented |
| 2 | Add student | not yet implemented |
| 3 | Sort roster by GPA | not yet implemented |
| 4 | Search student by name | not yet implemented |
| 5 | Swap two students | done |
| 6 | Remove student | done |
| 7 | Save and exit | done |

Load/save to `students.txt` is written but still needs fixes before it compiles.

## Build and run

```bash
g++ -std=c++17 -Wall -Wextra -o gpa_tracker Main.cpp
./gpa_tracker
```

## Data format

`students.txt` stores one record per two lines:

```
Student Name
3.75
```

## Project structure

```
Main.cpp      all program logic (menu + functions)
students.txt  roster data, created on first save (not tracked in git)
```

## Notes

- Roster capacity is capped at `MAX_STUDENT` (50).
- Names and GPAs are held in two parallel arrays and accessed through pointers.
- Functions that change the roster size take the counter by reference so the
  change is visible back in `main`.
