# CISP360 Final Project — Student GPA Tracker

A console-based student GPA roster written in C++ for CISP360.
Records persist to a plain-text file between runs.

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
