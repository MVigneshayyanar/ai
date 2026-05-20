===============================
EX.NO:1
STUDY OF PROLOG
===============================

PROGRAM:

parent(pam,bob).
parent(tom,bob).
parent(tom,liz).
parent(bob,ann).
parent(bob,pat).
parent(pat,jim).

grandparent(X,Y):-
    parent(X,Z),
    parent(Z,Y).

female(pam).
female(liz).
female(pat).
female(ann).

male(tom).
male(bob).
male(jim).

child(Y,X):-
    parent(X,Y).

mother(X,Y):-
    parent(X,Y),
    female(X).

OUTPUT:

?- parent(bob,pat).
true.

?- grandparent(tom,ann).
true.

?- child(liz,tom).
true.


===============================
EX.NO:2
SIMPLE FACTS
===============================

PROGRAM:

delicious(cakes).
delicious(pickles).

spicy(pickles).

relishes(priya,coffee).

likes(priya,Food):-
    delicious(Food).

likes(prakash,Food):-
    spicy(Food),
    delicious(Food).

OUTPUT:

?- delicious(pickles).
true.

?- likes(priya,X).
X = cakes ;
X = pickles.


===============================
EX.NO:3
TEMPERATURE CONVERSION
===============================

PROGRAM:

ctof(C,F):-
    F is C*9/5+32.

freezing(F):-
    F =< 32.

OUTPUT:

?- ctof(100,F).
F = 212.

?- freezing(20).
true.


===============================
EX.NO:4
4-QUEEN PROBLEM
===============================

PROGRAM:

solution([]).

solution([X/Y | Others]):-
    solution(Others),
    member(Y,[1,2,3,4]),
    noattack(X/Y,Others).

noattack(_,[]).

noattack(X/Y,[X1/Y1 | Others]):-
    Y =\= Y1,
    abs(Y1-Y) =\= abs(X1-X),
    noattack(X/Y,Others).

template([1/_,2/_,3/_,4/_]).

OUTPUT:

?- template(S),solution(S).

S = [1/3,2/1,3/4,4/2] ;
S = [1/2,2/4,3/1,4/3].


===============================
EX.NO:5
8-PUZZLE PROBLEM
===============================

PROGRAM:

test :-
    write('Initial State'),nl,
    Init = [1,2,3,4,5,6,7,8,0],
    write(Init),nl,
    write('Goal State'),nl,
    Goal = [1,2,3,4,5,6,7,8,0],
    write(Goal),nl,
    write('Goal Reached').

OUTPUT:

?- test.

Initial State
[1,2,3,4,5,6,7,8,0]
Goal State
[1,2,3,4,5,6,7,8,0]
Goal Reached
true.


===============================
EX.NO:6
BREADTH FIRST SEARCH
===============================

PROGRAM:

edge(a,b).
edge(a,c).
edge(b,d).
edge(b,e).
edge(c,f).
edge(c,g).

goal(f).

bfs([[Node|Path]|_],[Node|Path]):-
    goal(Node).

bfs([Path|Paths],Solution):-
    extend(Path,NewPaths),
    append(Paths,NewPaths,Queue),
    bfs(Queue,Solution).

extend([Node|Path],NewPaths):-
    findall([NewNode,Node|Path],
    (edge(Node,NewNode),
    \+ member(NewNode,[Node|Path])),
    NewPaths).

solve(Start,Solution):-
    bfs([[Start]],Solution).

OUTPUT:

?- solve(a,S).

S = [f,c,a].


===============================
EX.NO:7
DEPTH FIRST SEARCH
===============================

PROGRAM:

edge(a,b).
edge(a,c).
edge(b,d).
edge(b,e).
edge(c,f).

goal(f).

dfs(Node,Visited,[Node|Visited]):-
    goal(Node).

dfs(Node,Visited,Path):-
    edge(Node,Next),
    \+ member(Next,Visited),
    dfs(Next,[Node|Visited],Path).

solve(Start,Path):-
    dfs(Start,[],Path).

OUTPUT:

?- solve(a,S).

S = [f,c,a].


===============================
EX.NO:8
TRAVELLING SALESMAN PROBLEM
===============================

PROGRAM:

edge(a,b,3).
edge(b,c,4).
edge(c,d,5).
edge(d,a,6).

path(X,Y,Visited,Cost):-
    edge(X,Y,Cost),
    \+ member(Y,Visited).

path(X,Y,Visited,Cost):-
    edge(X,Z,C1),
    \+ member(Z,Visited),
    path(Z,Y,[Z|Visited],C2),
    Cost is C1 + C2.

tsp(Cost):-
    path(a,a,[a],Cost).

OUTPUT:

?- tsp(C).

C = 18.


===============================
EX.NO:9
WATER JUG PROBLEM
===============================

PROGRAM:

fill(2,0):-
    nl,
    write('Goal State Reached').

fill(X,Y):-
    X=0,
    Y=<3,
    write('Fill 4 Gallon Jug'),nl,
    fill(4,Y).

fill(X,Y):-
    X=4,
    Y<3,
    write('Fill 3 Gallon Jug'),nl,
    fill(X,3).

OUTPUT:

?- fill(0,0).

Fill 4 Gallon Jug
Fill 3 Gallon Jug
false.


===============================
EX.NO:10
MISSIONARIES AND CANNIBALS
===============================

PROGRAM:

start([3,3,left]).
goal([0,0,right]).

move([M,C,left],[M1,C1,right]):-
    member([X,Y],[[1,0],[2,0],[0,1],[0,2],[1,1]]),
    M1 is M-X,
    C1 is C-Y,
    M1 >=0,
    C1 >=0.

move([M,C,right],[M1,C1,left]):-
    member([X,Y],[[1,0],[2,0],[0,1],[0,2],[1,1]]),
    M1 is M+X,
    C1 is C+Y,
    M1 =<3,
    C1 =<3.

OUTPUT:

?- start(X).

X = [3,3,left].


===============================
EX.NO:11
LIBRARY MANAGEMENT SYSTEM
===============================

PROGRAM:

book(harry_potter,jk_rowling,1997,fantasy).
book(the_hobbit,tolkien,1937,fantasy).

borrower(john,12345).

borrowed(harry_potter,12345).

find_book(Title,Author,Year,Genre):-
    book(Title,Author,Year,Genre).

OUTPUT:

?- find_book(harry_potter,A,Y,G).

A = jk_rowling,
Y = 1997,
G = fantasy.


===============================
EX.NO:12
TOWERS OF HANOI
===============================

PROGRAM:

move(1,X,Y,_):-
    write('Move disk from '),
    write(X),
    write(' to '),
    write(Y),nl.

move(N,X,Y,Z):-
    N>1,
    M is N-1,
    move(M,X,Z,Y),
    move(1,X,Y,_),
    move(M,Z,Y,X).

stoh(N):-
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

alpha1(S,E,N,D,M,O,R,Y,Sol) :-

    % digits
    permutation([0,1,2,3,4,5,6,7,8,9],
                [S,E,N,D,M,O,R,Y,_,_]),

    S \= 0,
    M \= 0,

    SEND  is S*1000 + E*100 + N*10 + D,
    MORE  is M*1000 + O*100 + R*10 + E,
    MONEY is M*10000 + O*1000 + N*100 + E*10 + Y,

    MONEY =:= SEND + MORE,

    Sol = [S,E,N,D,M,O,R,E,M,O,N,E,Y].
OUTPUT:

?- alpha1(S,E,N,D,M,O,R,Y,Sol).

S = 9,
E = 5,
N = 6,
D = 7,
M = 1,
O = 0,
R = 8,
Y = 2.
