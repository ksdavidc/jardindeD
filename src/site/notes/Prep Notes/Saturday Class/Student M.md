---
{"dg-publish":true,"permalink":"/prep-notes/saturday-class/student-m/","dgHomeLink":true,"dgPassFrontmatter":false}
---


# Student M

## 2022 08 13

### Sword

<div class="blocks">


>  Add broadcast and waits for:
> * initialize 
> * get initialize values
> * show initial game screen
> * start game


```
when @greenFlag clicked
broadcast [initialize v] and wait
broadcast [get initial values v] and wait
broadcast [show initial game screen v] and wait
broadcast [start game v] and wait
```


> create a new draw routine
> This replaces the old one because
> Using if mouse down is better than if not mouse down
> also, make it draw only on left part of screen

```
when I receive [start game v]
set pen size to (10)
forever
    if <(CURRENT BUTTON) = [1]> then
        if <<mouse down?> and <(mouse x) < [120]>> then
            go to [mouse-pointer v]
            pen down
            repeat until <not <<mouse down?> and <(mouse x) < [120]>>>
                go to [mouse-pointer v]
            end
            pen up
        end
    end
end
```
2.create show variable and hide variables:



Set the starting value of the variables when the game starts. Do this in the in the receive initialize stack.

CURRENT BUTTON is which button we are using.
DRAWN is how much of the screen we have drawn on.

The screen is covered by 4 sections. Each of these takes up a certain amount of the screen.

QUAD FULL are how much of the screen each section uses by itself. 
QUAD is how much of that QUAD is covered by drawing.


### Sword

```
when I receive [initialize v]
hide variable [CURRENT BUTTON v]
set [CURRENT BUTTON v] to [0]
set [DRAWN v] to [0]
set [QUAD1 v] to [0]
set [QUAD1 FULL v] to [0]
set [QUAD2 v] to [0]
set [QUAD2 FULL v] to [0]
set [QUAD3 v] to [0]
set [QUAD3 FULL v] to [0]
set [QUAD4 v] to [0]
set [QUAD4 FULL v] to [0]
set [RESULT v] to [0]
```

Go to the costume editor and move the sword so the point of the sword is at the very center of the sprite.
This will 
 
 fix pen routine:
 when drawing goes to mouse, puts pen down, and keeps drawing until mouse is not longer down.
 
 change color detected to 000FF
 
 note that it is different than the color of the numbers
 
 
 
 Create variable CURRENT BUTTON. 
 When I click button set the variable. Make it only draw on CURRENT BUTTON = 1
 
 create new sprite TESTER and copy all costumes from backdrop to this sprite in same order and with same names
 
 create check current values stack and text coverage of backdrop # myblock
 
 
 
 
 
 copy all the costumes in the backdrop into a new sprite


 
```
when I receive [check current backdrop v]
hide
wait (0) seconds
if <(is clone) = [0]> then
    switch backdrop to [blank v]
    set [brightness v] effect to (0)::looks
    hide
    reset timer
    set [is clone v] to [top left no bg]
    test coverage of backdrop # (is clone)::custom
    set [QUAD1 v] to ((((RESULT) - (OUTSIDE OF SEGMENT)) / (QUAD1 FULL)) * (100))
    show variable [QUAD1 v]
    if <(QUAD1) > [80]> then
        create clone of [myself v]
    end
    set [is clone v] to [top right no bg]
    test coverage of backdrop # (is clone)::custom
    set [QUAD2 v] to ((((RESULT) - (OUTSIDE OF SEGMENT)) / (QUAD2 FULL)) * (100))
    if <(QUAD2) > [80]> then
        create clone of [myself v]
    end
    show variable [QUAD2 v]
    set [is clone v] to [bottom left no bg]
    test coverage of backdrop # (is clone)::custom
    set [QUAD3 v] to ((((RESULT) - (OUTSIDE OF SEGMENT)) / (QUAD3 FULL)) * (100))
    if <(QUAD3) > [80]> then
        create clone of [myself v]
    end
    show variable [QUAD3 v]
    set [is clone v] to [bottom right no bg]
    test coverage of backdrop # (is clone)::custom
    set [QUAD4 v] to ((((RESULT) - (OUTSIDE OF SEGMENT)) / (QUAD4 FULL)) * (100))
    if <(QUAD4) > [80]> then
        create clone of [myself v]
    end
    show variable [QUAD4 v]
    switch backdrop to [blank v]
    set [is clone v] to [00]
    broadcast [show variables v]
end

define test coverage of backdrop # (backdrop)
switch costume to (backdrop::custom)
set [ghost v] effect to (0)::looks
show
broadcast [check DRAWN v] and wait
set [OUTSIDE OF SEGMENT v] to (RESULT)
hide
broadcast [check DRAWN v] and wait

when [space v] key pressed
broadcast [hide variables v]
broadcast [check current backdrop v] and wait

when I receive [get initial values v]
clear graphic effects
erase all
set [is clone v] to [0]
switch backdrop to [blank v]
switch costume to [top left no bg v]
show
broadcast [check not white v] and wait
set [QUAD1 FULL v] to (RESULT)
next costume
broadcast [check not white v] and wait
set [QUAD2 FULL v] to (RESULT)
next costume
broadcast [check not white v] and wait
set [QUAD3 FULL v] to (RESULT)
next costume
broadcast [check not white v] and wait
set [QUAD4 FULL v] to (RESULT)
erase all
stamp full costumes::custom

define stamp full costumes
erase all
switch backdrop to [blank v]
go to x: (0) y: (0)
switch costume to [top left2 v]
wait (1) seconds
repeat (4)
    stamp
    next costume
end

when I start as a clone
set [is clone v] to [1]
set [ghost v] effect to (75)::looks
change [whirl v] effect by (100)::looks
set [brightness v] effect to (-50)::looks
show
say (is clone)

when I start as a clone
go to [back v] layer

```

</div>


