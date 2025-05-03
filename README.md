# MizuRunner

A simpler executable wrapper around the [Mizu](https://github.com/joshuadahlunr/mizuvm) assembly interpreter library.
It takes a input a binary in Mizu's [Portable Format](https://github.com/joshuadahlunr/MizuVM/blob/main/mizu/portable_format.hpp) and executes it.

```bash
# On linux this looks like:
mizu hello.mizu

# Or like this to see a printed trace of the instructions as they are executed
mizu-trace hello.mizu
```

## Features

- Lightweight Runtime (Only ~110kb)
- Write once run anywhere (Windows (todo: confirm), Linux, and Mac (todo: confirm) support).
- Foreign Function Interface to native DLLs (Example: https://github.com/joshuadahlunr/MizuRunner/blob/master/examples/hello_world_dumper.cpp).

## Creating Mizu Binaries

Unfortunately Mizu doesn't have an assembler, thus to create a Mizu binary you need to write a simple C++ executable with code for the Mizu program embedded. You then need to call Mizu's to_portable function and save the resulting binary blob to a file:
```cpp
fp::raii::dynarray<std::byte> portable = mizu::portable::to_portable(program_view, mizu_stack);
std::ofstream fout("program.mizu", std::ios::binary | std::ios::out);
fout.write((char*)portable.data(), portable.size());
```

A full example program dumper can be found in: https://github.com/joshuadahlunr/MizuRunner/blob/master/examples/bubble_sort_dumper.cpp