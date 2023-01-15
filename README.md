# Amanda Hanway - Streaming Data, Module 2


# streaming-02-multiple-processes

> Multiple processes accessing a shared resource concurrently

## Oveview

This example starts up a shared database and three different processes.

The processes represent multiple users, or locations, or programs 
hitting a shared database at the same time. 

## Prerequisite

Complete the setup at [streaming-01-getting-started](https://github.com/denisecase/streaming-01-getting-started).

## About

Execute about.py to generate some useful information.

## First Run

Executing multiple_processes.py script.

Read the output. Read the code. 
Try to figure out what's going on. 

1. What libraries did we import?
    sqlite3, time, multiprocessing, os, datetime, platform, sys
2. Where do we set the task_duration?
    line 34
3. How many functions are defined? 
    7
4. What are the function names? 
    create_table, drop_table, insert_pet, process_one, process_two, process_three, recreate_database
5. In general, what does each function do? 
    create_table: creates a database connection, then a sql table called pets
    drop_table: drops pets if it exists
    insert_pet: inserts the name and breed into pets
    process_one: inserts Ace and Buddy
    process_two: inserts Cooper and Rabbit
    process_three: inserts Emma and Felix
    recreate_database: drops pets, creates pets, and prints a message 
6. Where does the execution begin?
    line 132
7. How many processes do we start?
    3
8. How many records does each process insert?
    2 

In this first run, we start 3 processes, 
each inserting 2 records into a shared database 
(for a total of 6 records inserted.)

In each case, the process gets a connection to the database, 
and a cursor to execute SQL statements.
They insert a record, and get out of the database quickly.

In general, we're successful and six new records get inserted. 

## Second Run

For the second run, modify the task_duration to make each task take 3 seconds. Run it again. 
With the longer tasks, we now get into trouble - 
one process will have the database open and be working on it - 
then when another process tries to do the same, it can't and 
we end up with an error. 

## Document Results After Each Run

To clear the terminal, in the terminal window, type clear and hit enter or return. 

`clear` 
- Note: this did not work for me. A google search suggested using 'reset', also did not work. I just closed the terminal after each run.

To document results, clear the terminal, run the script, and paste all of the terminal contents into the output file.

Use out0.txt to document the first run. 

Use out3.txt to document the second run.

## Select All, Copy, Paste

On Windows the select all, copy, paste hotkeys are:

- CTRL a 
- CTRL c 
- CTRL v 

On a Mac the select all, copy, paste hotkeys are:

- Command a
- Command c
- Command v

Detailed copy/paste instructions (as needed)

1. To use these keys to transfer your output into a file, 
clear the terminal, run the script, then click in the terminal to make it active.
1. To select all terminal content, hold CTRL and the 'a' key together. 
1. To copy the selected content, hold CTRL and the 'c' key together. 
1. To paste, open the destination file (e.g. out0.py) for editing.
1. Click somewhere in the destination file to make it the active window.
1. Now hit CTRL a (both together) to select all of the destination file.
1. Hit CTRL v (both together) to paste the content from your clipboard.

Do a web search to find helpful videos on anything that seems confusing. 

## Reading Error Messages

Python has pretty helpful error messages. 
When you get an error, read them carefully. 

- What error do you get?  'database is locked'
- Can you tell what line it was executing when it failed?  line 106, in process_two
    insert_pet("P2", "Cooper", "Rabbit")


## Database Is Locked Error

Do a web search on the sqlite3 'database is locked' error.

- What do you learn?
   - This error code occurs when you try to do two incompatible things with a database at the same time from the same database connection. 
    For example, if you are in the middle of a SELECT statement and you try to DROP one of the tables being read by the SELECT, you will 
    get an SQLITE_LOCKED error. (https://www2.sqlite.org/cvstrac/wiki?p=DatabaseIsLocked)
- Once a process fails, it crashes the main process and everything stops. 

## Deadlock

Deadlock is a special kind of locking issue where a proces 
is waiting on a resource or process, that is waiting also. 

Rather than crashing, a system in deadlock may wait indefinitely, 
with no process able to move forward and make progress.

## Learn More

Check out Wikipedia's article on deadlock and other sources to learn how to prevent and avoid locking issues in concurrent processes. 

https://en.wikipedia.org/wiki/Deadlock 
- Handling Deadlock:
    - Ignoring
    - Detection
    - Prevention
    - Avoidance
