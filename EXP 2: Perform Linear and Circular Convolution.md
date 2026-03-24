# EXP 1 : Linear and Circular Convolution

## AIM: 

 To perform Linear and Circular Convolution for two given sequence using SCILAB. 

## APPARATUS REQUIRED: 
PC installed with SCILAB. 

## PROGRAM (Linear Convolution): 
```
clc;
clear;
clf;

// Define sequences
x = [1 2 3 4];      // First sequence
h = [1 1 1];        // Second sequence

lx = length(x);
lh = length(h);

// Length of output
ly = lx + lh - 1;

// Initialize output
y = zeros(1, ly);

// Manual convolution
for n = 1:ly
    for k = 1:lx
        if (n-k+1 > 0) & (n-k+1 <= lh) then
            y(n) = y(n) + x(k) * h(n-k+1);
        end
    end
end

// Display results
disp("First sequence x(n) = " + string(x));
disp("Second sequence h(n) = " + string(h));
disp("Linear Convolution y(n) = " + string(y));

// Plot results
subplot(3,1,1);
plot2d3(0:lx-1, x);
xtitle("First Sequence x(n)","n","x(n)");

subplot(3,1,2);
plot2d3(0:lh-1, h);
xtitle("Second Sequence h(n)","n","h(n)");

subplot(3,1,3);
plot2d3(0:ly-1, y);
xtitle("Convolution Result y(n)","n","y(n)");
```

## PROGRAM (Circular Convolution): 
```
clc;
clear;
clf;

// Input sequences
x = [1 5 2 4];
h = [1 2 4 3];
N = length(x);   // Circular length

// FFT Method
X = fft(x, -1);   // Forward FFT
H = fft(h, -1);

Y = X .* H;       // Multiply in frequency domain
y = real(fft(Y, 1));  // Inverse FFT and keep real part

// Display
disp("Sequence x(n) = " + string(x));
disp("Sequence h(n) = " + string(h));
disp("Circular Convolution y(n) = " + string(y));

// Index
n = 0:N-1;

// Plot x(n)
subplot(3,1,1);
plot2d3(n, x);
xtitle("Sequence x(n)", "n", "x(n)");
a = gca();
a.data_bounds = [-1, min(x)-1; N, max(x)+1];

// Plot h(n)
subplot(3,1,2);
plot2d3(n, h);
xtitle("Sequence h(n)", "n", "h(n)");
a = gca();
a.data_bounds = [-1, min(h)-1; N, max(h)+1];

// Plot y(n)
subplot(3,1,3);
plot2d3(n, y);
xtitle("Circular Convolution Result y(n)", "n", "y(n)");
a = gca();
a.data_bounds = [-1, min(y)-1; N, max(y)+1];
```


## OUTPUT (Linear Convolution): 
<img width="767" height="726" alt="image" src="https://github.com/user-attachments/assets/5bde54e7-8ae7-4c2e-ad59-3d7b3f18183a" />

<img width="1579" height="293" alt="image" src="https://github.com/user-attachments/assets/d65d1fb8-583f-488a-ad3d-3f69e0dcd6cf" />

## OUTPUT (Circular Convolution): 

<img width="763" height="734" alt="image" src="https://github.com/user-attachments/assets/c9af1323-0f5a-497e-a148-1dd1b1436fa1" />

<img width="1429" height="194" alt="image" src="https://github.com/user-attachments/assets/edaf685e-c198-4294-b13e-c3da33b25e57" />

## RESULT: 
Thus, the Linear and Circular Convolution of the given sequences were successfully computed and verified.
