.PHONY: all
all: limine bin include bootloaders

# Download & compile limine
limine:
	git clone https://github.com/limine-bootloader/limine.git --branch=v4.x-branch --depth=1
	cd limine && ./bootstrap
	cd limine && ./configure --enable-uefi-x86-64 --enable-uefi-cd --enable-bios --enable-bios-cd
	$(MAKE) -C ./limine/



# move useful bin stuff to bin/
bin: limine
	mkdir bin
	cp limine/bin/limine-deploy bin/
	#cp limine/bin/limine-version bin/
	
# move useful .h stuff to include/
include: limine
	mkdir include
	cp limine/limine.h include/

# move the limine bootloaders to bootloaders/
# download and extract OVMF.fd
bootloaders: limine
	mkdir bootloaders
	cp limine/bin/BOOTX64.EFI bootloaders/
	cp limine/bin/limine-cd-efi.bin bootloaders/
	cp limine/bin/limine-cd.bin bootloaders/
	cp limine/bin/limine-hdd.bin bootloaders/
	cp limine/bin/limine.sys bootloaders/
	curl -o OVMF-X64.zip https://efi.akeo.ie/OVMF/OVMF-X64.zip
	7z -y e OVMF-X64.zip '-obootloaders/' OVMF.fd
	rm -f OVMF-X64.zip

.PHONY: limine-clean
limine-clean:
	rm -rf limine

.PHONY: clean
clean: limine-clean
	rm -rf bin include bootloaders