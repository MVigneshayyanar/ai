===============================
EX.NO:1
STUDY OF PROLOG
===============================

PROGRAM:

parent(pam, bob).
parent(tom, bob).
parent(tom, liz).
parent(bob, ann).
parent(bob, pat).
parent(pat, jim).

grandparent(X,Y):-parent(X,Z),parent(Z,Y).

female(pam).
male(tom).
male(bob).
female(liz).
female(pat).
female(ann).
male(jim).

child(Y,X):-parent(X,Y).

mother(X,Y):- parent(X,Y), female(X).

OUTPUT:

?- parent(bob,pat).
true.

?- parent(liz,pat).
false.

?- parent(X,liz).
X = tom.

?- grandparent(tom,ann).
true.

?- male(jim).
true.

?- child(liz,tom).
true.

?- mother(pam,bob).
true.


===============================
EX.NO:2
SIMPLE FACT FOR THE STATEMENTS
===============================

PROGRAM:

delicious(cakes).
delicious(pickles).
spicy(pickles).
relishes(priya, coffee).

likes(priya, Food):- delicious(Food).
likes(prakash,Food):- spicy(Food), delicious(Food).

OUTPUT:

?- delicious(pickles).
true.

?- spicy(pickles).
true.

?- relishes(priya,coffee).
true.

?- delicious(Food).
Food = cakes ;
Food = pickles.


===============================
EX.NO:3
TEMPERATURE CONVERSION
===============================

PROGRAM:

ctof(C,F):-F is C*9/5+32.

freezing(F):-F=<32.

OUTPUT:

?- ctof(100,F).
F = 212.

?- freezing(20).
true.

?- freezing(40).
false.


===============================
EX.NO:4
4-QUEEN PROBLEM
===============================

PROGRAM:

solution([]).

solution([X/Y | Others]):-
solution(Others),
mem(Y,[1,2,3,4]),
noattack(X/Y,Others).

noattack(_,[]).

noattack(X/Y,[X1/Y1 | Others]):-
Y =\= Y1,
Y1-Y =\= X1-X,
Y1-Y =\= X-X1,
noattack(X/Y,Others).

mem(X,[X|_]).

mem(X,[_|T]):-mem(X,T).

template([1/Y1,2/Y2,3/Y3,4/Y4]).

OUTPUT:

?- template(S),solution(S).

S = [1/3,2/1,3/4,4/2] ;
S = [1/2,2/4,3/1,4/3];


===============================
EX.NO:5
8-PUZZLE PROBLEM
===============================

PROGRAM:

test(Plan):-
write('Initialstate:'),nl,
Init=[at(tile4,1),at(tile3,2),at(tile8,3),at(empty,4),
at(tile2,5),at(tile6,6),at(tile5,7),
at(tile1,8), at(tile7,9)],
write_sol(Init),

Goal=[at(tile1,1),at(tile2,2),at(tile3,3),
at(tile4,4),at(empty,5),at(tile5,6),
at(tile6,7),at(tile7,8), at(tile8,9)],

solve(Init,Goal,Plan).

solve(State, Goal, Plan):-
solve(State,Goal,[],Plan).

is_movable(X1,Y1):-
(1 is X1-Y1);
(-1 is X1-Y1);
(3 is X1-Y1);
(-3 is X1-Y1).

OUTPUT:

?- test(Plan).

Initial state:
at(tile7,9)
at(tile1,8)
at(tile5,7)

Goal state:
[at(tile1,1),at(tile2,2),at(tile3,3),
at(tile4,4),at(empty,5),at(tile5,6),
at(tile6,7),at(tile7,8),at(tile8,9)]

false.


===============================
EX.NO:6
BREADTH FIRST SEARCH
===============================

PROGRAM:

s(a,b).
s(a,c).
s(b,d).
s(b,e).
s(c,f).
s(c,g).

goal(f).
goal(j).

solve(Start,Solution):-
bfs([[Start]],Solution).

bfs([[Node|Path]|_],[Node|Path]):-
goal(Node).

OUTPUT:

?- solve(a,S).

[[b,a],[c,a]]

S = [f, c, a] ;


===============================
EX.NO:7
DEPTH FIRST SEARCH
===============================

PROGRAM:

s(a,b).
s(a,c).
s(b,d).
s(b,e).
s(c,f).

goal(f).
goal(j).

mem(X,[X|_]).

mem(X,[_|Tail]):-mem(X,Tail).

solve(Node,Solution):-
dfs([],Node,Solution).

dfs(Path,Node,[Node|Path]):-
goal(Node).

OUTPUT:

?- solve(a,S).

S = [j, e, b, a] ;
S = [f, c, a]


===============================
EX.NO:8
TRAVELLING SALESMAN PROBLEM
===============================

PROGRAM:

edge(a, b, 3).
edge(a, c, 5).
edge(a, d, 7).
edge(a, e, 8).

len([], 0).
len([H|T], N):- len(T, X), N is X+1.

best_path(Visited, Total):-
path(a, a, Visited, Total).

shortest_path(Path):-
setof(Cost-Path, best_path(Path,Cost), Holder),
pick(Holder,Path).

OUTPUT:

?- shortest_path(Path).

Path = 22-[a, h, d, c, e, b, a].


===============================
EX.NO:9
WATER JUG PROBLEM
===============================

PROGRAM:

fill(x,y).

fill(2,0):-
nl,
write('Goal State is Reached....').

fill(X,Y):-
X=0,
Y=<1,
write('Fill the 4-Gallon Jug'),
fill(4,Y).

OUTPUT:

?- fill(4,0).

Fill the 3-Gallon Jug:(4,3)
Empty the 4-Gallon Jug on Ground:(0,3)
pour all the water from 3-Gallon Jug to 4-Gallon:(3,0)
Fill the 3-Gallon Jug:(3,3)
Pour water from 3-Gallon Jug to 4-Gallon until is full:(4,2)
Empty the 4-Gallon Jug on Ground:(0,2)
pour all the water from 3-Gallon Jug to 4-Gallon:(2,0)

Goal State is Reached....


===============================
EX.NO:10
MISSIONARIES AND CANNIBAL PROBLEM
===============================

PROGRAM:

start([3,3,left,0,0]).

goal([0,0,right,3,3]).

legal(CL,ML,CR,MR) :-
ML>=0, CL>=0, MR>=0, CR>=0,
(ML>=CL ; ML=0),
(MR>=CR ; MR=0).

OUTPUT:

?- find.

[3,3,left,0,0] -> [1,3,right,2,0]
[1,3,right,2,0] -> [2,3,left,1,0]
[2,3,left,1,0] -> [0,3,right,3,0]
[0,3,right,3,0] -> [1,3,left,2,0]
[1,3,left,2,0] -> [1,1,right,2,2]
[1,1,right,2,2] -> [2,2,left,1,1]
[2,2,left,1,1] -> [2,0,right,1,3]
[2,0,right,1,3] -> [3,0,left,0,3]
[3,0,left,0,3] -> [1,0,right,2,3]
[1,0,right,2,3] -> [1,1,left,2,2]
[1,1,left,2,2] -> [0,0,right,3,3]


===============================
EX.NO:11
LIBRARY MANAGEMENT SYSTEM
===============================

PROGRAM:

book(harry_potter_1, jk_rowling, 1997, fantasy).
book(the_hobbit, jrr_tolkien, 1937, fantasy).

borrower(john, doe, 12345).

borrowed(harry_potter_1, 12345).

find_book_by_title(Title, Author, Year, Genre) :-
book(Title, Author, Year, Genre).

OUTPUT:

?- find_book_by_author(jk_rowling,A,Y,G).

A = harry_potter_1,
Y = 1997,
G = fantasy.

?- find_borrower_by_id(12345,A,B).

A = john,
B = doe.

?- list_borrowed_books.

Book: harry_potter_1, Author: jk_rowling,
Year: 1997, Genre: fantasy, Borrower: john doe


===============================
EX.NO:12
TOWERS OF HANOI
===============================

PROGRAM:

move(1,X,Y,_) :-
write('Move disk from '),
write(X),
write(' to '),
write(Y),
nl.

move(N,X,Y,Z) :-
N > 1,
M is N - 1,
move(M,X,Z,Y),
move(1,X,Y,_),
move(M,Z,Y,X).

stoh(N) :-
move(N,left,right,center).

OUTPUT:

?- stoh(3).

Move disk from left to right
Move disk from left to center
Move disk from right to center
Move disk from left to right
Move disk from center to left
Move disk from center to right
Move disk from left to right

true.


===============================
EX.NO:13
CRYPT ARITHMETIC PROBLEM
===============================

PROGRAM:

alpha1(S, E, N, D, M, O, R, Y,
[S, E, N, D, M, O, R, E, M, O, N, E, Y]) :-

between(1, 9, S),
between(0, 9, E),
E \=S,

Send is S*1000 + E*100 + N*10 + D,
More is M*1000 + O*100 + R*10 + E,
Money is M*10000 + O*1000 + N*100 + E*10 + Y,

Money is Send + More.

OUTPUT:

?- alpha1(S, E, N, D, M, O, R, Y, Sol).

S = 9,
E = 5,
N = 6,
D = 7,
M = 1,
O = 0,
R = 8,
Y = 2,
Sol = [9, 5, 6, 7, 1, 0, 8, 5, 1|...];
