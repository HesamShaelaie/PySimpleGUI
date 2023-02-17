# Help documentation
Simply you can add the following command to your code and you will have access to all instructions and documentation of the PySimpleGUI.

```python
import PySimpleGUI as sg
sg.main_sdk_help()
```
and the result

![](/Images/Help.png)


# Structure of the code

```python
# 1 - Import

# 2 - Layout

# 3 - Window

# 4 - Event loop / handling

# 5 - Close
```


# Example 1 - Simplest window
```python
# 1 - Import
import PySimpleGUI as sg

# 2 - Layout
layout = [
            [sg.Text('Hello, World!')],
            [sg.Button('Ok')],
         ]

# 3 - Window
window = sg.Window('Title', layout)

# 4 - Event loop / handling
event, values = window.read()

# 5 - Close
window.close()
```

# Example 1.1 - Simplest window

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

# Example 2.1 - Window with button

```python

import PySimpleGUI as sg

layout = [[sg.Text('This is just a window')],
          [sg.Button('1'), sg.Button('2'), sg.Button('Exit')]]

window = sg.Window('Title', layout)

while True:
    event, values = window.read()
    
    if event == sg.WIN_CLOSED or event == 'Exit':
        break
    if event == '1':
        print('You clicked 1')
    elif event == '2':
        print('You clicked 2')

window.close()

```



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

layout = [[sg.Text('This is a simple text element')],
          [sg.Input(key='-X1-')],
          [sg.Input(key='-X2-')],
          [sg.Button('Ok', key='-OK-'), sg.Button('Exit')]]

window = sg.Window('Title', layout)

while True:
    
    event, values = window.read()
    print(event, values)
    
    if event in (sg.WIN_CLOSED, 'Exit'):
        break

    window['-X1-'].update('new value')


window.close()
```

or you can do this


```python
import PySimpleGUI as sg

Inpt = sg.Input(key='-IN1-')

layout = [[sg.Text('This is a text element')],
          [Inpt],
          [sg.Input(key='-IN2-')],
          [sg.Button('Ok', key='-OK-'), sg.Button('Exit')]]

window = sg.Window('Title', layout)


cnt = 1
while True:
    event, values = window.read()
    print(event, values)
    if event in (sg.WIN_CLOSED, 'Exit'):
        break
    cnt +=1
    Inpt.update('new value   ' + str(cnt))

window.close()
```

# Example 5 - themes

```python
import PySimpleGUI as sg

sg.theme('Dark Grey 10')

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

Let's try it

```python

import PySimpleGUI as sg

def make_window():
    layout = [[sg.Text('My Window')],
              [sg.Input(key='-IN-')],
              [sg.Text(size=(30, 1), key='-OUT-')],
              [sg.Button('Theme change'), sg.Button('Exit')]]

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

        if event == 'Theme change':
            sg.theme('Dark Grey 10')
            window.close()
            window = make_window()
        else:
            window['-OUT-'].update(f'You clicked {event}')

    window.close()


if __name__ == '__main__':
    main()


```


# Example 5.5 - Answer to Question one

The example comes from the PySimpleGUI youtube channel. You can see it video with this [link](https://www.youtube.com/watch?v=KUW6khTdoC0&list=PLl8dD0doyrvFfzzniWS7FXrZefWWExJ2e&index=14&ab_channel=PySimpleGUI).

```python
import PySimpleGUI as sg
sg. theme ('Light Green')
# sg.set_options(font='Helvetica 18')

def main():


    #- Menu Definition - - - #
    menu_def=   [
                    ['&File', ['&Open Ctrl-0', '&Save Ctri-S', '&Properties', '!Disabled', 'Exit']],
                    ['&Edit', ['Special', 'Normal' , ['Normall', 'Normal2'], 'Undo'],],
                    ['&Toolbar', ['---', 'Command &1::Command_Key', 'Command &2', '---' , 'Command &3', 'Command &4']],
                    ['&Help', ['&About...']],
                ]

    right_click_menu = ['Unused', ['Right', '!&Click', '&Menu', 'E&xit', 'Properties::KEY']]
    input_right_click = ['Unused', ['Special', 'Normal', ['Normal1', 'Normal2'], 'Undo']]

    # ------- GUI Defintion ------ #
    layout= [  
                [sg.Menu(menu_def, tearoff=True, key='-MENU BAR-')],
                [sg.Text('Right click me for a right click menu example')],
                [sg.Output(size= (60, 20), key='-OUT-')],
                [sg.In(right_click_menu=input_right_click)],
                [sg.ButtonMenu ('ButtonMenu', right_click_menu, key='-BMENU-'), sg. Button ('Plain Button')],
            ]

    window = sg.Window ("Windows-like program", layout, keep_on_top=True, right_click_menu=right_click_menu)

    # Event Loop
    while True:
        event, values = window.read()
        print(event, values)
        if event == sg.WIN_CLOSED or event == 'Exit':
            break

        window['-OUT-'].update(f'Event={event} and value={values}')

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
    # & is for the underline and for the shortcut
    # --- is a seperator 


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


# Example 9 - Elements

## Listbox
```python
import PySimpleGUI as sg
import os


sg.Print('', font='Default 18', keep_on_top=True, size=(50,10), location=(1650,100))

sg.set_options(font='Default 18')

def main_listbox():
    sg.theme_text_color('yellow')

    color_names = ('red', 'green', 'blue', 'yellow', 'blue', 'blue green', 'sky blue', 'navy blue')
    mixed_list = (1,2,3, 3.1415, sg.Text(), 'yellow + orange = amber')

    layout = [
            [sg.T('SINGLE (default)'+' '*35), sg.T('MULTIPLE'+' '*40), sg.T('BROWSE'+' '*15), sg.T('EXTENDED (best for multiple)')],
            [sg.Listbox(color_names, size=(25,7), select_mode=sg.SELECT_MODE_SINGLE,  enable_events=True, k='-LBOX1-'),
             sg.Listbox(mixed_list, size=(25,7), select_mode=sg.SELECT_MODE_MULTIPLE,  enable_events=True, k='-LBOX2-'),
             sg.Listbox(mixed_list, size=(25,7), select_mode=sg.SELECT_MODE_BROWSE,  enable_events=True, k='-LBOX3-'),
             sg.Listbox(mixed_list, size=(25,7), select_mode=sg.SELECT_MODE_EXTENDED, no_scrollbar=True,  enable_events=True, k='-LBOX4-')],
            [sg.B('Go'), sg.B('Change'), sg.B('Exit')],
             ]

    window = sg.Window("Listbox", layout, keep_on_top=True)

    while True:
        event, values = window.read()
        if event in (sg.WIN_CLOSED, 'Exit'):
            break

        sg.Print(f'event = {event}', c='white on red', erase_all=True)
        sg.Print(*[f'   {k} = {values[k]}' for k in values], sep='\n')

        if event == 'Change':
            window['-LBOX1-'].update(values=mixed_list)
        elif event == 'Go':
            sg.Print(window['-LBOX2-'].get_indexes())
            window['-LBOX3-'].set_value((2,3,3.1415))



    window.close()


if __name__ == '__main__':
    main_listbox()

```


## Drawing Image

```python
import PySimpleGUI as sg

def main_example():
    sg.Print(font='Default 18', keep_on_top=True, size=(30, 14), relative_location=(600, -300))

    image = r'Images/Help.png'

    graph = sg.Graph((600, 600), (0,0), (600,600), drag_submits=True, enable_events=True, k='-GRAPH-')

    layout = [[graph],
              [sg.Button('Draw')]]

    window = sg.Window('Graph Element - Example 2', layout)

    image_fig = None
    while True:
        event, values = window.read()
        if event in (sg.WIN_CLOSED, 'Exit'):
            break
        if event == 'Draw':
            
            image_fig = graph.draw_image(filename=image, location=(0, 600))
            
        elif event == '-GRAPH-':
            graph.relocate_figure(image_fig, values[event][0], values[event][1])


        sg.Print(f'event = {event}', c='white on red', erase_all=True)
        sg.Print(*[f'   {k} = {values[k]}' for k in values], sep='\n')

    window.close()


if __name__ == '__main__':
    
   main_example()
```