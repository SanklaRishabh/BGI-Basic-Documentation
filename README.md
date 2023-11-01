# BGI-Basic-Documentation

C does not provide methods for creating graphics in its standard library. However, there are some open-source or third-party libraries available to create stunning visuals. This documentation introduces Borland Software Corporation's **BGI** (Borland Graphical Interface) library that was included with the computer installation of Turbo C/C++.

> [!info]
> `graphics.h` and other headers and libraries, maintained by open-source developers for GCC can be downloaded from the internet.

## Graphical Coordinate System

Unlike the usual Cartesian representation of the graph, computers start the plot from the top-left corner of the graphical window, with the X-axis extending towards the right and the Y-axis downwards.

![Comptuter Coordinate System](https://math.hws.edu/graphicsbook/c2/pixel-coordinates.png)
## Graph Functions

### Initializing the Graph

The first step in the path of creating graphics is to initialize the graphical drivers of the computer. The `initgraph` function initializes the graphical system by loading the graphics driver from the disk and putting the system into graphics mode.

```c
void initgraph(int *graphdriver, int *graphmode, char *pathtodriver);
```

- `graphdriver`: The system's graphics drivers stored in the drive. Passing it will load them.
- `graphmode`: Specifies the graphics mode.
- `pathtodriver`: Path to the BGI library. If you are using GCC, you have to find an alternative, like `libbgi.a`.

> [!note]
> To automatically detect the drivers, the `DETECT` macro is used. This detects the driver, sets the graphics to the highest screen resolution possible in `graphmode` and automatically sets `pathtodriver`.

### Closing the Graph

After the work has been done in the graphical mode, it must be closed to deallocate the memory taken up by the graphical system and restore the system back to text-mode. The `closegraph` function is used for this.

```c
void closegraph();
```

### Printing Text

1. `outtext`: This function writes output in the graphical window. The text starts from the top-left corner of the window (origin). It takes up the string to be printed as its argument.
   
```c
void outtext(char *string);
```

> [!note]
> Printing continues from the ending position of the last executed text instance.

2. `outtextxy`: This function writes output in the graphical window at the specified coordinates. It takes **three** arguments, `x`, `y`, `textstring`, where `x` and `y` represent the distance in the respective directions, and `textstring` represents the string to be printed.

```c
void outtextxy(int x, int y, char *textstring);
```

### Drawing Graphics

1. `line`: This function is used to draw a line from a point $(x_1, y_1)$ to a point $(x_2, y_2)$. Here, $(x_1, y_1)$ and $(x_2, y_2)$ are the end-points of the line.

```c
void line(int x1, int y1, int x2, int y2);
```

2. `rectangle`: This function creates a quadrilateral on the graph screen. It takes **four** arguments, `left`, `top`, `right`, `bottom`. `left` specifies how far the left border is from the Y-axis, `top` specifies the distance of the top border from the X-axis, `right` holds the distance of the right border and `bottom` the distance of the bottom border.

```c
void rectangle(int left, int top, int right, int bottom);
```

3. `circle`: This function creates a circle. It takes up **three** arguments, `x`, `y` and `radius`. `x` and `y` represent the coordinates of the center of the circle, and `radius` specifies the radius.

```c
void circle(int x, int y, int radius);
```

4. `arc`: This function is used to create an arc. It takes up **five** arguments, `x`, `y`, `stangle`, `endangle` and `radius`. `x` and `y`, represent coordinates of the center, `stangle` and `endangle` the starting and ending angles, respectively, in degrees, and `radius` takes up the information of the length of the radius.

```c
void arc(int x, int y, int stange, int endangle, int radius);
```

5. `ellipse`: This function creates an ellipse. It takes up **six** arguments, `x`, `y`, `stangle`, `endangle`, `xradius` and `yradius`. `x` and `y` represent the coordinates of the center, `stangle` and `endangle` the starting and ending angles, respectively, `xradius` the radius of the ellipse in the X-direction and `yradius` the radius of the ellipse in the Y-direction.

```c
void ellipse(int x, int y, int stangle, int endangle, int xradius, int yradius);
```

> [!note]
> The `ellipse` function can also be used to create circles.

6. `fillellipse`: This function creates an ellipse with a color-fill. It takes up **four** arguments, `x`, `y`, `xradius` and `yradius`. There are **no angle parameters** in this function.

```c
void fillellipse(int x, int y, int xradius, int yradius);
```

> [!note]
> Since the graphical window is black by default, the automatic color-fill is its inverse, i. e., white. It can be changed, though.

7. `bar`: This function creates a 2-dimensional bar (filled-rectangle). It takes up **four** arguments, same as the arguments for creating a rectangle, `left`, `top`, `right`, `bottom`.

```c
void bar(int left, int right, int top, int bottom);
```

8. `bar3d`: This function creates a 3-dimensional bar. It takes up **six** arguments, `left`, `top`, `right`, `bottom`, `depth` and `topflag`. The first four are the same for creating a rectangle, `depth` represents the extension of the 3-D object in the Z-axis, while `topflag` represents whether the top of the 3-D bar is present or not.

```c
void bar3d(int left, int top, int right, int bottom, int depth, int topflag);
```

> [!note]
> Any non-zero, positive value for the `topflag` marks the presence of a top.

9. `drawpoly`: This function creates any polygon of $n$ number of points. It takes up **two** arguments, `num`, and `polypoints`. `num` represents the $n + 1$ number of points, with the $(n + 1)^{th}$ point having the same coordinates as the first point. The other argument `polypoints` represents a pointer to an array of coordinates to all the points stored as $\{x_1, y_1, x_2, y_2, ... x_{n + 1}, y_{n + 1}\}$.

```c
void drawpoly(int num, int *polypoints);
```

> [!note]
> The values of $(x_1, y_1)$ and $(x_{n + 1}, y_{n + 1})$ must be same to close the polygon.

10. `fillpoly`: This function creates a filled-polygon. It takes up **two** arguments, same as the arguments for creating a polygon.

```c
void fillpoly(int num, int *polypoints);
```

### Colors

BGI works with 4-bit color system. 

| COLOR | INT VALUE | COLOR | INT VALUE |
| ----- | --------- | ----- | --------- |
| BLACK | 0 | DARKGRAY | 8 |
| BLUE | 1 | LIGHTBLUE | 9 |
| GREEN | 2 | LIGHTGREEN | 10 |
| CYAN | 3 | LIGHTCYAN | 11 |
| RED | 4 | LIGHTRED | 12 |
| MAGENTA | 5 | LIGHTMAGENTA | 13 |
| BROWN | 6 | YELLOW | 14 |
| LIGHTGRAY | 7 | WHITE | 15 |

1. `setcolor`: This function is used to change the current drawing color. The color which is to be set, is passed as the argument. It only sets the stroke color and not the fill color.

```c
void setcolor(int color);
```

2. `setbkcolor`: This function is used to change the current background color. The default is BLACK.

```c
void setbkcolor(int color);
```

3. `getcolor`: This function returns the current-set drawing color. The return type is integer, representing the color.

```c
int getcolor();
```

4. `getbkcolor`: This function returns the current-set background color.

```c
int getbkcolor();
```

5. `getmaxcolor`: Returns the maximum color value for the current color-set in graphics mode. For BGI, the maximum value is 15.

```c
int getmaxcolor();
```

6. `cleardevice`: Clears the screen in the graphics mode and sets the position back to $(0, 0)$. It is similar to the `clrscr` function used in text-mode. Clearing the screen fills it with current-set background color.

```c
void cleardevice();
```

### Coordinates

1. `getx`: This function returns the X-coordinate of the current graphical cursor position.

```c
int getx();
```

2. `gety`: This function returns the Y-coordinate of the current graphical cursor position.

```c
int gety();
```

3. `getmaxx()`: This function returns the maximum X-coordinate of the current graphical mode.

```c
int getmaxx();
```

4. `getmaxy()`: This function returns the maximum Y-coordinate of the current graphical mode.

```c
int getmaxy();
```

### Text

The original BGI library is compatible with 11 types of fonts in graphical mode:

| FONT NAME | INT VALUE | FONT NAME | INT VALUE | FONT NAME | INT VALUE |
| --------- | ----- | --------- | ----- | --------- | ----- |
| DEFAULT_FONT | 0 | SCRIPT_FONT | 5 | BOLD_FONT | 10 |
| TRIPLEX_FONT | 1 | SIMPLEX_FONT | 6 |
| SMALL_FONT | 2 | TRIPLEX_SCR_FONT | 7 |
| SANS_SERIF_FONT | 3 | COMPLEX_FONT | 8 |
| GOTHIC_FONT | 4 | EUROPEAN_FONT | 9 |

> [!info]
> The font styles may not work in newer editions of some popular operating systems, as well as in the BGI libraries maintained by open-source developers for extended support.

1. `settextstyle`: This function sets the text size, direction and font style. It takes up three arguments, `font`, `direction`, and `charsize`. `font` represents the font styles supported by BGI, `direction` represents the flow of the text— `HORIZ_DIR` is horizontal (left-to-right) and `VERT_DIR` is vertical (top-to-bottom), `charsize` represents the character size.

```c
void settextstyle(int font, int direction, int charsize);
```

