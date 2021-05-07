# Demo-Aplikasi-GUI

Project GUI Complement Image

![UTS Pengolahan Citra](https://user-images.githubusercontent.com/81820513/117439747-6e2a0900-af5d-11eb-908b-9d5dabdca362.PNG)

![UTS Pengolahan Citra I](https://user-images.githubusercontent.com/81820513/117439755-72562680-af5d-11eb-90da-1dbcb3314538.PNG)

![UTS Pengolahan Citra II](https://user-images.githubusercontent.com/81820513/117439770-78e49e00-af5d-11eb-8400-4ec4b6a92360.PNG)

![UTS Pengolahan Citra III](https://user-images.githubusercontent.com/81820513/117439784-7bdf8e80-af5d-11eb-8d6e-71a9025d9377.PNG)

![UTS Pengolahan Citra IIII](https://user-images.githubusercontent.com/81820513/117439792-7eda7f00-af5d-11eb-900f-e9422839d038.PNG)

Sourcode :

function varargout = Bismillah(varargin)
% BISMILLAH MATLAB code for Bismillah.fig
%      BISMILLAH, by itself, creates a new BISMILLAH or raises the existing
%      singleton*.
%
%      H = BISMILLAH returns the handle to a new BISMILLAH or the handle to
%      the existing singleton*.
%
%      BISMILLAH('CALLBACK',hObject,eventData,handles,...) calls the local
%      function named CALLBACK in BISMILLAH.M with the given input arguments.
%
%      BISMILLAH('Property','Value',...) creates a new BISMILLAH or raises the
%      existing singleton*.  Starting from the left, property value pairs are
%      applied to the GUI before Bismillah_OpeningFcn gets called.  An
%      unrecognized property name or invalid value makes property application
%      stop.  All inputs are passed to Bismillah_OpeningFcn via varargin.
%
%      *See GUI Options on GUIDE's Tools menu.  Choose "GUI allows only one
%      instance to run (singleton)".
%
% See also: GUIDE, GUIDATA, GUIHANDLES

% Edit the above text to modify the response to help Bismillah

% Last Modified by GUIDE v2.5 06-May-2021 20:40:13

% Begin initialization code - DO NOT EDIT
gui_Singleton = 1;
gui_State = struct('gui_Name',       mfilename, ...
                   'gui_Singleton',  gui_Singleton, ...
                   'gui_OpeningFcn', @Bismillah_OpeningFcn, ...
                   'gui_OutputFcn',  @Bismillah_OutputFcn, ...
                   'gui_LayoutFcn',  [] , ...
                   'gui_Callback',   []);
if nargin && ischar(varargin{1})
    gui_State.gui_Callback = str2func(varargin{1});
end

if nargout
    [varargout{1:nargout}] = gui_mainfcn(gui_State, varargin{:});
else
    gui_mainfcn(gui_State, varargin{:});
end
% End initialization code - DO NOT EDIT


% --- Executes just before Bismillah is made visible.
function Bismillah_OpeningFcn(hObject, eventdata, handles, varargin)
% This function has no output args, see OutputFcn.
% hObject    handle to figure
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
% varargin   command line arguments to Bismillah (see VARARGIN)

% Choose default command line output for Bismillah
handles.output = hObject;

% Update handles structure
guidata(hObject, handles);

% UIWAIT makes Bismillah wait for user response (see UIRESUME)
% uiwait(handles.figure1);


% --- Outputs from this function are returned to the command line.
function varargout = Bismillah_OutputFcn(hObject, eventdata, handles) 
% varargout  cell array for returning output args (see VARARGOUT);
% hObject    handle to figure
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)

% Get default command line output from handles structure
varargout{1} = handles.output;


% --- Executes on button press in pushbutton1.
function pushbutton1_Callback(hObject, eventdata, handles)
% hObject    handle to pushbutton1 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
[filename,pathname] = uigetfile('*.*');
 
if ~isequal(filename,0)
 
    Img = imread(fullfile(pathname,filename));
    [~,~,m] = size(Img);
    if m == 3
        axes(handles.axes1)
        imshow(Img)
        handles.Img = Img;
        guidata(hObject, handles)
    else
        msgbox('Please insert RGB Image')
    end
else
    return
end

% --- Executes on button press in radiobutton1.
function radiobutton1_Callback(hObject, eventdata, handles)
% hObject    handle to radiobutton1 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)

% Hint: get(hObject,'Value') returns toggle state of radiobutton1
set(handles.radiobutton1,'Value',1)
set(handles.radiobutton2,'Value',0)
set(handles.radiobutton3,'Value',0)
 
Img = handles.Img;
axes(handles.axes1)
cla('reset')
imshow(Img)
 
R = Img(:,:,1);
G = Img(:,:,2);
B = Img(:,:,3);
 
axes(handles.axes2)
cla('reset')
h = histogram(R(:),256);
h.FaceColor = [1 0 0];
h.EdgeColor = 'r';
hold on
 
h = histogram(G(:),256);
h.FaceColor = [0 1 0];
h.EdgeColor = 'g';
 
h = histogram(B(:),256);
h.FaceColor = [0 0 1];
h.EdgeColor = 'b';
grid on
set(gca,'Xlim',[0 255])
hold off
 
% Image Complement
Img_Comp = imcomplement(Img);
 
axes(handles.axes3)
cla('reset')
imshow(Img_Comp)
 
R = Img_Comp(:,:,1);
G = Img_Comp(:,:,2);
B = Img_Comp(:,:,3);
 
axes(handles.axes4)
cla('reset')
h = histogram(R(:),256);
h.FaceColor = [1 0 0];
h.EdgeColor = 'r';
hold on
 
h = histogram(G(:),256);
h.FaceColor = [0 1 0];
h.EdgeColor = 'g';
 
h = histogram(B(:),256);
h.FaceColor = [0 0 1];
h.EdgeColor = 'b';
set(gca,'Xlim',[0 255])
grid on
hold off

% --- Executes on button press in radiobutton2.
function radiobutton2_Callback(hObject, eventdata, handles)
% hObject    handle to radiobutton2 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)

% Hint: get(hObject,'Value') returns toggle state of radiobutton2

set(handles.radiobutton1,'Value',0)
set(handles.radiobutton2,'Value',0)
set(handles.radiobutton3,'Value',1)
 
Img = handles.Img;
Gray = rgb2gray(Img);
bw = im2bw(Gray,graythresh(Gray));
 
axes(handles.axes1)
cla('reset')
imshow(bw)
 
axes(handles.axes2)
h = histogram(double(bw(:)),2);
h.FaceColor = [0 0 0];
h.EdgeColor = [0 0 0];
set(gca,'Xlim',[0 1])
grid on
 
% Image complement
bw_Comp = ~bw;
 
axes(handles.axes3)
cla('reset')
imshow(bw_Comp)
 
axes(handles.axes4)
h = histogram(double(bw_Comp(:)),2);
h.FaceColor = [0 0 0];
h.EdgeColor = [0 0 0];
set(gca,'Xlim',[0 1])
grid on


% --- Executes on button press in radiobutton3.
function radiobutton3_Callback(hObject, eventdata, handles)
% hObject    handle to radiobutton3 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)


% Hint: get(hObject,'Value') returns toggle state of radiobutton3
set(handles.radiobutton1,'Value',0)
set(handles.radiobutton2,'Value',1)
set(handles.radiobutton3,'Value',0)
 
 
Img = handles.Img;
Gray = rgb2gray(Img);
 
 
axes(handles.axes1)
cla('reset')
imshow(Gray)
 
 
axes(handles.axes2)
cla('reset')
h = histogram(Gray(:),256);
h.FaceColor = [0.5 0.5 0.5];
h.EdgeColor = [0.5 0.5 0.5];
set(gca,'Xlim',[0 255])
grid on
 
 
% Image Complement
Gray_Comp = imcomplement(Gray);
axes(handles.axes3)
cla('reset')
imshow(Gray_Comp)


axes(handles.axes4)
cla('reset')
h = histogram(Gray_Comp(:),256);
h.FaceColor = [0.5 0.5 0.5];
h.EdgeColor = [0.5 0.5 0.5];
set(gca,'Xlim',[0 255])
grid on

