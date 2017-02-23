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
