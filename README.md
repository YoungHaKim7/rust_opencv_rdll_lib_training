# rust_opencv_training

#  Creating A DLL With Rust
- https://samrambles.com/guides/window-hacking-with-rust/creating-a-dll-with-rust/index.html#wait-what

<hr />

# Windows dll 분석
- https://users.rust-lang.org/t/rustc-windows-how-to-specify-dllexport-for-staticlib-functions/97296/4
- https://github.com/mesonbuild/meson/tree/master/test%20cases/rust/15%20polyglot%20sharedlib

```bash
[1/7] "cl" "-Iadder-1.dll.p" "-I." "-I.." "/MDd" "/nologo" "/showIncludes" "/utf-8" "/W2" "/Od" "/Zi" "-DBUILDING_ADDER" "/Fdadder-1.dll.p\adder.c.pdb" /Foadder-1.dll.p/adder.c.obj "/c" ../adder.c
[2/7] "cl" "-Iaddertest.exe.p" "-I." "-I.." "/MDd" "/nologo" "/showIncludes" "/utf-8" "/W2" "/Od" "/Zi" "/Fdaddertest.exe.p\addertest.c.pdb" /Foaddertest.exe.p/addertest.c.obj "/c" ../addertest.c
[3/7] "rustc" "-C" "linker=link" "--color=always" "--crate-type" "cdylib" "-g" "-C" "relocation-model=pic" "--crate-name" "radder" "--emit" "dep-info=radder.d" "--emit" "link" "-o" "radder.dll" ../adder.rs
[4/7] "C:\Python38\python.exe" "C:\Users\Collabora\xclaesse\meson\meson.py" "--internal" "symbolextractor" "C:\Users\Collabora\xclaesse\meson\test cases\rust\15 polyglot sharedlib\builddir" radder.dll "radder.dll.lib" radder.dll.p/radder.dll.symbols
[5/7] "link"  /MACHINE:x64 /OUT:adder-1.dll adder-1.dll.p/adder.c.obj "/nologo" "/release" "/nologo" "/DEBUG" "/PDB:adder-1.pdb" "/DLL" "/IMPLIB:adder.lib" "radder.dll.lib" "-Wl,-u,adder_add" "kernel32.lib" "user32.lib" "gdi32.lib" "winspool.lib" "shell32.lib" "ole32.lib" "oleaut32.lib" "uuid.lib" "comdlg32.lib" "advapi32.lib"
LINK : warning LNK4044: unrecognized option '/Wl,-u,adder_add'; ignored
   Creating library adder.lib and object adder.exp
[6/7] "C:\Python38\python.exe" "C:\Users\Collabora\xclaesse\meson\meson.py" "--internal" "symbolextractor" "C:\Users\Collabora\xclaesse\meson\test cases\rust\15 polyglot sharedlib\builddir" adder-1.dll "adder.lib" adder-1.dll.p/adder-1.dll.symbols
[7/7] "link"  /MACHINE:x64 /OUT:addertest.exe addertest.exe.p/addertest.c.obj "/nologo" "/release" "/nologo" "/DEBUG" "/PDB:addertest.pdb" "adder.lib" "/SUBSYSTEM:CONSOLE" "kernel32.lib" "user32.lib" "gdi32.lib" "winspool.lib" "shell32.lib" "ole32.lib" "oleaut32.lib" "uuid.lib" "comdlg32.lib" "advapi32.lib"
FAILED: addertest.exe addertest.pdb
"link"  /MACHINE:x64 /OUT:addertest.exe addertest.exe.p/addertest.c.obj "/nologo" "/release" "/nologo" "/DEBUG" "/PDB:addertest.pdb" "adder.lib" "/SUBSYSTEM:CONSOLE" "kernel32.lib" "user32.lib" "gdi32.lib" "winspool.lib" "shell32.lib" "ole32.lib" "oleaut32.lib" "uuid.lib" "comdlg32.lib" "advapi32.lib"
addertest.c.obj : error LNK2019: unresolved external symbol __imp_adder_add referenced in function main
addertest.exe : fatal error LNK1120: 1 unresolved externals
ninja: build stopped: subcommand failed.
```
