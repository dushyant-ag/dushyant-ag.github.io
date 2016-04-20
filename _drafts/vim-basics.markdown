---
layout: post
title:  "Vim Basics"
date:   2016-02-03 10:18:00
comments: true
desc: "Basic Vim commands to get started on Ruby on Rails"
keywords: vim basics, vim commands, vim with rails
categories: vim vi
---

Best thing about VIM is that is made by programmers for programmers and it is very much programmer friendly. I am gonna show you how in next couple of minutes.

Install VIM (Vi IMproved)

sudo apt-get install vim (on Ubuntu)

Now, start by Vimtutor (it gets installed with the installation of VIM)

It will show you a page for playing with VIm.

Now, we have a general tendency to move up/down/left/right using arrows, where we have to leave out our comfort zone of typing i.e. "Home row" (i.e. ASDF JKL;). Vim comes here to rescue. 
using VIM we can move up/down/left/right using K/J/H/L respectively. Isn't it amazing ? Its a habit worth developing from beginning. 

You would be happy to know that there are lot of applications have adopted this including Gmail, Trello etc. 
https://vimium.github.io/
https://support.google.com/mail/answer/6594?hl=en
https://trello.com/shortcuts


2. The 'x' command

'x' the simple it looks, prettier it do the job. This is used to delete the character under the cursor. 
Need ? Ever wondered when we are writing long paragraphs and there are typos, we quickly skim through hjkl and use x to delete unwanted characters. You will realize how fast it is when you are actually doing it. 

3. Help command

What if you get stuck somewhere in between ?? 
Not a problem with VIM, simple get to normal mode (ESC key) and type :help or :h and VIM will load all the commands with details, you do not have to look at the whole documentation. Instead you can search the command using :help/:h command_name/function/etc . Vim has really really good help searching system. 

Infact there is another great thing called Vim Wiki (where you get all the answers/best practises related to VIm). http://vim.wikia.com/wiki/Vim_Tips_Wiki 

4. the 'a' and 'i' command

So for inserting we have to type 'i' and for appending 'a' 

5. Save/Cancel

So far we have learned basic commands, its time to save/cancel all the changes we have done. 

:q! to trash the changes and exit the editor 
:wq to save and exit the editor


6. the 'dw' command

You know, where the real power lies, when you perform extraordinary tasks with just a 2 character command. Yes, that is right. 
the 'dw' command lets you delete the word. 
How to do that? Just place your cursor to the first character of the word to be deleted and type 'dw'. That is it! Awesome, isn't it ?

7. the 'd$' command

Well 'dw' is not the only wonder VIm has, infact it has lot of other commands to help you achieve what you want in few characters, one of them is 'd$'. What it does is- it lets you delete till the end of line from where the cursor currently is. 
Place your cursor to the point where you want to delete and press 'd$' and Voila! 

In the last two commands 'ds' and 'd$', you might notice that delete is somewhere related to character 'd'. Yes you got this right! Infact in VIM, many commands that change text are made from an operator and a motion, where 'd' is our operator for delete and 'w' '$' are motions which represents how_much and from_where to_where. 

We have learned about 'dw' and 'd$'. Lets add one more commands to our glossary i.e. 'de'- it delete to end of current word, including last character.

A short list of motions:
    w - until the start of the next word, EXCLUDING its first character.
    e - to the end of the current word, INCLUDING the last character.
    $ - to the end of the line, INCLUDING the last character.


Now comes the best part: We have learned about 'operators' and 'motions'. Now what if you just provide motions without operators ? Any guesses ? It helps you move to the cursor to that position without doing the work of operator (like delete in case of 'd'). ;-) You can thank VIM later. 

There is lot more you can do with motions: You can even provide numbers before motions to multiply their work. 
ex: 2w will take you two words forward, 3w, 4e etc. '0' would get you at start of line. 

Whats more ? You can club operators with motions and numerals for fast and multi processing. 
ex '2dw' will get you delete two words from where the cursor currently sets in. 

8. the 'dd' command
Due to the frequency of line deletions, we can get it done simply by issuing 'dd' command, which will delete whole line for us. 
Further you can provide numerals to multiply its effect. Like '2dd' would delete current and next line. 

9. the undo and redo command

So far we have learned how to add/edit/delete the text, but what if we accidentally did something and we want to revert it back ? Here comes the rescue operator UNDO. 
How to: Just press 'u' and it will undo the last command, whereas 'U' would return the current line to its original state i.e. reverting back all the changes. 

Now comes the work of Redo (CTRL + R), which can also be understood as undoing undo. 

Lets say you made couple of changes in a line. For example:

Original line: Wee are herree to leaarnn some bassics of Vim.
Edited line (5 edits): We are here to learn some basics of Vim.

Now issuing 'u' would revert last change i.e. We are here to learn some bassics of Vim.
However issuing 'U' would revert all changes to this line i.e. Wee are herree to leaarnn some bassics of Vim.

Now let say I want to revert all the changes but first one. 
Long way would be issuing repeated 'u' commands
Short way would be issuing 'U' and then CTRL R 
Shortest would be '4u' (numerals and operators ;-) )



10. the 'p' command

this p command appends the last delete text. 
Sometimes we need something needs to be cut from somewhere and appended somewhere. (sorry of all these somes :P)

For ex: You have this para

1. this is first line.
3. this is third line.
2. this is second line. 

Now to order them correctly, what you can do is- 
go to last line, issue 'dd' this will delete "this is second line", now go to "this is third line" and press 'p'. Voila! Its that simple!

11. the 'rx' command

this is to replace the character with x (the x in rx)

ex: this line is typed wromg.
Now you go the character which is typed wrong i.e. m in wromg. press 'r' to replace and 'n' to replace with. So the command would be 'rn'

12. the 'ce' command

In previous command we learned how to replace a single character, in this we will see how 'ce' helps us replace the entir word. Cool! Insn't it ?

In 'ce', 'c' is for change and 'e' is motion to get us to the desired location. So 'ce' will erase the text from current cursor location to the end of word and takes you in insert mode to type the correct text. 

ex: This is exemlple text.
Now go to e in exemlple and type 'ce' plus the required text i.e. ample (ex ample) and it will append that to the current word. Press ESC to return to normal mode. 


Further you can use motions with 'c' command like $, e, w etc and numerals too. Yes yes, Vim is fascination I know, there is lot more coming. 


13. Delete multiple lines 

Use Visual mode, type 'V', then move up/down to highlight the block you want to delete and then remove it with 'x' or 'd'. 


14. 'v' command

It select the current character. Where as 'V' select the current line.

15. the 'y' command 

this is yank command, which copies the selected text. 


16. '<' and '>' 

select the text and indent using '<' and '>'.


17. CTRL + o

It lets you enter one command while being in Insert mode.