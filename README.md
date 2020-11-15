# 540EVENT2
ROUTH HURWITZ SOLUTION 

 
 
 
EC540: Control System '\n'
A Report on \n
Problem statement Solution
By applying Routh-Hurwitz test, find how many roots of the polynomial a(s) =
4s^4 + 12s^3 + 25s^2 + 30s + 60 = 0 are left of -1. Show analytically and then verify
using MATLAB.
 
 
Submitted by 
 
ROLL NO 
NAME 
USN 
57 
SUMANTHA ULLASA PRABHU 
01JST18EC117 
 
 
  
 
Under the guidance of 
SUDHARSHAN PATIL KULKARNI
AssistantProfessor 
DEPARTMENT OF ELECTRONICS AND COMMUNICATION 
SJCE MYSURU- 57000 









THEORETICAL CALCULATION





MATLAB CODE AND PLOT

% Initialization
clear ;
close all;
clc
coeffVector = input('input vector of your system coefficients: \n i.e. [an an-1 an-2 ... a0] = ');
ceoffLength = length(coeffVector);
rhTableColumn = round(ceoffLength/2);

rhTable = zeros(ceoffLength,rhTableColumn);

rhTable(1,:) = coeffVector(1,1:2:ceoffLength);

if (rem(ceoffLength,2) ~= 0)
   % if odd, second row of table will be
   rhTable(2,1:rhTableColumn - 1) = coeffVector(1,2:2:ceoffLength);
else
   % if even, second row of table will be
   rhTable(2,:) = coeffVector(1,2:2:ceoffLength);
end
epss = 0.01;
for i = 3:ceoffLength
   if rhTable(i-1,:) == 0
       order = (ceoffLength - i);
       cnt1 = 0;
       cnt2 = 1;
       for j = 1:rhTableColumn - 1
           rhTable(i-1,j) = (order - cnt1) * rhTable(i-2,cnt2);
           cnt2 = cnt2 + 1;
           cnt1 = cnt1 + 2;
       end
   end
  
   for j = 1:rhTableColumn - 1
firstElemUpperRow = rhTable(i-1,1);
rhTable(i,j) = ((rhTable(i-1,1) * rhTable(i-2,j+1)) - ....
(rhTable(i-2,1) * rhTable(i-1,j+1))) / firstElemUpperRow;
end
% special case: zero in the first column
if rhTable(i,1) == 0
rhTable(i,1) = epss;
end
end
% Initialize unstable poles with zero
unstablePoles = 0;
% Check change in signs
for i = 1:ceoffLength - 1
if sign(rhTable(i,1)) * sign(rhTable(i+1,1)) == -1
unstablePoles = unstablePoles + 1;
end
end
% Print calculated data on screen
fprintf('\n Routh-Hurwitz Table:\n')
rhTable
% Print the stability result on screen
if unstablePoles == 0
fprintf('it is a stable system!\n')
else
fprintf('it is an unstable system!\n')
end
fprintf('\n Number of right hand side poles =%2.0f\n',unstablePoles)
reply = input('Do you want roots of system be shown? Y/N ', 's');
if reply == 'y' || reply == 'Y'
sysRoots = roots(coeffVector);
fprintf('\n Given polynomial coefficients roots :\n')
sysRoots
end


OUTPUT AND PLOTS:

input vector of your system coefficients:
i.e. [an an-1 an-2 ... a0] =
[4 -4 13 0 47]
Routh-Hurwitz Table:

rhTable =
   4.0000   13.0000   47.0000
  -4.0000         0         0
  13.0000   47.0000         0
  14.4615         0         0
  47.0000         0         0

it is an unstable system!

Number of right hand side poles = 2
Do you want roots of system be shown? Y/N
y

Given polynomial coefficients roots :

sysRoots =
  1.2595 + 1.6817i
  1.2595 - 1.6817i
 -0.7595 + 1.4440i
 -0.7595 - 1.4440i

G  = tf([4 -4 13 0 47],[1])
pzmap(G)

If we use the given equation, then in the pzmap there is shift in the imaginary axis but roots remain the same.
G1 = tf([4 12 25 30 60],[1])
pzmap(G1)





CONCLUSION:

As we have seen that in the A(s) equation the necessary condition is not satisfied, i.e  all the coefficients of the equation should be in the same size. Even though it's not a sufficient condition we did the Routh herwitz test in which all the poles(roots ) are present in the right of the plane s = -1.
Thus we can conclude that the system is unstable when the s = -1.and 4 roots are present at the right of the plane s = -1.


Thank you

