# Strings and streams


####Let’s include WriteLine statements in the destructor and constructor of our class and see how the program behaves when an object of that class is created and when the program ends:
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
####When the program runs, it first creates the object, which calls the constructor. The object is deleted at the end of the program and the destructor is invoked when the program's execution is complete.
### If the class is working with storage or files. The constructor would initialize and open the files. Then, when the program ends, the destructor would close the files.



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
####The following example instantiates a StreamReader object and calls its ReadAsync method to read a file asynchronously.

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
