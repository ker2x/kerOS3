.PHONY: all
all: limine basedirs basefiles

# Download & compile limine
limine:
	git clone https://github.com/limine-bootloader/limine.git --branch=v4.x-branch --depth=1
	cd limine && ./bootstrap
	cd limine && ./configure --enable-uefi-x86-64 --enable-uefi-cd --enable-bios --enable-bios-cd
	$(MAKE) -C ./limine/

.PHONY: basedirs
basedirs: bin include bootloaders

bin:
	mkdir -p bin

include:
	mkdir -p include

bootloaders:
	mkdir -p bootloaders

.PHONY: basefiles
basefiles : basedirs limine bin/limine-deploy include/limine.h bootloaders/BOOTX64.EFI bootloaders/limine-cd-efi.bin bootloaders/limine-cd.bin bootloaders/limine-hdd.bin bootloaders/limine.sys bootloaders/OVMF.fd

bin/limine-deploy:
	cp limine/bin/limine-deploy bin/

include/limine.h: 
	cp limine/limine.h include/

bootloaders/BOOTX64.EFI:
	cp limine/bin/BOOTX64.EFI bootloaders/

bootloaders/limine-cd-efi.bin:
	cp limine/bin/limine-cd-efi.bin bootloaders/

bootloaders/limine-cd.bin:
	cp limine/bin/limine-cd.bin bootloaders/

bootloaders/limine-hdd.bin:
	cp limine/bin/limine-hdd.bin bootloaders/

bootloaders/limine.sys:
	cp limine/bin/limine.sys bootloaders/

bootloaders/OVMF.fd: 
	7z -y e ext/OVMF-X64.zip '-obootloaders/' OVMF.fd
	#touch bootloaders/OVMF.fd

ext/OVMF-X64.zip:
	curl -o ext/OVMF-X64.zip https://efi.akeo.ie/OVMF/OVMF-X64.zip

.PHONY: limine-clean
limine-clean:
	rm -rf limine

.PHONY: clean
clean: limine-clean
	rm -rf bin include bootloaders