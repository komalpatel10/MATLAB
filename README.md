# MATLAB
Bouncing ball for Body Movement 
%Given  values
x0=-5;  y0=0;  z0=200;  v0_x=2;  v0_y=4;  v0_z=0;
%values  of  Constants
g  =  10;  bounce_loop  =  5;  k  =  1;
%Calculate  the  diffT
diffT  =  t_1(x0,  y0,  z0,  v0_x,  v0_y,  v0_z,  g);
%Calculate  the  Velocity  before  movement v  =  [v0_x,  v0_y,  v0_z  -  g*diffT];
x=x0;  y=y0;  z=z0;
%result  =  [0,x0,y0,z0];
result  =  [];
for  n  =  1  :  bounce_loop
%Calculate  position
x  =  x  +  v(1)  *diffT; y  =  y  +  v(2)  *diffT; z  =  x^2+y^2;
if  n  ==  1
v(3)  =  v(3)  -  g*diffT;
end
%Find  The  Kinetic,  Potential  and  Total  Energies
Ek  =  norm(v)^2/2;  Ep  =  g*z;  Et  =  Ek  +  Ep;
%Calculate  the  Velocity  after  movement v  =  v_after(v,  k,  x,  y);
%v(3)  =  v(3)  -  g*diffT;
%Final  matrix
result  =  [result;[diffT,x,y,z,Ek,Et]];
%Calculate  the  diffT
diffT  =  t_1(x,  y,  z,  v(1),  v(2),  v(3),  g);
end result

%Make  plot
x  =  -30:1:30;
y  =  -30:1:30;
[X,Y]  =  meshgrid(x,y); mesh(X,Y,X.^2+Y.^2) hold  on
plot3(result(:,2),result(:,3),result(:,4),'r','LineWidth',2);
hold  off xlabel("x") ylabel("y") zlabel("z") xlim([-15  15]) ylim([-15  15]) zlim([0  400])
function  v  =  v_after(v_before,  k,  x_value,y_value)
syms  x  y  z;

%for root  equations
f  =  x^2  +  y^2; 
N  =  [subs(-diff(f,x),x,x_value),  subs(-diff(f,y),y,y_value),  1];

N_norm  =  norm(N); n_normal  =  N./N_norm; n_normal  =  double(n_normal);
v  =  sqrt(k)  .*  (v_before  -  2.*(  dot(v_before,  n_normal)  )  .*  n_normal);
end
Helper  Function

function  time  =  t_1(x,  y,  z,  vx,  vy,  vz,  g)
syms  t;  time  =  -inf;
t1  =  double(solve(z  +  vz*t  -  0.5*g*(t^2)  ==  (x  +  vx*t)^2  ...
+  (y  +  vy*t)^2,  t));

for  tim  =  [t1(1),t1(2)]
if  isreal(tim)  &&  tim  >  time time  =  tim;
end end end


