## resinfs

### Information
This library implements a platform-agnostic embedded filesystem mountpoint for use with various homebrew'd consoles. The implementation works by statically linking the romfs directory compressed with ustar to the executable.

This allows files to be stored in a hierarchical manner inside the binary directly, to be accessed by the program at run time. The aim is to solve the common problem of needing to access necessary files without them being external or bundled via a platform-specific library.

### Usage
#### Library usage
- Include library's header: `#include <romfs-wiiu.h>` (file is named this way even on other platforms)
- Call `ramfsInit()` at the start of your app and `ramfsInit()` before exiting

#### Makefile
To generate the resinfs, define a RAMFS_DIR variable in you makefile containing the path of your desired folder:

    RAMFS_DIR := ramfs_example_folder

Then, include this project's makefile and add the resinfs target to your linking targets along with the ld flags (change the example according to your makefile):

    include $(PORTLIBS_PATH)/wiiu/share/romfs-wiiu.mk
    CFLAGS		+=	$(ROMFS_CFLAGS)
    CXXFLAGS	+=	$(ROMFS_CFLAGS)
    LIBS		+=	$(ROMFS_LIBS)
    OFILES		+=	$(ROMFS_TARGET)

#### cmake
Include romfs's cmake file:

    include("${DEVKITPRO}/portlibs/wiiu/share/romfs-wiiu.cmake" REQUIRED)

Then, call romfs_add to build and link the romfs (make sure it's after all your_project add_executable calls):

    romfs_add(your_project "romfs_example_folder")

### Installing
A prebuild version for wiiu is available at the wiiu-fling pacman repository.
Please reffer to [these](https://gitlab.com/QuarkTheAwesome/wiiu-fling) instructions to set up wiiu-fling. 

To manually install the library:

    $ git clone https://github.com/yawut/libromfs-wiiu.git
    $ cd libromfs-wiiu
    $ make
    $ sudo make install