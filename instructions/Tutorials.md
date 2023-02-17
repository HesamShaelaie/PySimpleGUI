# Structure of the code







# Example 1 - Simplest window


```python
import PySimpleGUI as sg
sg.Window(title="Hello World", layout= [[]], margins= (100,50)).read ()
```
Result:

![](/Images/T1.png)



# Example 2 - Window with button

```python
import PySimpleGUI as sg

layout = [
            [sg. Text ("Hello from PySimpleGUI")],
            [sg.Button ("OK" )]
         ]


window = sg.Window("Demo", layout, keep_on_top=True)

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

# Example 3 - Simple print

```python
import PySimpleGUI as sg

sg.main()


layout = [[sg.Button('Hello World\n(click me)', size=(10,2))],
          [sg.Button('QUIT', button_color=('red',None))]]

window = sg.Window('', layout, element_justification='center')

while True:
    event, values = window.read()
    if event in (sg.WIN_CLOSED, 'QUIT'):
        break
    if event == 'Hello World\n(click me)':
        print("hi there, everyone!")

window.close()
```

# Example 4 - Windows keys

```python
import PySimpleGUI as sg


layout = [[sg.Text('This is a text element')],
          [sg.Input(key='-IN1-')],
          [sg.Input(key='-IN2-')],
          [sg.Button('Ok', key='-OK-'), sg.Button('Exit')]]

window = sg.Window('Title', layout)

while True:
    event, values = window.read()
    print(event, values)
    if event in (sg.WIN_CLOSED, 'Exit'):
        break
    
    window['-IN1-'].update('new value')
    #window.find_element('-IN1-').update('new value')

window.close()
```

or you can do this


```python
import PySimpleGUI as sg

input1 = sg.Input(key='-IN1-')

layout = [[sg.Text('This is a text element')],
          [input1],
          [sg.Input(key='-IN2-')],
          [sg.Button('Ok', key='-OK-'), sg.Button('Exit')]]

window = sg.Window('Title', layout)

while True:
    event, values = window.read()
    print(event, values)
    if event in (sg.WIN_CLOSED, 'Exit'):
        break
    input1.update('new value')

window.close()
```

# Example 5 - themes

```python
sg.theme('Dark Grey 13')

new_theme = {'BACKGROUND': '#32414B',
                 'TEXT': '#ffffff',
                 'INPUT': '#32414B',
                 'TEXT_INPUT': '#ffffff',
                 'SCROLL': '#505F69',
                 'BUTTON': ('#ffffff', '#32414B'),
                 'PROGRESS': ('#505F69', '#32414B'),
                 'BORDER': 4, 'SLIDER_DEPTH': 0, 'PROGRESS_DEPTH': 0,
                 }

sg.theme_add_new('Your New Theme', new_theme)
sg.theme('Your New Theme')

```
in an example:

```python

import PySimpleGUI as sg

def make_window():
    layout = [[sg.Text('My Window')],
              [sg.Input(key='-IN-')],
              [sg.Text(size=(30, 1), key='-OUT-')],
              [sg.Button('Go'), sg.Button('Exit')]]

    window = sg.Window('Window Title', layout, keep_on_top=True)
    return window

def main():
    sg.set_options(font='Default 18')

    new_theme = {'BACKGROUND': '#32414B',
                 'TEXT': '#ffffff',
                 'INPUT': '#32414B',
                 'TEXT_INPUT': '#ffffff',
                 'SCROLL': '#505F69',
                 'BUTTON': ('#ffffff', '#32414B'),
                 'PROGRESS': ('#505F69', '#32414B'),
                 'BORDER': 4, 'SLIDER_DEPTH': 0, 'PROGRESS_DEPTH': 0,
                 }

    sg.theme_add_new('Your New Theme', new_theme)

    sg.theme('Your New Theme')
    # sg.theme_background_color('#FF0000')
    # sg.popup(sg.theme_background_color())

    window = make_window()



    while True:             # Event Loop
        event, values = window.read()
        print(event, values)
        if event == sg.WIN_CLOSED or event == 'Exit':
            break

        if event == 'Go':
            sg.theme('Dark Grey 13')
            window.close()
            window = make_window()
        else:
            window['-OUT-'].update(f'You clicked {event}')

    window.close()


if __name__ == '__main__':
    main()


```

# Example 6 - Common Parameters


```python

import PySimpleGUI as sg
sg.theme('dark red')
# sg.set_options(font='Helvetica 18')

def main():
    right_click_menu = ['Unused', ['Right', '!&Click', '&Menu', 'E&xit', 'Properties::KEY']]
    font1 = 'Courier 18'
    font2 = 'Courier 18 underline italic'
    font3 = ('Courier', 18)
    font4 = ('Courier', 18, 'underline italic bold overstrike')

    layout = [
              [sg.Text('Test of fonts', font=font1)],
              [sg.Text('Test of fonts', font=font2)],
              [sg.Text('Test of fonts', font=font3)],
              [sg.Text('Test of fonts', font=font4)],
              [sg.Text('Padding', pad=(0,0)), sg.Text('Padding', pad=(0,0))],
              [sg.Text('Padding'), sg.Text('Padding')],
              [sg.Text('Padding', pad=((5,50), (10,20))), sg.Text('Padding')],
              [sg.Text('Invisible', visible=False), sg.Text('Visible', visible=True)],
              [sg.Text('Right Click Me', right_click_menu=right_click_menu)],
              [sg.Text('Left Click Me', enable_events=True, key='-TEXT-')],
              [sg.Text('Color Parms', background_color='white', text_color='#FF0000')],
              [sg.Text('Metadata', metadata='MY METADATA', key='-META-', tooltip='has metadata')],
              [sg.Input(key='-IN-')],
              [sg.Text(size=(40, 1), key='-OUT-',  font='Courier 18')],
              [sg.Button('Go'), sg.Button('Exit')]]

    window = sg.Window('Window Title', layout, font='Helvetica 18')

    while True:             # Event Loop
        event, values = window.read()
        print(event, values)
        if event == sg.WIN_CLOSED or event == 'Exit':
            break

        window['-OUT-'].update(f'Event={event}')
        print(window['-META-'].metadata)

    window.close()

if __name__ == '__main__':
    main()

 
```

# Example 7 - Common Methods and Properties

```python
import PySimpleGUI as sg



def main():
    txt = sg.Text('An element to update', k='-TXT-')

    layout = [
              [txt],
              [sg.Input(key='-IN1-', tooltip='Initial tooltip')],
              [sg.Input(key='-IN2-', size=(10,1))],
              [sg.Multiline(size=(40,10), k='-ML-')],
              [sg.Text(size=(30, 1), key='-OUT-')],
              [sg.Text(size=(40, 1), key='-VALUES-')],
              [sg.Button('Go'), sg.B('Scroll'), sg.B('Focus2'),sg.B('Expand2'), sg.B('Size'), sg.B('Tooltip'), sg.Button('Exit')],
              ]

    window = sg.Window('Window Title', layout, keep_on_top=True, font='Default 16', finalize=True, resizable=True)


    while True:             # Event Loop
        event, values = window.read()
        print(event, values)

        if event == sg.WIN_CLOSED or event == 'Exit':
            break
        if event == 'Focus2':
            window['-IN2-'].set_focus()
        if event == 'Expand2':
            window['-ML-'].expand(True, True)
        if event == 'Size':
            window['-IN2-'].set_size((30,None))
            window.refresh()
            print(f"size = {window['-IN2-'].get_size()}")
        if event == 'Tooltip':
            window['-IN1-'].set_tooltip('New tooltip')
        if event == 'Scroll':
            window['-ML-'].set_vscroll_position(.5)

        window['-OUT-'].update(f'EVENT: {event}')
        window['-VALUES-'].update(f'VALUES: {values}')

    window.close()


if __name__ == '__main__':
    main()
```
# Example 8 - Auto generate layout

```python

import PySimpleGUI as sg

example_number = 1

sg.set_options(font='Default 16', keep_on_top=True)


#========================== 1 - EXAMPLE - for loop  ==========================

def main_example1():

    row = []
    for i in range(4):
        row.append(sg.Button(i))

    layout = [row]

    window = sg.Window('Generated Layouts 1', layout)


    while True:
        event, values = window.read()
        if event in (sg.WIN_CLOSED, 'Cancel'):
            break

    window.close()




# ========================== 2 - EXAMPLE - List Comprehension  ==========================

def main_example2():


    window = sg.Window('Generated Layouts 2', [[sg.Button(i) for i in range(4)]])

    while True:
        event, values = window.read()
        if event in (sg.WIN_CLOSED, 'Cancel'):
            break

    window.close()


# ========================== 3 - EXAMPLE - List Comprehension  ==========================

def main_example3():

    layout = [[sg.Button(i)] for i in range(4)]

    window = sg.Window('Generated Layouts 3', layout)

    while True:
        event, values = window.read()
        if event in (sg.WIN_CLOSED, 'Cancel'):
            break

    window.close()




# ========================== 4 - EXAMPLE - List Comprehension - dual  ==========================

def main_example4():

    layout = [[sg.Button(f'row {row} col {col}') for col in range(4)] for row in range(5)]

    window = sg.Window('Generated Layouts 4', layout)

    while True:
        event, values = window.read()
        if event in (sg.WIN_CLOSED, 'Cancel'):
            break

    window.close()




# ========================== 5 - EXAMPLE - Addition of lists - one a row ==========================

def main_example5():
        # [a] + [b] = [a,b]
    layout = [[sg.Text('Row 1') for i in range(5)] + [sg.Text('Also row 1')]]

    window = sg.Window('Generated Layouts 5', layout)

    while True:
        event, values = window.read()
        if event in (sg.WIN_CLOSED, 'Cancel'):
            break

    window.close()



# ========================== 6 - EXAMPLE - Addition of layouts  ==========================

def main_example6():


    use_ok = True

    layout = [[sg.Text('My Group of Elements')],
              [sg.In(size=25)]]

    if use_ok:
        layout += [ [sg.In()],
                    [sg.Button('Ok'), sg.Button('Cancel')]]
    else:
        layout += [[sg.Button('Go'), sg.Button('Exit')]]



    window = sg.Window('Generated Layouts 6', layout)

    while True:
        event, values = window.read()
        if event in (sg.WIN_CLOSED, 'Cancel', 'Exit'):
            break

    window.close()


# ========================== 7 - EXAMPLE - Extending existing layouts  ==========================

def main_example7():


    layout = [[sg.Text('My Group of Elements')],
              [sg.In(size=25)],
              [sg.Frame('Frame', [[]], key='-COL-')],
              [sg.Button('Go'), sg.Button('Exit')]]

    window = sg.Window('Generated Layouts 7', layout)

    while True:
        event, values = window.read()
        if event in (sg.WIN_CLOSED, 'Cancel', 'Exit'):
            break
        if event == 'Go':
            window.extend_layout(window['-COL-'], [[sg.Text('My New Row1!')],
                                                   [sg.Text('My New Row2!')]])
    window.close()



#========================== 0 - Intro (element only)  ==========================

def main_intro():

    layout = [[sg.Text('Layout Generation')],
              [sg.Text('Using Code to Make (and extend) Layouts', enable_events=True)]]

    sg.Window('Element Justification & Alignment', layout, no_titlebar=True, element_justification='c', font='_ 22').read(close=True)





if __name__ == '__main__':
    examples = [main_intro, main_example1, main_example2, main_example3, main_example4, main_example5, main_example6, main_example7 ]
    # for func in examples:
    #     func()
    examples[example_number]()
```