# WebAssembly.NET
This library is for loading and executing WebAssembly files entirely in managed .NET (it's not a wrapper).

# Status
It doesn't currently handle imports or tables yet, however, all opcodes aside from grow_memory and the complete file loading process have been implemented. Lots of testing required at this point!

# S-expressions? (wast)
This library doesn't load wast files at the moment - it's for the binary wasm files only.

# Usage

Here's an example of loading and using a WebAssembly module:

```csharp
using WebAssembly;


public static class Program
{
    
	public static void Main(string[] args)
	{
		
		// Load a wasm module from a file:
		Module module = new Module("hello.wasm");
		
		// Or from bytes:
		// byte[] myFile = System.IO.File.ReadAllBytes("hello.wasm");
		// module = new Module(myFile);
		
		// -- Accessing the contents --
		
		// Get e.g. a particular section:
		// module.ImportSection.Imports[0];
		
		// -- Executing the module --
		
		// Current approach for importing memory:
		// module.Memory = new Memory(2048);
		
		// Compile it now (one off):
		module.Compile();
		
		// Or cache it under the given name:
		// module.Compile("MyCachedWasm");
		
		if(module.Start())
		{
			// Module successfully started!
			Console.WriteLine("Module ready!");
		}
		
	}
	
}

```