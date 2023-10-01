# pidmap
get pid mapping.

# functions
refet to test.lua

```
local Cpidmap = require("pidmap")

local m = Cpidmap.new("self", 'x', true)
local res = m:elfInfo(".*libc")
assert(res, "get libc position failed.")
local libc = res[4]
res = m:query(res[1] + 400)
assert(res, "check libc position failed.")
assert(libc == res[4], "check libc name failed.")
```

* new

create a new pidmap object, args list:

1. pid of task or self.
2. filter for segment permissions, use lua regular expression, eg to filter code segment, use 'x'. By default, no filtering.
3. Whether to filter only files. By default, no filtering.

* elfInfo

Gets the ELF file information in the first match. args list:

1. filter for segment file name, use lua regular expression,
 
the result is a table, {segment start address, segment end address, segment permissions, elf file name}.

* elfInfos

reter to elfInfo, the result is tables for matching elf name.

* query

Gets the ELF file information for address match. 

1. The address within the process.

the result is a table, {segment start address, segment end address, segment permissions, elf file name}.