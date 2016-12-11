# tema-2
clc;
clear all;
close all;

% durata =22
D=22;
% perioada=40
P=40;

w0=2*pi/P;
t_T=0:0.01:D;
% sawtooth genereaza un semnal dinte de fierastrau
xTriunghi= sawtooth((pi/11)*t_T,0.5)/2+0.5; 
t = 0:0.01:P-0.01; 
x = zeros(1,length(t)); 

for i = 1: size(t_T,2)-1
x(i) =xTriunghi(i); 
end


%calcularea coeficientilor fourier
for k = -50:50
    xSuma = x;
    xSuma = xSuma.*exp(-j*k*w0*t);
    X(k+51) = trapz(t,xSuma);
end
    
%afisearea lui x original
figure(1);
plot(t,x); 
title('x(t)(linie solida) si reconstructia folosind N coeficienti (linie punctata)');

% reconstruirea semnalului
for i = 1: length(t)
    x_r(i) = 0;
    for k=-50:50
        x_r(i) = x_r(i) + (1/P)*X(k+51)*exp(j*k*w0*t(i)); 
    end
end

%afisarea cu linie punctata
hold on;
plot(t,x_r,'--'); 

% afisarea spectrului
figure(2);
w=-50*w0:w0:50*w0; 
stem(w/(2*pi),abs(X));
title('Spectrul lui x(t)')


