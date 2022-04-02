# A repro of a fsi bug when loading scripts

If you load multiple files in a fsx script with the same filename but different path everything works OK. (Try executing `dotnet fsi working.fsx`).

But, if you create a `load-script.fsx` and you load the same files from different directories in it and `#load "load-script.fsx"` then you get an error

`error FS0239: An implementation of the file or module 'FSI_0001_Person' has already been given`

Try executing `dotnet fsi not-working.fsx`.

The problem appears to have to do something with namespaces. If both file define namespaces (with different names) the load-script does not work but if you change one of the files to define module then it works again.