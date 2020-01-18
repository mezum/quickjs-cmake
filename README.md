# Unofficial QuickJS CMake scripts
[QuickJS](https://bellard.org/quickjs/) is a JavaScript interpreter.
This repository contains scripts to build QuickJS on CMake system.

# Usage
You must put "CMakeLists.txt" and "get_quickjs.cmake.in" on same cmake directory.
If you embed in your application, use "add_subdirectory()"
and add "quickjs" dependency to your project using "target_link_libraries()".

# Contributing
Welcome.
See [CONTRIBUTING.md](CONTRIBUTING.md) for more details.

# License
This cmake scripts are distributed under the MIT License.
See [LICENSE](LICENSE) for more details.

# Copyright
Copyright (c) 2020 Kosaki Mezumona
