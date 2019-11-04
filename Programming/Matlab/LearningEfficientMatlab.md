Poor Matlab code will run slowly. 
Bad programmers blame Matlab instead of themselves.

## The Profiler
```profview``` in the command window
## MLint
```mlint xxxfunction```

## Tips
### Preallocation and anonymous functions
* Always pre-allocate storage for arrays.
* Prefer anonymous functions over the inline construction.

Example
```matlab
clear all
close all

%% Parameter

% func = inline('[x(1)+1 x(2)-1]','t','x');
% use anonymous function instead of inline function
func = @(t, x) [x(1)+1 x(2)-1];
t_0  = 0;
t_end = 3.02157;
h = 0.0001;
u_0 = [0 0];
Nt = round((t_end - t_0) / h) + 1;
h = (t_end - t_0) / (Nt - 1);

%% IC
t = t_0;
u = u_0;

%% Time-stepping
%{
T= t;
U = u;
for i = 2 : Nt
    u = u + h * func(t, u);
    t = t + h;
    T = [T ; t]; % allocate memory at each itertaion
    U = [U ; u];
end
%}

% Pre allocate memory
T = zeros(Nt, 1);
U = zeros(Nt, length(u));

T(1) = t;
U(1, :) = u_0;
for i = 2 : Nt
    u = u + h*func(t, u);
    t = t + h;
    T(i) = t;
    U(i,:) = u;
end

```

### Evaluating a piecewise function
* Scanning down columns promotes cache effciency, thus the loop order is by row first.
* It is really important to vectorize computations!
* Logical indexing is faster than find.

Example: a piecewise function
``` matlab
% t is a vector of size N
%% implementation 1 Loop
f = zeros(N, 1);
for i = 1:N
    if t(i) < 1
        f(i) = 1;
    elseif t(i) >=1 && t(i) < 2
        f(i) = 2;
    end
end

%% implementation 2 Find
f = zeros(N, 1);
f(find(t < 1>)) = 1; % find return the index
f(find(t >= 1 & t<2>) ) = 2;

%% implementation 3 Logical referencing
f = zeros(N, 1);
f(t < 1) = 1; % return a logical array as a mask
f(t >= 1 & t < 2) = 2;

%% implementation 4 Logical conversion
f = (t < 1) + 2 * (t >= 1 & t < 2) ;
```

### Evaluating a symmetric difference formula
* The implementation with precomputed index vectors is slow.
* When precomputing index arrays, cast them to int32.
* The JIT compiler can somehow accelerate a loopy code
``` matlab
%% direct indexing
fp = [f(2:N); f(1)];
fm = [f(N); f(1:N-1)];
df = (fp - fm)/(2 * h)

%% indirect indexing
%{
ip = [2:N  1];
im = [N 1:N-1];
%}
% cast index vector to int
ip = int32([2:N  1]);
im = int32([N 1:N-1]);
df = (f(ip) - f(im))/(2 * h)

```
### Pass by reference and copy-on-write
* If input to a function is unchanged, this data is passed to the
function as a reference (no copy). 
* An assignment triggers a copy operation, i.e. copy-one-write, which can be costly.
``` matlab
%% pass by reference
function s = sum_matrix(mat)
    s = sum(mat, 'all');

%% copy-on-write
function s = change_and_sum(mat)
    mat(1, 1) = 4000;
    s = sum(mat, 'all');
```

### Constructing a tridiagonal sparse matrix
* A(J(i), K(i)) = X(i), construct a sparse matrix using these three vectors by calling A= sparse(J,K,X) 
* Any insertion of an element into a sparse matrix is really costly!
