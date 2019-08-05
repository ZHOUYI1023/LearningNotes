Inline Function Uses Guidelines :-
1. Always use inline function when your are sure it will give performance.
1. Always prefer inline function over macros.
1. Don't inline function with larger code size, one should always inline small code size function to get performance.
1. If you want to inline a function in class, then prefer to use inkine keyword outside the class with the function definition.
1. In c++, by default member function declared and defined within class get linlined. So no use to specify for such cases.
1. Your function will not be inlined in case there is differences between exception handling model. Like if caller function follows c++ structure handling and your inline function follows structured exception handling.
1. For recursive function most of the compiler would not do in-lining but microsoft visual c++ compiler provides a special pragma for it i.e. pragma inline_recursion(on) and once can also control its limit with pragma inline_depth.

1. If the function is virtual and its called virtually then it would not be inlined. So take care for such cases, same hold true for the use of function pointers.