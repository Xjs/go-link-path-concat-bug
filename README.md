# Illustration of pathname concatenation failure

The linker concatenates the package name `fmt` with the backslashy, relative, and very long `GOROOT` path with a `/`. This leads to the Windows syscalls not seeing the file. More information about that under https://docs.microsoft.com/en-gb/windows/desktop/FileIO/naming-a-file#maxpath .

To reproduce (assuming GOROOT=C:\Go): 

```
> initialise.bat
> run-test.bat
warning: unable to find runtime.a
C:\\Go\\pkg\\tool\\windows_amd64\\link.exe: cannot open file aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa\Go\pkg\windows_amd64/fmt.a: open aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa\Go\pkg\windows_amd64/fmt.a: The system cannot find the path specified.
```


