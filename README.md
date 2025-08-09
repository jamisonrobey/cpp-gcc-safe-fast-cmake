Safe + Fast minimal GCC CMake (FOR DA BOYZ / FTB FTB FTB)

## Requirements:

- `gcc` 
    - [`CMakePresets.json`](CMakePresets.json) uses `-std=c++23` by default but can be modified
    - `main.cpp` uses `<print>` which requires `gcc` >= 14 but also can easily be changed
- `cmake`
- `ninja`
    -  [`CMakePresets.json`](CMakePresets.json) uses ninja as generator but you can easily change this
- release uses `mtune` and `march` set to native so this template is best for projects that will be built by users and not distributed binaries.
    - test release build vs plain `-O3` and you will observe faster binaries (with less runtime variation as well)
## clone w/ project name and init git
```bash
PROJECT_NAME=$(bash -c 'read -p "Project name: " n && echo "$n"')
git clone https://github.com/jamisonrobey/cpp-gcc-safe-fast-cmake.git "$PROJECT_NAME"
cd "$PROJECT_NAME"
sed -i "s/template/$PROJECT_NAME/g" CMakeLists.txt
rm -rf .git && git init
unset PROJECT_NAME
```



