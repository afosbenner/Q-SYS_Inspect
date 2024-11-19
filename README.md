# Q-SYS Inspect
Utility module for representing Lua values in a human-readable way.  This is useful for viewing tables in a pretty way to aid in debugging.

Based on inspect.lua by Enrique García Cota, commit 8686162. See https://github.com/kikito/inspect.lua for more information.  

## Installation
For more information, see [External Lua Modules on Q-SYS Online Help](https://help.qsys.com/q-sys_9.10/#Control_Scripting/External_Lua_Modules.htm "External Lua Modules on Q-SYS Online Help")

1. Clone repository to %DOCS%/QSC/Q-Sys Designer/Modules (such that all files are contained in a directory named Q-SYS_Inspect).
2. In Q-SYS Designer, open Design Resources, where Q-SYS_Inspect should now be listed under the Available tab.
3. Click on Install Module button. The module should now be listed under the Installed tab. See below for usage infomation.

## Typical Usage
Drop this into your script, at the top:
```lua
-- Reminder: install module in design using Design Resources
inspect = require("Q-SYS_Inspect")
local function insp(obj, objName)
  local objStr = inspect(obj)
  if objName then
    objStr = "Inspecting '"..objName.."'\n"..objStr
  end
  print("\n\n"..objStr.."\n")
end
```

Later, when you need to inspect a table (called tbl in this example):
```lua
insp(tbl, "tbl")
```
or just
```lua
insp(tbl)
```

## Example
Example script to demonstrate how it works:

```lua
inspect = require("Q-SYS_Inspect")
local function insp(obj, objName)
  local objStr = inspect(obj)
  if objName then
    objStr = "Inspecting '"..objName.."'\n"..objStr
  end
  print("\n\n"..objStr.."\n")
end

-- example table
local tbl = {"hello", "there", 100, true}
tbl.k = "v"

-- most basic usage
print("basic usage:")
print("\n"..inspect(tbl)) -- inspect returns a string, but does not print

-- usage with wrapper function
print("using wrapper function:")
insp(tbl)
print("using wrapper function with optional objName:")
insp(tbl, "tbl")
```

Output:

```
basic usage:

{
  [1] = "hello",
  [2] = "there",
  [3] = 100,
  [4] = true,
  ["k"] = "v"
}
using wrapper function:


{
  [1] = "hello",
  [2] = "there",
  [3] = 100,
  [4] = true,
  ["k"] = "v"
}

using wrapper function with optional objName:


Inspecting 'tbl'
{
  [1] = "hello",
  [2] = "there",
  [3] = 100,
  [4] = true,
  ["k"] = "v"
}


```

## Known Issues
Due to a deliberate limitation in the Q-SYS Lua environment, attempting to use inspect on tables of a sufficient size can cause a "Max execution limits exceeded" error to be thrown.