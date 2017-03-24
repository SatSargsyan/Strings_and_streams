# Strings and streams


#### Let’s include WriteLine statements in the destructor and constructor of our class and see how the program behaves when an object of that class is created and when the program ends:
```C#
class Dog
{
  public Dog() {
    Console.WriteLine("Constructor");
  }
  ~Dog() {
    Console.WriteLine("Destructor");
  }
}
static void Main(string[] args) {
  Dog d = new Dog();
}
/*Outputs:
Constructor
Destructor
/*
```
#### When the program runs, it first creates the object, which calls the constructor. The object is deleted at the end of the program and the destructor is invoked when the program's execution is complete.
### If the class is working with storage or files. The constructor would initialize and open the files. Then, when the program ends, the destructor would close the files.





### StreamReader Class (using System.IO)
<a href=https://msdn.microsoft.com/en-us/library/system.io.streamreader(v=vs.110).aspx#Thread Safety> StreamReader</a> is designed for character input in a particular encoding, whereas the Stream class is designed for byte input and output. Use StreamReader for reading lines of information from a standard text file.

#### This type implements the IDisposable interface. When you have finished using the type, you should dispose of it either directly or indirectly. To dispose of the type directly, call its Dispose method in a try/catch block. To dispose of it indirectly, use a language construct such as using (in C#) or Using (in Visual Basic). For more information, see the “Using an Object that Implements IDisposable” section in the IDisposable interface topic.

By default, a StreamReader is not thread safe. 
See <a href=https://msdn.microsoft.com/en-us/library/system.io.textreader.synchronized(v=vs.110).aspx> TextReader.Synchronized</a> for a thread-safe wrapper.


### To view the .NET Framework source code for this type, 
see the <a href=https://referencesource.microsoft.com/#mscorlib/system/io/streamreader.cs,b5fe1efcec14de32> Reference Source</a>. You can browse through the source code online, download the reference for offline viewing, and step through the sources (including patches and updates) during debugging; see instructions.


The Read(Char[], Int32, Int32) and Write(Char[], Int32, Int32) method overloads read and write the number of characters specified by the count parameter. These are to be distinguished from BufferedStream.Read and BufferedStream.Write, which read and write the number of bytes specified by the count parameter. Use the BufferedStream methods only for reading and writing an integral number of byte array elements.

#### When reading from a Stream, it is more efficient to use a buffer that is the same size as the internal buffer of the stream.

#### The following example uses an instance of StreamReader to read text from a file. The constructor used in this example is not supported for use in Windows Store Apps.
```C#
using System;
using System.IO;

class Test 
{
    public static void Main() 
    {
        try 
        {
            // Create an instance of StreamReader to read from a file.
            // The using statement also closes the StreamReader.
            using (StreamReader sr = new StreamReader("TestFile.txt")) 
            {
                string line;
                // Read and display lines from the file until the end of 
                // the file is reached.
                while ((line = sr.ReadLine()) != null) 
                {
                    Console.WriteLine(line);
                }
            }
        }
        catch (Exception e) 
        {
            // Let the user know what went wrong.
            Console.WriteLine("The file could not be read:");
            Console.WriteLine(e.Message);
        }
    }
}
```
#### The following example instantiates a StreamReader object and calls its
<a href=https://msdn.microsoft.com/en-us/library/system.io.streamreader.readasync(v=vs.110).aspx> ReadAsync </a>method to read a file asynchronously.

```C#
using System;
using System.IO;
using System.Threading.Tasks;

class Example
{
    public static void Main()
    {
        ReadAndDisplayFilesAsync();
    }

    private async static void ReadAndDisplayFilesAsync()
    {
        String filename = "TestFile1.txt";
        Char[] buffer;

        using (var sr = new StreamReader(filename)) {
            buffer = new Char[(int)sr.BaseStream.Length];
            await sr.ReadAsync(buffer, 0, (int)sr.BaseStream.Length);
        }

        Console.WriteLine(new String(buffer));
    }
}
```


### StreamWriter Class  (using System.IO)

<a href=https://msdn.microsoft.com/en-us/library/system.io.streamwriter(v=vs.110).aspx> Implements a TextWriter for writing characters to a stream in a particular encoding.</a>

The following example shows how to use a StreamWriter object to write a file that lists the directories on the C drive, and then uses a StreamReader object to read and display each directory name. A good practice is to use these objects in a using statement so that the unmanaged resources are correctly disposed. The using statement automatically calls Dispose on the object when the code that is using it has completed. The constructor used in this example is not supported for use in Windows Store Apps.

```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;

namespace StreamReadWrite
{
    class Program
    {
        static void Main(string[] args)
        {
            // Get the directories currently on the C drive.
            DirectoryInfo[] cDirs = new DirectoryInfo(@"c:\").GetDirectories();

            // Write each directory name to a file.
            using (StreamWriter sw = new StreamWriter("CDriveDirs.txt"))
            {
                foreach (DirectoryInfo dir in cDirs)
                {
                    sw.WriteLine(dir.Name);

                }
            }

            // Read and show each line from the file.
            string line = "";
            using (StreamReader sr = new StreamReader("CDriveDirs.txt"))
            {
                while ((line = sr.ReadLine()) != null)
                {
                    Console.WriteLine(line);
                }
            }
        }
    }
}
```


### TextReader Class

```C#
using System;
using System.Windows;
using System.IO;
using System.Text;

namespace WpfApplication
{
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
        }

        private async void Button_Click_1(object sender, RoutedEventArgs e)
        {
            string filename = @"C:\Example\existingfile.txt";
            char[] result;
            StringBuilder builder = new StringBuilder();

            using (StreamReader reader = File.OpenText(filename))
            {
                result = new char[reader.BaseStream.Length];
                await reader.ReadAsync(result, 0, (int)reader.BaseStream.Length);
            }

            foreach (char c in result)
            {
                if (char.IsLetterOrDigit(c) || char.IsWhiteSpace(c))
                {
                    builder.Append(c);
                }
            }
            FileOutput.Text = builder.ToString();
        }
    }
}
```
