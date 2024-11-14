# Virtual arena

A arena backed by virtual memory and easy useage of scratch arenas, see the tests for the interface (it's simple, I promise).

## Install
1. Declare as dependency:
```console
zig fetch --save git+https://github.com/freergit/virtual-arena.git#main
```

2. Expose the lib as a module in build.zig (this may get outdated since Zig changes all the time)
```zig
const std = @import("std");

pub fn build(b: *std.Build) void {
    const target = b.standardTargetOptions(.{});
    const optimize = b.standardOptimizeOption(.{});

    const virt_arena_dep = b.dependency("virtual-arena", .{ .target = target, .optimize = optimize });
    const virt_arena_module = mpsc_dep.module("virtual-arena");

    const exe = b.addExecutable(.{
        .name = "my-project",
        .root_source_file = b.path("src/main.zig") ,
        .target = target,
        .optimize = optimize,
    });
    exe.root_module.addImport("virtual-arena", virt_arena_module);
    
    // ...
}

```

Of course, you can simply copy paste the implementation (it's just one file) or use something like gitsubtree.