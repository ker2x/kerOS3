# kerOS3
an operating system for (my) training purpose

## random note

```
# in windows WSL
git subtree add --prefix limine https://github.com/limine-bootloader/limine.git v4.x-branch
cd limine
sudo apt install automake autoconf nasm mtools xorriso
./bootstrap
./configure --enable-uefi-x86-64 --enable-uefi-cd --enable-bios --enable-bios-cd
make
sudo make install
cd ..
git subtree add --prefix os/limine-barebones https://github.com/limine-bootloader/limine-barebones.git
```