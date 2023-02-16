# PySimpleGUI

## How to install PySimpleGUI

For installing the package in mac, you can simple open the terminal and write

```bash
pip install pysimplegui
```

for Pycharm you can follow the following steps:

* Settings ...
* Project Interpreter
* Click on + for installing the package
* Search for the PySimpleGUI
* Click install

![](/Images/install-v1.png)
![](/Images/install-v2.png)


Now you need to check if the package is installed properly. For this, you need to check copy and paste the following code inside your project and run it. A simpler solution is to just run the file _**test.py**_. 

```python
import PySimpleGUI as sg

sg.theme('LightBrown')   # Add a touch of color
# All the stuff inside your window.
layout = [  [sg.Text('Some text on Row 1')],
            [sg.Text('Enter something on Row 2'), sg.InputText()],
            [sg.Button('Ok'), sg.Button('Cancel')] ]

# Create the Window
window = sg.Window('Window Title', layout)
# Event Loop to process "events" and get the "values" of the inputs
while True:
    event, values = window.read()
    if event == sg.WIN_CLOSED or event == 'Cancel': # if user closes window or clicks cancel
        break
    print('You entered ', values[0])

window.close()
```

The result should be like 

![](/Images/err-v0.png)

if you see the following image or you getting the the following warnings, you need to install the latest python. 

![](/Images/err-v1.png)

Warnings:
```matlab
"/Users/hesam/Documents/TA class/PySimpleGUI/venvsimplgui/bin/python" "/Users/hesam/Documents/TA class/PySimpleGUI/main.py"
/Users/hesam/Documents/TA class/PySimpleGUI/venvsimplgui/lib/python3.9/site-packages/PySimpleGUI/PySimpleGUI.py:24845: UserWarning: You are running a VERY old version of tkinter 8.5.9. You cannot use PNG formatted images for example.  Please upgrade to 8.6.x
  warnings.warn('You are running a VERY old version of tkinter {}. You cannot use PNG formatted images for example.  Please upgrade to 8.6.x'.format(tclversion_detailed), UserWarning)
Mac OS Version is 13.1 and patch enabled so applying the patch
Applyting Mac OS 12.3+ Alpha Channel fix.  Your default Alpha Channel is now 0.99
```

## Installing latest of Python

At the time of writing this instruction, the latest version of Python is 3.11.2. You need to download it from [here](https://www.python.org/downloads/). After you installed the Python you need to run the following steps:

* Settings ...
* Project Interpreter
* Add Project Interpreter
* Virtualenv Environment
* New environment
* Set the location and name for your virtual env
* Base interpreter -> search for the path 

```
/Library/Frameworks/Python.framework/Versions/3.11/bin/python3
```
* install the following packages
    
  * pysimplegui
  * matplot
  * matplotlib
  * numpy
  * panda

# Start creating simple GUI



