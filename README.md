# Safe + Fast minimal GCC CMake (FOR DA BOYZ / FTB FTB FTB)
## clone, replace project name, init git and generate `compile_commands.json`
```bash
PROJECT_NAME=$(bash -c 'read -p "Project name: " n && echo "$n"')
git clone https://github.com/jamisonrobey/cpp-gcc-safe-fast-cmake.git "$PROJECT_NAME"
cd "$PROJECT_NAME"
sed -i "s/template/$PROJECT_NAME/g" CMakeLists.txt
cmake --preset debug
ln -s build-debug/compile_commands.json compile_commands.json
rm -rf .git && git init
unset PROJECT_NAME
```
## Requirements:
- `gcc` 
    - Compiled to C++23 which requires `gcc >= 15` so if needed modify `"CMAKE_CXX_STANDARD` in [`CMakePresets.json`](CMakePresets.json).
- `cmake`
- `ninja`
    -  [`CMakePresets.json`](CMakePresets.json) uses ninja as generator but you can easily change this
- Release uses `mtune=native` and `march=native`, so if you need to distribute your binaries modify the release flags.
- May need sanitizer runtimes for debug
## Benchmarks of release preset
A CPU focused benchmark to show benefits or architecture tuning:
```cpp
#include <print>
#include <string>
int main(int argc, char **argv) {
  if (argc != 2) {
    return -1;
  }
  const auto n{std::stoll(argv[1])};
  double sum = 0.0;
  for (int i = 1; i <= n; i++) {
    sum += 1.0 / (i * i + 1.0);
  }
  std::println("{}", sum);
}
```
### Results
#### Release preset
```bash
cmake --preset release
cd build-release
hyperfine --warmup=3 "./template 1000000000"

Benchmark 1: ./template 1000000000
Time (mean ± σ): 629.4 ms ± 0.6 ms [User: 625.9 ms, System: 1.0 ms]
Range (min … max): 628.7 ms … 630.4 ms 10 runs
```
#### -O3
```bash
g++ src/main.cpp -o template -O3 -std=c++23
hyperfine --warmup=3 "./template 1000000000"

Benchmark 1: ./template 1000000000
  Time (mean ± σ):      1.111 s ±  0.005 s    [User: 1.105 s, System: 0.001 s]
  Range (min … max):    1.101 s …  1.117 s    10 runs
  ```











