### Command-line plotting tool
**pyplot** is a command-line plotting tool written in python. It uses matplotlib and pandas to create line plots from tabular data. The source of the data can either be text data files or tables from a database. In particular, it creates a tabular or grid-like view of plots for *similar* data files/tables. This is primarily meant to quickly *view* data on the fly.

### How to use it with datafiles
A typical instance of the command will look like this,

```
pauls:~$ pyplot file1 file2 cols M option1 option2 option3
```

where, `file1` and `file2` are the data files. We can have any number of data files, provided all the files have same number of columns. Also, use of wildcards in datafile names is permitted. A typical data file should have the following format:

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

The list of data files *must* be followed by the keyword `cols M`, where `cols` marks the end of the list of data files, and `M` is the number of columns in any data file ( it has to be the same `M` for all files). For the above example file, `M=4`.

There can be several plot options, and they are implemented from left to right, i.e., in the order of their appearance in the command-line. They are broadly of two types.

###### *Type 1*

Options that are inbuilt or provided by the program, that can be used in the command-line in any order, and they are:

* `absy`  -- plots abs(*Y*) vs *X*
* `absx`  -- plots *Y* vs abs(*X*)
* `absxy` -- plots abs(*Y*) vs abs(*X*)
* `logy`  -- plots abs(*Y*) vs *X* with log-scale for *Y*
* `logx`  -- plots *Y* vs abs(*X*) with log-scale for *X*
* `logxy` -- plots abs(*Y*) vs abs(*X*) with log-log scale.

The option for log-scaling is slightly different, in that it takes the abs(*Y*) or abs(*X*) after all other plot options have been implemented.

###### *Type 2*

Options that are provided by the user to perform certain arithmetic operations on the data before plotting. These user-defined options should conform to the following form:
* `a+b*r**c` or `a+b*r^c`
* `a+b*r*c`
* `a+b*r+c`

where, `a,b,c` are `+/-`floats, and `r = x,y,xy`. If any of `a,b,c = 0`, we can drop these terms from the expression. For example, shortened expressions like `x+30.0`, `2*y`, etc. are valid expressions. No white-space is allowed inside expressions. We can have any number of user-defined expressions, and they will be implemented from left to right. So, `y+30 absy` is not similar to `absy y+30`!

**pyplot** plots these data files in a *2XN* grid, and labels the *x* axis as *X* and all the *Y* columns as *Y0*, *Y1*, *Y2*, etc as a plot legend. Also, each plot is titled according to the name of the datafile, provided the file-name has an extension, i.e., names like `/PATHTO/datafile_123-check.dat`. In this instance, the plot title will be `datafile_123-check.dat`. In case the file-name does not conform to this standard, the plots are titled 
as *datafile 1*, *datafile 2*, etc, in the order of their appearance in the command-ine.

The plot appears as a *pdf* file, and is automatically opened using *evince*. After the plot window is closed, the plotted *pdf* file is automatically deleted! 

### How to use it with tables from a database
A typical instance of the command will look like this,

```
pauls:~$ pyplot db host user database table1 table2 use option1 option2 option3
```

where, `table1` and `table2` are the tables from the same database. We can have any number of tables, provided all the tables have numeric columns in the form of *X*, *Y0*, *Y1*, *Y2*, etc. They need not have same number of columns (a constraint we have in the datafile case). 

In the absence of plot options, the keyword *use* can be omitted. The plot options are exactly similar to that of the datafile case, and they are implemented in the order of their appearance in the command-line.

Once these details are entered, there will be a password prompt for connecting to the database. Following a successful connection, an evince plot window will appear!


