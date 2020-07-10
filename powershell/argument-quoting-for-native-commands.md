# Quoting command arguments

When calling a native command, Powershell builds the command
line by simply wrapping arguments in double quotes.

This means that programs that use C-like argument parsing will
not get correctly quoted arguments when the arguments include
double quotes.

This can be fixed by running `$arg -replace '"', '\"'`

The following Python program can be used to demonstrate this:

```python
import sys
from ctypes import POINTER, byref, cdll, c_int, windll
from ctypes.wintypes import LPCWSTR, LPWSTR

GetCommandLineW = cdll.kernel32.GetCommandLineW
GetCommandLineW.argtypes = []
GetCommandLineW.restype = LPCWSTR

print("Raw command line:")
print(GetCommandLineW())
print("Arguments:")
for n, arg in enumerate(sys.argv):
    print(n, arg)
```

Note that I still don't fully understand the quoting rules. In
theory I could check the Powershell (core) sources, I guess.
