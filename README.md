# xls2xlsx
This script provides a quick way to turn a set of .xls files into .xslx files (the originals are preserved).

## Documentation

### Introduction
This script will convert every xls file in a given input directory to a xlsx file in a given output directory, and it works on both Mac and Windows. If there are folders within the input directory, those folders will be made in the output directory and filled with the corresponding xlsx files. This script (as-is) will not read or copy non-xls files. Although there are comments in the code, I figured a document with a tutorial and warnings would be better. In this document, "terminal window" (for Mac) will mean "command prompt" for Windows.

### Libraries
The libraries this script uses are listed below, as well as the download instructions. **My assumption is that you already have Python 3 installed on your computer.** To check, open a terminal window and type `python3 -V`. If the output does not display a version number, try `python -V`. If the latter command works, use `python` and `pip` instead of `python3` and `pip3`, respectively. If neither command shows a version number, install Python 3 first, and then return here. To see which non-built-in libraries are already installed, open a terminal window and type `pip3 list`.
1. os
    * This library is built-in, so you should not need to install anything.
2. xlsxwriter
    * This library is not built-in, so you need to open a terminal window and enter `pip3 install xlsxwriter` if you do not have the library.

### Warning
In Spring 2023, my semester of AME-341b, the xls files were opening in TextEdit as tab-delimited values. My assumption when making this script was that the delimiter would still be a tab, so it is a hard-coded value instead of a user input. If the values are not displaying properly in the xlsx files, maybe the delimiter changed. In that case, open one of the xls files in a plain text editor, see what the delimiter is, and then update the value in the code.

Also, I am using a Mac, so the path slashes in the tutorial are different from those for Windows: "/" versus "\\" (the script accounts for this difference in input, but the tutorial does not).
    * Note that Python's `os.path.normpath()` will correct "/" to "\\" on Windows, but will not correct "\\" to "/" on Mac.

### Example Folder Organization
Note that the ellipses in the folder paths below are meant to indicate that there could be a longer path. Suppose you had your xls files in folders that are all in one folder called XLS_Data:

.../XLS_Data
* /WT_Monday
* /WT_Tuesday
* /WT_Wednesday
* /WT_Thursday
* (etc.)

If you enter the XLS_Data folder path as the input and enter a new path for the output (for example, .../XLSX_Data), the following directory will be created, with every xls file in each folder (including the main one) converted to an xlsx file:

.../XLSX_Data
* /WT_Monday
* /WT_Tuesday
* /WT_Wednesday
* /WT_Thursday
* (etc.)

Note: there can be other non-xls files in the folders, but they will not be read or copied.

### Tutorial
If all of the libraries are installed, and the xls files are all in one folder (no matter how many subfolders there are), you are ready for the tutorial.
1. Run the script. **You can do this either from your IDE or a terminal window.** For this tutorial, I will use the terminal window (I used the `cd` command to get to the directory with the code). Beyond this step, the process is the same whether you use an IDE or terminal window.
```
brad@Brads-MBP ~ % cd "/Users/brad/Desktop/Courses/AME 341b/HW/Assignment Submissions/SE2/Python_XLS_Conv"
brad@Brads-MBP Python_XLS_Conv % python3 xls2xlsx.py
Enter the path to the folder containing the xls files:
 >> 
```

2. At this point, enter the path to the existing xls folder. Afterwards, you will be prompted to enter the path to the xlsx folder. Note the following:
    * The xlsx folder does not have to be currently existing; the code can make new folders. If the xlsx folder does exist, it will give you a warning and ask you to confirm.
    * The xls and xlsx folders **cannot** be the same.
    * The xlsx folder **cannot** be inside the xls folder.
    * **Do not use quotation marks.** The script evaluates these inputs as strings, so it does not matter if there are spaces in the file paths.
```
Enter file path to the folder containing the xls files:
 >> /Users/brad/Desktop/Courses/AME 341b/HW/Assignment Submissions/SE2/Python_XLS_Conv/XLS_Folder
Enter file path to the folder that will contain the converted xlsx files:
 >> /Users/brad/Desktop/Courses/AME 341b/HW/Assignment Submissions/SE2/Python_XLS_Conv/XLSX_Folder

Input (xls) root directory:
    /Users/brad/Desktop/Courses/AME 341b/HW/Assignment Submissions/SE2/Python_XLS_Conv/XLS_Folder
Output (xlsx) root directory:
    /Users/brad/Desktop/Courses/AME 341b/HW/Assignment Submissions/SE2/Python_XLS_Conv/XLSX_Folder
Continue? ('y'/'n'):
```

3. If the input and output directories are correct, continue. Note that the ellipsis in the output below is meant to show that there could be more files processed, and is **not** generated by the code.
```
Continue? ('y'/'n'): y
Current file: /Users/brad/Desktop/Courses/AME 341b/HW/Assignment Submissions/SE2/Python_XLS_Conv/XLS_Folder/WT_Monday/NACA0010U10Ap05_4.xls
Current file: /Users/brad/Desktop/Courses/AME 341b/HW/Assignment Submissions/SE2/Python_XLS_Conv/XLS_Folder/WT_Monday/NACA0010U10Ap05_3.xls
...
Done.
```

4. Your xlsx folder should now be created (or updated if it already existed).
    * Note that if the xlsx folder already existed, any files in it that do not have a corresponding xls file in the xls folder will **not** be overwritten or deleted.
