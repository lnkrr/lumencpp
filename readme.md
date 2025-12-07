![lumencpp](assets/logo.svg)

Lumen config file parser for C++20.

## CMake

Use `FetchContent` to include the library in your project:

```cmake
include(FetchContent)

FetchContent_Declare(
    lumencpp
    GIT_REPOSITORY https://github.com/lnkrr/lumencpp.git
    GIT_TAG v0.1
)

FetchContent_MakeAvailable(lumencpp)

target_link_libraries(<target> lumencpp)
```

## Usage

To parse a file, use the `lumen::parse_file` function:

```cpp
#include <iostream>
#include <string>

#include <lumencpp/lumen.h>

int main() {
    auto document = lumen::parse_file("metadata.lm");
    std::cout << document["license"].get<std::string>() << '\n';
}
```

To parse a string, use the `lumen::parse` function:

```cpp
#include <iostream>
#include <string>

#include <lumencpp/lumen.h>

int main() {
    auto document = lumen::parse(R"(
        license = "MIT License"
    )");

    std::cout << document["license"].get<std::string>() << '\n';
}
```

You can construct documents using syntax similar to `std::map`.

```cpp
#include <iostream>

#include <lumencpp/lumen.h>

int main() {
    lumen::Document document{
        {
            "data", {
                {"number", 42}
            }
        }
    };

    std::cout << document["data"]["number"].get<int>() << '\n';
}
```
