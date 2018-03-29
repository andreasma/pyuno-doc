Introduction
============

The Python-UNO bridge (PyUNO bridge) gives the opportunity to:

* use the LibreOffice API with the Python3 language,
* develop UNO components in Python3 and run them also within the LibreOffice process with other languages like Java, C++ or StarBasic scripting language,
* create and run Python scripts within the LibreOffice scripting framework.

State
-----

The current LibreOffice (6.0) delivers Python (CPython) version 3.5. LibreOffie changed the Python version from version 2 to 3 a longer time ago. The PyUNO bridge of LibreOffice is feature complete.  Because the PyUNO features are not used heavily there may be some unknown issues inside this scrpting framework. If you find a problem you could file an issue in the LibreOffice bugtracker and help to improve the Python scripting framework / UNO api.


PyUNO Documentation
-------------------

This documentation should show how the PyUNO bridge could be used to automate LibreOffice. This is not a documentation of LibreOffice.


PyUNO Installation
------------------

The PyUNO bridge will be installed within a default installation process of LibreOffice. That's also true for the installation within the package system of a Linux distribution (e.g. openSuSE).

PyUNO Bridge Modes
------------------

PyUNO could be used in three dirrerent modes:

1. Inside LibreOffice process within the scripting framework.
2. Inside the Python executable (and outside the LibreOffice process).
3. Inside the LibreOffice process


First Start of the LibreOffice from Command Line
------------------------------------------------

It's important to ensure that LibreOffice is not running. If you are on Windows probably you have also to terminate the quick starter in the system tray at the right bottom of your desktop. Start a system shell and type in a similar command like the one in the following examples. You could type in the whole path to (and including) 'soffice' within the LibreOffice program subdirectory or go to that directory and call 'soffice' with the parameters directly.

**Examples:**

Windows:
::

   c:\Program Files\libreOffice6.0\program  soffice "--accept=socket,host=localhost,port=2002;urp;"


Linux
::

  /opt/libreoffice6.0/program/soffice "--accept=socket,host=localhost,port=2002;urp;"
  

Hello World
-----------

You could now start your prefered text editor and create a new Python sample amodule hello_libreoffice_world.py

::

  import uno
  
  # get the uno component context from the PyUNO runtime
  context = uno.getComponentContext()
  
  
  # create the UnoUrlResolver
  resolver = context.ServiceManager.createInstanceWithContext("com.sun.star.bridge.UnoUrlResolver", context )
  
  # connect to the running LibreOffice
  libreo = resolver.resolve( "uno:socket,host=localhost,port=2002;urp;StarOffice.ComponentContext" )
  libmsgn = libreo.ServiceManager
  

  # get the central desktop object
  desktop = libmsgn.createInstanceWithContext( "com.sun.star.frame.Desktop",libreo)
  
  # access the current LibreOffice writer document
  currentdocument = desktop.getCurrentComponent()
  
  # access the LibreOffice document's text property
  text = currentdocument.Text

  # create a cursor
  cursor = text.createTextCursor()
  
  #insert text in the LibreOffice writer document
  text.insertString( cursor, "Hello LibreOffice World \n You have successfull submitted a text to LibreOffice.\n Congratulations!\n The Document Foundation", 0 )
  
  #
  libreo.ServiceManager
  

Because this example writes text to a new textdocument you have to start LibreOffice with the modul Writer. Thus you had to change the lines above as follows:


Windows:
::

   c:\Program Files\libreOffice6.0\program>  soffice --writer "--accept=socket,host=localhost,port=2002;urp;"


Linux
::

  /opt/libreoffice6.0/program/soffice --writer "--accept=socket,host=localhost,port=2002;urp;"
  

Then you could run the hello_libreoffice_world.py script:

Windows:
::
  c:\Program Files\libreOffice6.0\program\python hello_libreoffice_world.py
  
  
Linux:
::
  /opt/libreoffice6.0/program/python hello_libreoffice_world.py
  

You will get a new LibreOffice Writer document with the (expanded) hello world text.
  
  
  
