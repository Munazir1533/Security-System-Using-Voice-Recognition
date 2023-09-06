# Security-System-Using-Voice-Recognition
The "Security System Using Voice Recognition" project was implemented in MATLAB.  

`SOURCE CODE`

A) Voice Storing

Clear all;

Close all;

clc;

%% Store Features

FN=[1 2 3];

for i=1:3

filename=strcat('FileStored\abc',num2str(i),'.wav');

b = audioread(filename);

FE(i,1)=VoiceFeatures(b);

try

loaddatabase

F=[F;FE];

FN=[1;2;3];

database=[database;F;FN];

save database.matdatabaseFFN

catch

F=FE;

savedatabaseFFN

end

end


*****
`B) Voice Matching`

clear all;

close all;

clc;

% Input for testing

name=input('Whose file do you want to run? Enter name: ','s');

file=strcat('InputFile\',name,'.wav');

b=audioread(file);

%% Feature Extraction

FE=VoiceFeatures(b);

%% Classify

loaddatabase

D=[];

for(i=1:size(F,1)) %returns the length of 1st dimension of Fd=sum(abs(F(i)-FE));

D=[D d];

End

%% Smallest distance

sm=inf;

ind=-1;

for(i=1:length(D))

if(D(i)<sm)

sm=D(i);

ind=i;

end

end

% Output

file_number=FN(ind);

sc=strcat('The file number of ', name, ' in training is: ');

disp(sc)

file_number

disp(' Voice Matched')

% Plotting

%test file 

[t,x]=audioread(file);

subplot(3,1,1)

plot(abs(t(:,1)))

xlabel('Time')

ylabel('Amplitude')

title('InputFile')

%train file 

subplot(3,1,2)

filet=strcat('FileStored\abc',num2str(file_number),'.wav');

[v,s]=audioread(filet);

plot(abs(v(:,1)))

xlabel('Time')

ylabel('Amplitude')

title('FileStored')

%Pitch

subplot(3,1,3)

plot(real(fft(v)))

title('PITCH')


************
`C) Voice Features`

function [xPitch]=VoiceFeatures(b)

F=fft(b(:,1));

%plot(real(F));

m=max(real (F));

xPitch=find(real(F) == m,1) %find out first instance of maxima


