# Messages & Events in GUI

<span style="font-size:18px ; font-weight: bold;">Lunar, like windows, sends messages when something interesting happenes to programs</span>
<span style="font-size:18px ; font-weight: bold;">EVERY functional GUI program needs to have this function implemented:</span>

```c
int WINEVENT(){
    // Events
}
```

<span style="font-size:18px ; font-weight: bold;">You may ask, how tf do i get the messages and do fun stuff with them. Only 1 function is needed</span>

```c
int TranslateMsg(
    // no inputs
    // we get the message
);
```
<span style="font-size:18px ; font-weight: bold;">How to check if user presses LMB?</span>

```c
int WINEVENT(){
    int msg;
    msg = TranslateMsg(); // we get the message

    if(msg == 0x0010){ // 0x0010 > LMB || 0x0011 > MMB || 0x0012 > RMB
        printf("LMB pressed\n");
    }
    return 0;
}
```

<span style="font-size:18px ; font-weight: bold;">Not very fun, is it? Another function we can use from the LAPI is GetClickedWidgetID</span>

```c
int GetClickedWidgetID(){
    // no inputs
    // we get the widget id when user clicks on it, if no widget is being clicked on, we get -1 (IMPORTANT)
}
```

```c
int WINEVENT(){
    int msg;
    int widgetid;
    widgetid = GetClickedWidgetID(); // we get the widget id
    msg = TranslateMsg(); // we get the message


    if(widgetid == 0){ // widget 0 is our button lets say
        // Textout(...);
    }
    if(widgetid != -1){
        // any widget clicked
    }
    return 0;
}
```

<div style="
    background-color:#004173;
    border-left: 5px solid #0066cc;
    color: #ffffff;
    border-radius: 12px;
    padding: 16px;
    margin: 16px 0;
    box-shadow: 0 2px 8px rgba(255, 255, 255, 0.1);
">
<span style="font-size:22px ; font-weight: bold;">🔷 IMPORTANT</span>

<span style="font-size:18px ; font-weight: bold;">Below is the table of some useful messages you can use in Lunar while developing your program</span>
</div>

| Hex  | Name          | Information                                                           |
| ---- | ------------- | --------------------------------------------------------------------- |
| 0000 | WIN_CREATE    | sent when window has finished creation                                |
| 0001 | WIN_CLOSE     | sent right when close button is clicked, before destroying the window |
| 0002 | WIN_DESTROY   | sent right after window is destroyed from the screen                  |
| 0003 | WIN_ONFOCUS   | sent when window is focused                                           |
| 0004 | WIN_LFOCUS    | sent when window looses focus                                         |
| 0005 | WIN_MOVE      | sent when window is moved                                             |
| 0006 | WIN_MAXIMIZE  | sent when window is maximized, on supported programs                  |
| 0007 | WIN_RESTORE   | sent when window is restored from being in a maximized state          |
| 0008 | WIN_NOTIFGET  | sent after program sends a notification to the user                   |
| 000a | WIN_POWER     | sent before trying to shut down the PC [WIP]                          |
| 000b | WIN_PAINT     | sent when window needs to be redrawn                                  |
| 000c | WIN_KEYDOWN   | sent when a key is pressed while the window has focus                 |
| 000d | WIN_KEYUP     | sent when a key is released while the window has focus                |
| 000e | WIN_WIDGETF   | sent when user clicks on a widget, we dont know whicn one tho         |
| 000f | MOUSE_MOVE    | sent when mouse is being moved (used to draw the cursor)              |
| 0010 | MOUSE_LMBDOWN | sent when user presses LMB                                            |
| 0011 | MOUSE_MMBDOWN | sent when user presses MMB                                            |
| 0012 | MOUSE_RMBDOWN | sent when user presses RMB                                            |

<span style="font-size:35px ; font-weight: bold;">.</span>
<br>
<span style="font-size:35px ; font-weight: bold;">.</span>
<br>
<span style="font-size:35px ; font-weight: bold;">.</span>