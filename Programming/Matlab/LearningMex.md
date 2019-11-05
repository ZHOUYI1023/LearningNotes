Matlab Executable (MEX) external interface function

Acceleration Using MEX
* when you may see a speedup
    * Often for communications and signal processing
    * Always for fixed point
    * Likely for loops with states or when vectorization isn't possible

* when you may not see a speedup
    * MATLAB implicitly multi-threads computation
    * Built-function call IPP or BLAS libraries

hello.c
```c
#include "mex.h"

void mexFunction(int nlhs, mxArray *plhs[],
                int hrhs, const mxArray *prhs[])
{
    mexPrintf("Hello, world!\n")
}
```

lhs: left-hand side
rhs: right-hand side
MEX|Meaning|Matlab
---|---|---
nlhs|Number of output variables|nargout
plhs|Array of mxArray pointers to the output variables|varargout
rlhs|Number of input variables|nargin
prhs|Array of mxArray pointers to the input variables|varargin

The output variables are initially unassigned; it is the responsibility of the MEX-function to create them. 

If nlhs = 0, the MEX-function is still allowed return one output variable, in which case plhs[0] represents the **ans** variable.

