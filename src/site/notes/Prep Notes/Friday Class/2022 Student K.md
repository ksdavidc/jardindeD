---
{"dg-publish":true,"permalink":"/prep-notes/friday-class/2022-student-k/","dgHomeLink":true,"dgPassFrontmatter":false}
---



- [[Prep Notes/Friday Class/2022 Student K#08 05|08 05]]
	- [[Prep Notes/Friday Class/2022 Student K#08 05|SKELETON]]
	- [[Prep Notes/Friday Class/2022 Student K#08 05|WEAPONS]]
	- [[Prep Notes/Friday Class/2022 Student K#08 05|MAIKEY]]
	- [[Prep Notes/Friday Class/2022 Student K#08 05|SPIDER HP BAR]]
- [[Prep Notes/Friday Class/2022 Student K#07 29|07 29]]
	- [[Prep Notes/Friday Class/2022 Student K#07 29|MAIKEY]]
	- [[Prep Notes/Friday Class/2022 Student K#07 29|in WEAPONS]]



## 08 05

<div class="blocks">

### SKELETON
```

Add this to make the skeleton step away when he strikes:

when I receive [a hit! v]
if <touching [Weapons v]?> then
    point towards [maikey v]
    move (-50) steps
end

```

### WEAPONS

```
change 
 if <key (join [] (clone id)) pressed?> then
 to this:
if <<key (join [] (clone id)) pressed?> or <<touching [mouse-pointer v]?> and <mouse down?>>> then


when I receive [attack v]
set rotation style [all around v]
turn @turnRight ((15) * (ABS of MAIKEY DIRECTION)) degrees::motion
if <<touching [スケルトン v]?> or <touching [くも v]?>> then
    change [HP v] by (5)
    broadcast [a hit! v]
end
wait (.1) seconds
point in direction (MAIKEY DIRECTION)

FIND:
when I receive [attack v]
set rotation style [all around v]

DELETE this:
turn @turnRight (15) degrees::motion
get abs (MAIKEY DSIRECTION)::custom
point in direction ((MAIKEY DSIRECTION) + ((15) * (abs)))

and REPLACE it with:
turn @turnRight ((15) * (ABS of MAIKEY DSIRECTION)) degrees::motion

KEEP this:
if <<touching [スケルトン v]?> or <touching [くも v]?>> then
    change [HP v] by (5)
    broadcast [a hit! v]
end
wait (.1) seconds

DELETE this:
set rotation style [left-right v]

KEEP this:
point in direction (MAIKEY DSIRECTION)

DELETE: (we will move this to MAIKEY)
define get abs (number or text)
set [abs v] to (([abs v] of (number)::operators) / (number or text::custom))

DELETE: (if you look we already have this...)
when I start as a clone
show
go to [front v] layer

IN THIS STACK:
define mikey
....

FIND:
    change x by (32)
and MAKE IT
    change x by (((32) * <not <(MAIKEY DSIRECTION) < [0]>>) + ((-32) * <(MAIKEY DSIRECTION) < [0]>))
    point in direction ((MAIKEY DSIRECTION) + ((90) * <(ABS of MAIKEY DIRECTION) < [0]>))

```

### MAIKEY

```

CREATE:
define set maikeys direction
set [MAIKEY DIRECTION v] to (direction)
set [ABS of MAIKEY DIRECTION v] to (([abs v] of (MAIKEY DSIRECTION)::operators) / (MAIKEY DSIRECTION))

CHANGE:
when [right arrow v] key pressed
move (10) steps
TO:
when [right arrow v] key pressed
point in direction (90)
set maikeys direction::custom
move (10) steps

CHANGE:
when [left arrow v] key pressed
move (-10) steps
TO (note that -10 becomes 10):
when [left arrow v] key pressed
point in direction (-90)
set maikeys direction::custom
move (10) steps


CHANGE  THIS STACK:
when I receive [c.b v]
...
TO
when I receive [c.b v]
set rotation style [left-right v]
set maikeys direction::custom
set [HP v] to [100]
hide
repeat until <not <(HP) > [0]>>
    say (direction)
    if <key [space v] pressed?> then
        set maikeys direction::custom
        broadcast [attack v]
    end
end



```

### SPIDER HP BAR

```
First CHANGE THE NAME

ADD
when I receive [15 v]
hide
set [SPIDER HP v] to [50]
set [my color v] to [40]
set [starting x v] to [-220]
set [starting y v] to [135]
go to x: (starting x) y: (starting y)

ADD
when I receive [draw healths v]
draw health ((2) * (SPIDER HP))::custom

ADD {a second receive 15 stack}
when I receive [15 v]
set pen (color v) to {(my color)}
set pen size to (20)
forever
    erase all
    broadcast [draw healths v]
end

ADD: 
define draw health (health)
go to x: (starting x) y: (starting y)
pen down
point in direction (90)
move (health::custom) steps
pen up


```


</div >


## 07 29


<div class="blocks">


### MAIKEY

```

LET'S MAKE SURE MAIKEY IS POINTING IN THE RIGHT DIRECTION 

MAKE THIS INTO:

when I receive [c.b v]
set rotation style [left-right v]
set [HP v] to [100]
hide
repeat until <not <(HP) > [0]>>
    set [MAIKEY DIRECTION v] to (direction)
    if <key [space v] pressed?> then
        broadcast [attack v]
    end
end

to the right arrow:
point in direction (90)

to the left arrow
point in direction (-90)
```

### in WEAPONS

```
if <touching mouse-pointer> then
say (costume name)
else
say ()
end
change all costume names to weapon name
```



</div>