# lumencpp

Lumen config file parser for C++20.

## Build

Clone the repository:

```bash
$ git clone https://github.com/veevol/lumencpp && cd lumencpp
```

Build with `make`:

```bash
$ make
```

To install the library system-wide, run:

```bash
$ sudo make install
```

## Usage

To parse a file, use the `lumen::parse_file` function:

```cpp
#include <iostream>
#include <string>

#include <lumencpp/document.h>

int main() {
    try {
        auto document = lumen::parse_file("metadata.lm");
        std::cout << document["license"].as<std::string>() << '\n';
    } catch (const lumen::SyntaxError& error) {
        std::cout << error.pretty() << '\n';
    } catch (const std::exception& error) {
        std::cout << "error: " << error.what() << '\n';
    }
}
```

To parse a string, use the `lumen::parse` function:

```cpp
#include <iostream>
#include <string>

#include <lumencpp/document.h>

int main() {
    try {
        auto document = lumen::parse(R"(
            license = "MIT License"
        )");

        std::cout << document["license"].as<std::string>() << '\n';
    } catch (const lumen::SyntaxError& error) {
        std::cout << error.pretty() << '\n';
    } catch (const std::exception& error) {
        std::cout << "error: " << error.what() << '\n';
    }
}
```

You can construct documents using syntax similar to `std::map`.

```cpp
#include <iostream>

#include <lumencpp/document.h>

int main() {
    lumen::Document document{
        {
            "data", {
                {"number", 42}
            }
        }
    };

    std::cout << document["data"]["number"].as<int>() << '\n';
}
```
