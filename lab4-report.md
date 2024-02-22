# Lab 4 - Vim
---
Steps (4 - 9): 
- Log into ieng6
- Clone your fork of the repository from your Github account (using the SSH URL)
- Run the tests, demonstrating that they fail
- Edit the code file to fix the failing test
- Run the tests, demonstrating that they now succeed
- Commit and push the resulting change to your Github account (you can pick any commit message!)


## Log into ieng6
[screenshot here]
`ssh ket003@ieng6.ucsd.edu <enter>`
summarize the commands you ran and what the effect of those keypresses were.

## Clone your fork of the repository from you Github account (using the SSH URL)
[screenshot of obtaining SSH link]
Obtain the Github SSH link
`git clone git@github.com:7seraph/lab7.git <enter>`
summarize the commands you ran and what the effect of those keypresses were.
[screenshot after cloning]

[screenshot of cd into lab7]
`cd la <tab> <enter>`
summarize the commands you ran and what the effect of those keypresses were.

## Run the tests
[screenshot of failed tests]
`bash test.sh <enter>`
summarize the commands you ran and what the effect of those keypresses were.

## Edit the code file to fix the failing test
[screenshot of going into vim]
`vim ListE <tab> .java <enter>`
summarize the commands you ran and what the effect of those keypresses were.
Begin keystrokes `:$ <enter> j j j j j j l l l l x i 2 <esc> :wq! <enter>`
summarize the commands you ran and what the effect of those keypresses were.
[screenshot of fixed code]

## Run the test, demonstrating that they now succeed
[screenshot of tests passed]
`bash test.sh <enter>`
summarize the commands you ran and what the effect of those keypresses were.

## Commit and push the resulting change to your Github account
[screenshot of successful commit]
`git commit -m "fixed index1 to index2" <enter>`
summarize the commands you ran and what the effect of those keypresses were.
`git push`
summarize the commands you ran and what the effect of those keypresses were.
[screenshot of successful push]
