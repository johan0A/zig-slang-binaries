# zig-slang-binaries

This is [Slang](https://shader-slang.org/) compiler binaries 
packaged for the [Zig](https://ziglang.org/) build system.

## how to use

1. Add `Slang` to the dependency list in `build.zig.zon`: 

```sh
zig fetch --save git+https://github.com/johan0A/zig-slang-binaries#v0.1.0+2025.6.3
```

2. Config `build.zig`:

```zig
const slang_dep = b.dependency("zig_slang_binaries", .{});
// get the path to the binaries
const slang_path = slang_dep.namedLazyPath("binaries");
// then for example here I can get an absolute path to slangc
const slang_exe_path = slang_path.join(b.allocator, "bin/slangc") catch @panic("OOM");
// and then use it with a run step
const system_command = b.addSystemCommand(&.{slang_exe_path.getPath2(b, null)});
// ...
```
