While most of the methods mentioned above are predominantly used in the frontend (TypeScript), these concepts are also available in the backend. However, for C#, we mainly use the **_async_** and **_await_** keywords.

Any method we normally create in C# is synchronous by default. We can change this by placing the async keyword before the return data type of a method. If the said method returns a value, the return type of the method should then be changed to **Task<data type of return value>**. Calling this new async method should then be preceded by the await keyword to properly retrieve the value returned by the Task.

Below is sample code showcasing simple usage of the keywords:

``` cs
class Program  
{  
    static void Main()  
    {  
        Task task = new Task(CallMethod);  
        task.Start();  
        task.Wait();  
        Console.ReadLine();  
    }  
  
    static async void CallMethod()  
    {  
        string filePath = "E:\\sampleFile.txt";  
        Task<int> task = ReadFile(filePath);  
  
        Console.WriteLine(" Other Work 1");  
        Console.WriteLine(" Other Work 2");  
        Console.WriteLine(" Other Work 3");  
  
        int length = await task;  
        Console.WriteLine(" Total length: " + length);  
  
        Console.WriteLine(" After work 1");  
        Console.WriteLine(" After work 2");  
    }  
  
    static async Task<int> ReadFile(string file)  
    {  
        int length = 0;  
  
        Console.WriteLine(" File reading is stating");  
        using (StreamReader reader = new StreamReader(file))  
        {  
            // Reads all characters from the current position to the end of the stream asynchronously    
            // and returns them as one string.    
            string s = await reader.ReadToEndAsync();  
  
            length = s.Length;  
        }  
        Console.WriteLine(" File reading is completed");  
        return length;  
    }  
}  

```