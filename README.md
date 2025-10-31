# Safe + Fast minimal GCC CMake (FOR DA BOYZ / FTB FTB FTB)
## clone, replace project name, init git and generate `compile_commands.json`
```bash
read -rp "Project name: " PROJECT_NAME
git clone https://github.com/jamisonrobey/cpp-gcc-safe-fast-cmake.git "$PROJECT_NAME"
cd "$PROJECT_NAME"
sed -i "s/template/${PROJECT_NAME}/g" CMakeLists.txt
cmake --preset debug
ln -sf build-debug/compile_commands.json compile_commands.json
rm -rf .git && git init -q
```
## Requirements:
- `gcc` 
    - Compiled to C++23 which requires `gcc >= 15` so if needed modify `CMAKE_CXX_STANDARD` in [`CMakePresets.json`](CMakePresets.json).
- `cmake`
- `ninja`
    -  [`CMakePresets.json`](CMakePresets.json) uses ninja as generator but you can easily change this
- Release uses `march=native`, so if you need to distribute your binaries modify the release flags.
- May need sanitizer runtimes for debug
