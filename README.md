Download Link: https://assignmentchef.com/product/solved-cop4600-project-2-posix-standards-bindings
<br>






<h1>Prologue</h1>

Your work in the Legion has been highly praised, but you’ve had a creeping concern since. You’d always assumed that, as a faithful soldier, you would be rewarded and be permitted to serve as a vassal upon the subjugation of Earth. However, through the metadata you’ve analyzed, you’ve discovered that ultimately “lesser creatures” – including humans such as yourself – will likely be eliminated once Earth is conquered. As you continue your investigation, you take on another task with hopes you’ll still be considered a useful pawn on the board. This time, you’re tasked with creating a program capable of printing out the contents of specified files. Realizing the importance of the documents being stored on Sky Skink, the Legion’s cloud system, you’ll also create a backdoor that connects the file’s contents to a GUI for readability for later access. It might come in handy down the road.

<h1>Overview</h1>

Modern operating systems are often built in layers with specific goals and limited privileges. Layering also facilitates the implementation of recognized standards by separating hardware and OS-specific implementations from generalized API calls. Often these layers are written in different languages and permit access via a binding layer to lower level functionality. In Android, POSIX functions can be called from Java applications via the Native Development Kit (NDK).




In this project, you will build a C++ language function that calls POSIX system library procedures to read a text file and return it as a C-style string (null-terminated character array). You will also build two programs that use your C++ functions – a simple program at the Android application layer that uses the NDK binding to call your C++ functions to read and display a text file in an application window, and another version that will print the text file to the screen in Ubuntu. We will provide a program that exercises your new call and program on the command line. You’ll then create a short video to demonstrate your code. You’ll submit the project via Canvas.

<h1>Structure</h1>

The project is broken into four main parts:




<ul>

 <li>Create a C++ function that reads a text file via POSIX calls and returns a pointer to its contents</li>

 <li>Create a short program that uses the function above to display a file via the command line</li>

 <li>Create a simple Android GUI application that accepts a text file name as input and has a text box</li>

 <li>Bind the function via the NDK to that the application to display the contents of the file in the text box</li>

</ul>

<strong>Figure 1: A function is called from a text program, and separately, bound to the GUI application. </strong>




While exact implementation may vary, the library functions must match the signatures laid out in this document.

<strong> </strong>

<h2>Specification</h2>

Students will write several sections of code according the following specifications.

<strong> </strong>

<u>File Reader Library</u>

The files <strong>read_file.h</strong> / <strong>read_file.cpp</strong> will contain declaration / definition of this function:




<em>char *</em><strong>read_file</strong>(const char *filename)

Makes POSIX calls to read the contents of filename from disk to be stored in a null-terminated character array (C-style string). The array should be allocated dynamically. A pointer to the array will be returned. <strong><em>The caller will be expected to free the memory allocated for the array. </em></strong>If the file is not found, it should return <strong>nullptr</strong>.







<u>Text Program</u>

The text program, once built, should have the name <strong>displayfile</strong> and should take exactly one command line argument – the filename of the file to be displayed on the screen. It should use the <strong>read_file()</strong> function. If a file cannot be found, the text program should print “<strong>Error: File Note Found</strong>”:




<strong>$</strong><strong> ./displayfile /sdcard/example.txt </strong>

Contents of

<strong>Hello world!                                           </strong><strong>/sdcard/example.txt </strong>

<strong>This is the last line of the file.         </strong>Hello world!     <strong> </strong>

<strong>$                                          </strong>This is the last line of the file.<strong>       </strong>

<strong> </strong><em> </em>

<strong>$</strong><strong> ./displayfile nope.txt </strong>

<strong>Error: File Not Found                         </strong><em>Note that </em><strong><em>nope.txt</em></strong><em> does not exist.</em>

<strong>$                                          </strong><strong> </strong>







<u>GUI Program</u>

The GUI program skeleton <strong><u>provides</u></strong> three GUI elements (without functional code). Students must add code as necessary to elicit the following behavior:




<ul>

 <li>One-line text box where the file to be displayed will be typed by the user, named <strong>filenameBox</strong></li>

 <li>Button to submit the filename (which should trigger the read and display), named <strong>submitButton</strong></li>

 <li>Multi-line text box where the file will be displayed when the button is pressed, named <strong>displayBox</strong></li>

</ul>




Students should modify the Java source to invoke the C++ functions. A simple example of transmitting a string from C++ to Java is included in the project base code. You must use <u>the exact same source files</u> created in the File Reader Library for this task to receive credit, <em>comments and includes are no exception</em>. As in the text program, if a file cannot be found, then the GUI must display the error message in the text box (“<strong>Error: File Not Found</strong>”).




<strong>NOTE: </strong>You will need to add any new C++ source files to the <strong>CMakeLists.txt </strong>build file! When accessing files, it must be the absolute path starting with <strong>/mnt/ubuntu/&lt;abs_path&gt;</strong>, do NOT prepend this in your code!