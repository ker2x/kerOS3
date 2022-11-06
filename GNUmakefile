.PHONY: all
all: limine basedirs basefiles

.PHONY: limine-clean
limine-clean:
	rm -rf limine

.PHONY: clean
clean: limine-clean
	rm -rf bin include bootloaders

.PHONY: basedirs
basedirs: bin include bootloaders

.PHONY: basefiles
basefiles : basedirs limine bin/limine-deploy include/limine.h bootloaders/BOOTX64.EFI bootloaders/limine-cd-efi.bin bootloaders/limine-cd.bin bootloaders/limine-hdd.bin bootloaders/limine.sys bootloaders/OVMF.fd

limine:
	git clone https://github.com/limine-bootloader/limine.git --branch=v4.x-branch --depth=1
	cd limine && ./bootstrap
	cd limine && ./configure --enable-uefi-x86-64 --enable-uefi-cd --enable-bios --enable-bios-cd
	$(MAKE) -C ./limine/

bin:
	mkdir -p bin

include:
	mkdir -p include

bootloaders:
	mkdir -p bootloaders

bin/limine-deploy: limine
	cp limine/bin/limine-deploy bin/

include/limine.h: limine
	cp limine/limine.h include/

bootloaders/BOOTX64.EFI: limine
	cp limine/bin/BOOTX64.EFI bootloaders/

bootloaders/limine-cd-efi.bin: limine
	cp limine/bin/limine-cd-efi.bin bootloaders/

bootloaders/limine-cd.bin: limine
	cp limine/bin/limine-cd.bin bootloaders/

bootloaders/limine-hdd.bin: limine
	cp limine/bin/limine-hdd.bin bootloaders/

bootloaders/limine.sys: limine
	cp limine/bin/limine.sys bootloaders/

bootloaders/OVMF.fd: 
	7z -y e ext/OVMF-X64.zip '-obootloaders/' OVMF.fd

# never called since i included it in the git repo but i keep it here for reference
ext/OVMF-X64.zip:
	curl -o ext/OVMF-X64.zip https://efi.akeo.ie/OVMF/OVMF-X64.zip
