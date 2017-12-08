# Heuristics

This document is designed to outline the basic elements and interpretation of
each element.

## Header

The first X number of lines are for description. It's possible that this
section will be one day used to define variables for code-compile time.
Everything up to the first set of 7 consecutive underscores should be
considered a part of the header.

```
HEADER
HEADER WOOHOO
________
~all code down here!
```

## Input

Input signal shoots rightward and enters from the upper-leftmost square below
the header

## Signals

### Timing
each signal moves once per block

### Stacked Signals
strings are an example of this


## Operators and Direction Flow

### Directionality

There are 8 directions used by ASSCII
```
NW N NE
 W   E  
SW S SE
```
Signals can travel along all these directions (yes including diagonals).


### Operators 

Operators include:
 - `+` concatenate string
 - `+`,`-`,`*`,`/` basic math stuff
 - `(`,`)` brackets used for logic equations
 - `|`, `&` or/and in logic 
 - `>`, `<`, `=`, `<=`, `>=`, `!=` equalities 
 
### Direction / Concurrency

#### Lone operator

If a signal passes by a single lone operator, then the signal will be 
keep on trajecting in the same direction, but as an incomplete signal-operation
if another character is then hit during it's trajection, then that operation
may be complete and the signal will continue to traject.Ex:

```
5>    +      2    >signal here will be 7
```


#### Operator with friends

If an operator has any adjacent pals hanging out then the signalling entering
will perform the operation and further more continue on a new trajectory. Ex:

```
5>    +
       2
        the signal here will be 7
```

#### Clumps

If a whole bunch of stuff is clumped together then we should intepret the clump 
from left to right, followed by the next line

If you hit a clump from any such angle you should still process that clump from
left to right (starting at the NW corner) and then keep moving on your way as
if you had passed STRAIGHT THROUGH that clump.


#### Signal Diversions 

Signal directionality can be changed during the procressing of one of these operators

 - `>` 
 - `<` 
 - `v` 
 - `^` 
 - `>v`
 - `>^`
 - `v>`
 - `v<`

#### Splits

Concurrency can be achieved using the split operators, `{` and `}`. 

If the signal enters from the one-pointed end of the operator, one signal is
split into two, At the next step both signals are processed to the next block
as following: 

```
  2 (travelling rightward)
1{
  2 (travelling rightward)
```

Similarly the split operators can be used in reverse, where any single signal
is shifted down the same direction.

```
1   
 }2 travelling rightward
``` 
or
```
1}2 travelling rightward
``` 
or
```
 }2 travelling rightward
1
``` 
Note that if multiple signals enter into to the split at the same time, 
the signals are stacked from uppermost to lowermost

```
1
2} (1,2,3) stacked signal travelling rightward
3
```

#### Stacked Signal Operators
Basic primitives exist to operate on stacked signals, however more can be custom defined. 

An operation on a stack should always begin with the split operator. Ex:

add evertything in the stack
```
}+
```

##### Referencing elements within the stack

should treat it like an array
```
s[0]
```


# 3rd PArty Library

3rd party library functions can be used, custom mechansisms for these library functions will
need to be defined for each programming language, as well as how to deal with processing
out-of band according to the stepwise function.
