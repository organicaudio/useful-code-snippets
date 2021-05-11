# remove black frame from ulauncher

## black Frame

[Open Issue](https://github.com/Ulauncher/Ulauncher/issues/230)

If window effect is disabled there is the chance that there is a black frame around the Ulauncher window. Probably because the compositor ist somehow affected or disabled by the disabling of the window effect in deepin.

In [https://github.com/Ulauncher/Ulauncher/issues/212] someone proposed a workaround which works:

add ‘margin: -20px;’ to the css of a theme. [Documentation on how to create an own Theme](http://docs.ulauncher.io/en/latest/themes/themes.html)

Extended white theme:

```css
.app {
   box-shadow: 0 0 5px @window_shadow;
   background-color: @window_bg;
   border: 1px solid @window_border_color;
   border-radius: 4px;
   margin: -20px; /*override black area when window effect is disabled*/
}
```

```css
Extended dark theme:
.app {
   background-color: @window_bg;
   border-color: @window_border_color;
   margin: -20px; /*override black area when window effect is disabled*/
}
```
