### Command-line plotting tool
**pyplot** is a command-line plotting tool written in python. It uses matplotlib and pandas to create line plots from data files. In particular, it creates a grid of plots for *similar* data files. This is primarily meant to quickly *view* data files on the fly.

### How to use it
A typical instance of the command will look like this,

```
pauls:~$ pyplot file1 file2 cols M option1 option2
```

where, `file1` and `file2` are the data files. We can have any number of data files, provided all the files have same number of columns. A typical data file should have the following format:

```
# comment 1
# comment 2
# comment 3
#  X     Y0     Y1    Y2
   1.0   1.2   3.2   4.3
   2.0   1.8   2.3   5.4
   3.0   1.6   4.2   4.4
```

This file has 4 columns, one *X* and 3 *Y* columns. The file can have comments, where the comment lines must start with `#`. **pyplot** plots *Y0*, *Y1*, *Y2* vs *X* as a line plot. In this case, all the files should have 4 columns. 

The list of data files *must* be followed by the keyword `cols M`, where `cols` marks the end of the list of data files, and `M` is the number of columns in any data file ( it has to be `M` for all files). For the above example file, `M=4`.

Lastly, we have several plot options. Currently, we have the following options:

1. `absy`  -- plots abs(*Y*) vs *X*
2. `absx`  -- plots *Y* vs abs(*X*)
3. `absxy` -- plots abs(*Y*) vs abs(*X*)
4. `logy`  -- plots abs(*Y*) vs *X* with log-scale for *Y*
5. `logx`  -- plots *Y* vs abs(*X*) with log-scale for *X*
6. `logxy` -- plots abs(*Y*) vs abs(*X*) with log-log scale

*We will soon add a more general option, that will transform the X or Y values according to the user defined arithmetic expression.*

**pyplot** plots these data files in a *2XN* grid, and labels the *x* axis as *X* and all the *Y* columns as *Y0*, *Y1*, *Y2*, etc as a plot legend. Also, each plot is titled as *datafile1*, *datafile2*, etc, in the order of their appearance in the command-ine.

The plot appears as a *pdf* file, opened using *evince*. After the plot window is closed, the plot *pdf* file is automatically deleted. 