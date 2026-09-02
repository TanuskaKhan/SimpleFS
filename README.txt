CSE 321: Operating Systems
SimpleFS Lab Term Project
Summer 2026

GROUP INFORMATION
Group Number: 13

Group Members:
1. Tanuska Khan (23101241)
2. MD Al-farabi (22299262)
3. Syed Sayan Kabir Onan (24101501)

PROJECT DESCRIPTION
SimpleFS is a small educational file system implemented in C inside a 256 KiB binary image. The builder program creates and initializes an empty SimpleFS image with a superblock, inode bitmap, data bitmap, inode table, root inode, and the root directory entries "." and "..". The adder program adds regular files from the current working directory using first-fit inode and data-block allocation, stores file data in up to three direct blocks, creates the corresponding inode and root-directory entry, and updates the allocation bitmaps and root-directory size.

FILES INCLUDED
1. simplefs.h          - Fixed constants and structures from the starter package. Not modified.
2. simplefs_builder.c  - Creates and initializes an empty SimpleFS image.
3. simplefs_adder.c    - Adds one regular file to an existing SimpleFS image.
4. README.txt          - Project information, commands, implementation summary, contributions, and limitations.

COMPILATION
Run the following commands in the project directory:

gcc -Wall -Wextra -std=c11 simplefs_builder.c -o simplefs_builder
gcc -Wall -Wextra -std=c11 simplefs_adder.c -o simplefs_adder

EXECUTION EXAMPLES
Create a new SimpleFS image:
./simplefs_builder --image disk.img

Add files from the current working directory:
./simplefs_adder --input disk.img --file test1.txt
./simplefs_adder --input disk.img --file test2.txt

IMPLEMENTATION SUMMARY
- Uses a block size of 4096 bytes and 64 total blocks.
- Creates an image of exactly 262144 bytes (256 KiB).
- Stores the superblock in Block 0.
- Stores the inode bitmap in Block 1.
- Stores the data bitmap in Block 2.
- Stores 32 fixed-size inodes in Block 3.
- Uses Blocks 4-63 as the data region.
- Reserves inode 1 and Block 4 for the root directory.
- Initializes the root directory with "." and ".." entries.
- Uses first-fit allocation for inodes and data blocks.
- Supports regular files up to 12288 bytes using three direct block pointers.
- Supports filenames up to 58 characters.
- Rejects duplicate filenames, oversized files, missing source/image files, invalid images, exhausted inodes, and insufficient free data blocks.
- Zero-fills unused bytes in the final allocated data block.
- Supports zero-byte files without allocating a data block.

GROUP MEMBER CONTRIBUTIONS
1. Tanuska Khan (23101241) - Took primary responsibility for the core implementation and integration of the project, including the SimpleFS builder logic, superblock and root-directory initialization, inode/data allocation logic, file-copying workflow, inode and directory-entry updates, overall debugging, test coordination, and final documentation preparation.

2. MD Al-farabi (22299262) - Contributed to implementation review and verification, with emphasis on bitmap behavior, builder output checks, compilation/execution testing, and selected error-handling cases.

3. Syed Sayan Kabir Onan (24101501) - Contributed to testing and validation of the file-adder workflow, including multiple-file tests, boundary/edge-case checks, output inspection, and review of the final project files and README.

KNOWN LIMITATIONS / PROBLEMS
No known problems were found during the completed test suite. The implementation intentionally follows the project specification and therefore does not support subdirectories, deletion, renaming, indirect blocks, links, permissions, journaling, checksums, mounting, caching, or multi-level directory traversal.
