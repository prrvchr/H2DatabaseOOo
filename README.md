<!--
╔════════════════════════════════════════════════════════════════════════════════════╗
║                                                                                    ║
║   Copyright (c) 2020 https://prrvchr.github.io                                     ║
║                                                                                    ║
║   Permission is hereby granted, free of charge, to any person obtaining            ║
║   a copy of this software and associated documentation files (the "Software"),     ║
║   to deal in the Software without restriction, including without limitation        ║
║   the rights to use, copy, modify, merge, publish, distribute, sublicense,         ║
║   and/or sell copies of the Software, and to permit persons to whom the Software   ║
║   is furnished to do so, subject to the following conditions:                      ║
║                                                                                    ║
║   The above copyright notice and this permission notice shall be included in       ║
║   all copies or substantial portions of the Software.                              ║
║                                                                                    ║
║   THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,                  ║
║   EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES                  ║
║   OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.        ║
║   IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY             ║
║   CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,             ║
║   TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE       ║
║   OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.                                    ║
║                                                                                    ║
╚════════════════════════════════════════════════════════════════════════════════════╝
-->
# [![H2DatabaseOOo logo][1]][2] Documentation

**Ce [document][3] en français.**

**The use of this software subjects you to our [Terms Of Use][4].**

# version [1.1.3][5]

## Introduction:

**H2DatabaseOOo** is part of a [Suite][6] of [LibreOffice][7] ~~and/or [OpenOffice][8]~~ extensions allowing to offer you innovative services in these office suites.  

This extension allows you to use [H2 Database][9] in embedded mode, making the database portable (a single odb file).  
It allows you to take advantage of the [ACID][10] properties of the underlying [H2 Database][11] database.

Being free software I encourage you:
- To duplicate its [source code][12].
- To make changes, corrections, improvements.
- To open [issue][13] if needed.

In short, to participate in the development of this extension.  
Because it is together that we can make Free Software smarter.

___

## Requirement:

The H2DatabaseOOo extension uses the jdbcDriverOOo extension to work.  
It must therefore meet the [requirement of the jdbcDriverOOo extension][14].

This extension cannot be installed together with the [HyperSQLOOo][15] extension.  
It's one or the other, but at the moment they can't work together (see [issue #156471][16]).

**On Linux and macOS the Python packages** used by the extension, if already installed, may come from the system and therefore **may not be up to date**.  
To ensure that your Python packages are up to date it is recommended to use the **System Info** option in the extension Options accessible by:  
**Tools -> Options -> Base drivers -> Embedded SQLite Driver -> View log -> System Info**  
If outdated packages appear, you can update them with the command:  
`pip install --upgrade <package-name>`

___

## Installation:

It seems important that the file was not renamed when it was downloaded.  
If necessary, rename it before installing it.

- [![jdbcDriverOOo logo][18]][19] Install **[jdbcDriverOOo.oxt][20]** extension [![Version][21]][20]

    This extension is necessary to use SQLite version 3.42.0.0 with all its features.

- ![H2DatabaseOOo logo][22] Install **[H2DatabaseOOo.oxt][23]** extension [![Version][24]][23]

Restart LibreOffice after installation.  
**Be careful, restarting LibreOffice may not be enough.**
- **On Windows** to ensure that LibreOffice restarts correctly, use Windows Task Manager to verify that no LibreOffice services are visible after LibreOffice shuts down (and kill it if so).
- **Under Linux or macOS** you can also ensure that LibreOffice restarts correctly, by launching it from a terminal with the command `soffice` and using the key combination `Ctrl + C` if after stopping LibreOffice, the terminal is not active (no command prompt).

___

## Use:

### How to create a new database:

In LibreOffice / OpenOffice go to File -> New -> Database...:

![H2DatabaseOOo screenshot 1][25]

In step: Select database:
- select: Create a new database
- in: Emdedded database: choose: Embedded SQLite Driver
- click on button: Next

![H2DatabaseOOo screenshot 2][26]

In step: Save and proceed:
- adjust the parameters according to your needs...
- click on button: Finish

![H2DatabaseOOo screenshot 3][27]

Have fun...

___

## How does it work:

H2DatabaseOOo is an [com.sun.star.sdbc.Driver][28] UNO service written in Python.  
It is an overlay to the [jdbcDriverOOo][19] extension allowing to store the SQLite database in an odb file (which is, in fact, a compressed file).

Its operation is quite basic, namely:

- When requesting a connection, three things are done:
    1. If it does not already exist, a **subdirectory** with name: `.` + `odb_file_name` + `.lck` is created in the location of the odb file where all SQLite files are extracted from the **database** directory of the odb file (unzip).
    2. A [DocumentHandler][29] is added as an [com.sun.star.util.XCloseListener][30] and [com.sun.star.document.XStorageChangeListener][31] to the odb file.
    3. The [jdbcDriverOOo][19] extension is used to get the [com.sun.star.sdbc.XConnection][32] interface from the **subdirectory** path + `odb_file_name`.

- When closing or renaming (Save as) an odb file the [DocumentHandler][29] copy all the files present in the **subdirectory** into the (new) **database** directory of the odb file (zip) and then delete the **subdirectory**.

___

## Has been tested with:

* OpenOffice 4.1.8 - Ubuntu 20.04 - LxQt 0.14.1

* OpenOffice 4.1.8 - Windows 7 SP1

* LibreOffice 7.0.4.2 - Ubuntu 20.04 - LxQt 0.14.1

* LibreOffice 6.4.4.2 - Windows 7 SP1

* LibreOffice 7.6.0.1 - Windows 10

* LibreOffice 7.6.0.1 - Ubuntu 22.04

I encourage you in case of problem :confused:  
to create an [issue][13]  
I will try to solve it :smile:

___

## Historical:

### What has been done for version 1.0.0:



### What remains to be done for version 1.0.0:

- Add new language for internationalization...

- Anything welcome...

[1]: </img/sqlite.svg#collapse>
[2]: <https://prrvchr.github.io/H2DatabaseOOo/>
[3]: <https://prrvchr.github.io/H2DatabaseOOo/README_fr>
[4]: <https://prrvchr.github.io/H2DatabaseOOo/source/H2DatabaseOOo/registration/TermsOfUse_en>
[5]: <https://prrvchr.github.io/H2DatabaseOOo#historical>
[6]: <https://prrvchr.github.io/>
[7]: <https://www.libreoffice.org/download/download/>
[8]: <https://www.openoffice.org/download/index.html>
[9]: <https://github.com/xerial/sqlite-jdbc>
[10]: <https://en.wikipedia.org/wiki/ACID>
[11]: <https://www.sqlite.org/transactional.html>
[12]: <https://github.com/prrvchr/H2DatabaseOOo/>
[13]: <https://github.com/prrvchr/H2DatabaseOOo/issues/new>
[14]: <https://prrvchr.github.io/jdbcDriverOOo/#requirement>
[15]: <https://prrvchr.github.io/HyperSQLOOo/#requirement>
[16]: <https://bugs.documentfoundation.org/show_bug.cgi?id=156471>

[18]: <https://prrvchr.github.io/jdbcDriverOOo/img/jdbcDriverOOo.svg#middle>
[19]: <https://prrvchr.github.io/jdbcDriverOOo>
[20]: <https://github.com/prrvchr/jdbcDriverOOo/releases/latest/download/jdbcDriverOOo.oxt>
[21]: <https://img.shields.io/github/v/tag/prrvchr/jdbcDriverOOo?label=latest#right>
[22]: <img/H2DatabaseOOo.svg#middle>
[23]: <https://github.com/prrvchr/H2DatabaseOOo/releases/latest/download/H2DatabaseOOo.oxt>
[24]: <https://img.shields.io/github/downloads/prrvchr/H2DatabaseOOo/latest/total?label=v1.0.0#right>
[25]: <img/H2DatabaseOOo-1.png>
[26]: <img/H2DatabaseOOo-2.png>
[27]: <img/H2DatabaseOOo-3.png>
[28]: <https://www.openoffice.org/api/docs/common/ref/com/sun/star/sdbc/Driver.html>
[29]: <https://github.com/prrvchr/H2DatabaseOOo/blob/main/uno/lib/uno/embedded/documenthandler.py>
[30]: <https://www.openoffice.org/api/docs/common/ref/com/sun/star/util/XCloseListener.html>
[31]: <http://www.openoffice.org/api/docs/common/ref/com/sun/star/document/XStorageChangeListener.html>
[32]: <https://www.openoffice.org/api/docs/common/ref/com/sun/star/sdbc/XConnection.html>
[33]: <https://github.com/gotson>
[34]: <https://github.com/xerial/sqlite-jdbc/issues/786>
[35]: <https://bugs.documentfoundation.org/show_bug.cgi?id=156511>
[36]: <https://github.com/prrvchr/uno/commit/a2fa9f5975a35e8447907e51b0f78ac1b1b76e17>
[37]: <https://github.com/prrvchr/H2DatabaseOOo/releases/latest/download/requirements.txt>
[38]: <https://peps.python.org/pep-0508/>
[39]: <https://prrvchr.github.io/H2DatabaseOOo/#requirement>
[40]: <https://prrvchr.github.io/jdbcDriverOOo/#what-has-been-done-for-version-112>
[41]: <https://github.com/prrvchr/sqlite-jdbc/releases/download/3.45.1.3-SNAPSHOT/sqlite-jdbc-3.45.1.3-SNAPSHOT.jar>
[42]: <https://www.openoffice.org/api/docs/common/ref/com/sun/star/sdbc/XGeneratedResultSet.html>
[43]: <https://github.com/prrvchr/sqlite-jdbc/releases/download/3.45.1.6-SNAPSHOT/sqlite-jdbc-3.45.1.6-SNAPSHOT.jar>
