---
{"dg-publish":true,"permalink":"/prep-notes/2022-07-25-monday-class-instructions/","dgHomeLink":true,"dgPassFrontmatter":false}
---



## July 25th

## PREP

### KITTY BLOCK

<div class="blocks">

```
1. First we are going to creat a game loop. 
then we can replay the game at the end. 

To do that we will divide this main game stack into two stacks. 

first find this block:
When green flag clicked
broadcast [initialize v] and wait
and AFTER IT PUT THIS BLOCK:
broadcast [Game Loop v]

Then we make a new stack, which will be the game loop. 
This is where we restart the game from. 
Add this block:
when I receive [Game Loop v]
And move all 5 of these blocks, 
{**they are from the green flag above**} 
onto the  {when I receive \[Game Loop v\] } 
broadcast [add music v]
broadcast [choose difficulty v] and wait
wait until <(DIFFICULTY) > [0]>
broadcast [Countdown v] and wait
broadcast [Start v] and wait
Then we are going to add two blocks on the end...
1. The first will make a landing effect, and replay if you tell it to
broadcast [Landed v] and wait
2. Then, if you don't replay,
this block will make the game really over:
broadcast [Game Over v]


Now go to the updraft sprite and follow the next set of directions

```

### UPDRAFT block


```
1. After this block:
clear graphic effects
we are going to insert some blocks here. 
First, we delete any clones that might be left over 
from the last time the game was played. 
Add this: {note there is NOTHING in the not block}
if <not <>> then
    delete this clone
end
Then we make the updraft go to the front:
go to [front v] layer
at some random position: 
go to [random position v]
When it is there, create a clone. This "shadow-clone" is the updraft's shadow.
create clone of [myself v]
Keep this block that was there before:
show
We also want the updraft to move around the screen, 
so add this onto the show block:
broadcast [move updraft v] 

Why a broadcast, instead of just putting the code here?
Because then it will act on both 
the updraft AND the clone at the same time. 
This stack is only working on the mother 
{because we deleted the leftover clones at the top...}


2. Before we do the code to move the updraft and its shadow,
let's make the shadow clone look right.  
To control the shadow-clone one of these blocks: 
when I start as a clone
We want the clones to look like shadows, so we do a couple of things:
1. put the clone behind the mother updraft
go [backward v] (1) layers
2. Make it black like a shadow:
set [brightness v] effect to (-100)::looks
3. but add a little transparency:
set [ghost v] effect to (75)::looks
we offset it a little bit, so it looks like a shadow
change x by (2)
change y by (-2)
and then finally, we make sure it is showing:
show


Now, at last we can make the updraft and its shadow move. 
Remember this stack is working on both of them, 
so they will always both move together.
First we create the partner to the broadcast above, that is the receive block:
when I receive [move updraft v]
We want to keep them moving up until either:
a) they they the top OR
b) the round is over
repeat until <<(y position) > [186]> or <(ROUND OVER) = [1]>>
You might have to adjust the "186" depending on the size of your updraft. Inside this loop:
We move up:
    change y by (.5)
If they are touching the kitty
    if <touching [KItty v]?> then
we make them fade out :
        broadcast [fade out updraft v]
And then we are done with this round, so we stop the code.
        stop [this script v]
The {repeat loop} ends
    end

The {when I receive} loop ends
end
Lastly, we hide the updraft. This may not be necessary here...
hide


This is the stack that does the fadeout:
when I receive [fade out updraft v]
repeat (10)
    change [ghost v] effect by (10)::looks
    wait (0) seconds
end
hide
delete this clone


```

</div>


