# Matlab Tricks
## anonymous function
```matlab
sqrt = @(x) x.^2 
sqrt(10)
```
## function handle
example: solve an ode
```matlab
tspan=[3.9 4.0]; %求解区间
y0=[8 2]; %初值
[t,x]=ode45(@odefun,tspan,y0);

function y=odefun(t,x)
    y=zeros(2,1); % 列向量
    y(1)=x(2);
    y(2)=-t*x(1)+exp(t)*x(2)+3*sin(2*t); %常微分方程公式
end
```

```matlab
f = @(t,Y) [Y(2), -sin(Y(1))];
y1 = linsppace(-2,8,20);
y2 = linspace(-2,2,20);
[x, y] = meshgrid(y1, y2);
u = zeros(size(x));
v = zeros(size(y));
t = 0;
for i = 1:numel(x)
    Y_prime = f(t,[x(i),y(i)]);
    u(i) = Y_prime(1);
    v(i) = Y_prime(2);
end

quiver(x,y,u,v,'r');
xlabel('y1')
ylabel('y2')
axis tight equal
hold on

for y20 = [0 0.5 1 1.5 2 2.5]
    [ts, ys] = ode45(f, [0,50], [0;y20]);
    plot(ys(:,1), ys(:,2))
    plot(ys(1,1), ys(1,2), 'bo') % start point
    plot(ys(end,1), ys(end,2), 'ks') % end point
end

```
## class
```matlab
classdef WaypointClass
    properties
        latitude
        longtitude
    end
    methods
        % constructor
        function obj = WaypointClass(lat, lon)
            obj.latitude = lat;
            obj.longtitude = lon;
        end

        function r = multiplyLatBy(obj, n)
            r = n * [obj.latitude];
        end
        % overload arithmetic operator
        function r = plus(o1, o2)
            r = WaypointClass([o1.latitude]+[o2.latitude],...
            [o1.longtitude]+[o2.longtitude]);
        end
    end
end

```
## nargin nargout
nargin：number of argument in 
nargout：number of argument out

```matlab
function [x0, y0] = myplot(x, y, npts, angle, subdiv)
if nargin < 5, subdiv = 20; end
if nargin < 4, angle = 10; end
if nargin < 3, npts = 25; end
 ...
if nargout == 0
     plot(x, y)
else
     x0 = x;
     y0 = y;
end

```

## varargin varargout
varargin : variable argument in
varargout : variable argument outvarargout

``` matlab
function  varargout = foo(varargin)
    fprintf('How many output arguments? %d \nAnd they are: \n',nargout);
    for k=1:nargout
        varargout(k) = varargin(k); % the same as {varargin{k}};
        fprintf('%s ', num2str(varargout{k}));
    end
    disp(' ');
end
```