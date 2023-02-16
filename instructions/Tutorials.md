# Simplest window

```python
import PySimpleGUI as sg
sg.Window(title="Hello World", layout= [[]], margins= (100,50)).read ()
```
Result:

![](/Images/T1.png)



# Window with button

```python
layout = [
            [sg. Text ("Hello from PySimpleGUI")],
            [sg.Button ("OK" )]
         ]

window = sg.Window("Demo", layout)

while True:
    event, values = window.read()
    # End program if user closes window or
    # presses the OK button
    if event == "OK" or event == sg. WIN_CLOSED:
        break

window.close()
```

Result:

![](/Images/T2.png)