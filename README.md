# mh3u-se
Fork of mh3u-se that is buildable on Unix-like Systems (Linux and macOS)

Compilation (macOS / Linux)

Dependencies

CMake (≥ 3.10)
Qt5 (Core, Widgets, Gui)
A C++11 compiler (Clang or GCC)
Build steps

bash
# Clone the repository
git clone https://github.com/yourusername/mh3u-se.git
cd mh3u-se

# Configure and build
mkdir build && cd build
cmake ..
make

# (macOS only) Create a portable .app bundle
make install   # or manually run: macdeployqt mh3u-se-gui.app
Running

macOS: Double‑click mh3u-se-gui.app in the build/ folder (data files are bundled inside the app).

Linux: Run ./mh3u-se-gui from the build/ directory – the data/ folder must be present in the same location (copy it manually if needed).

Note: On Linux, the application looks for a data/ folder in the current working directory. You can either run from the repository root (./build/mh3u-se-gui) or copy the data/ folder into the build directory.
