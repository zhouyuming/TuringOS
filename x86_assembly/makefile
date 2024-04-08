hello.bin: hello.asm
	nasm -f bin hello.asm -o hello.bin

master.img: hello.bin
	dd if=/dev/zero of=master.img bs=16M count=1
	dd if=hello.bin of=master.img bs=512 count=1 conv=notrunc

.PHONY: qemu
qemu: master.img
	qemu-system-i386 \
	-m 32M \
	-boot c \
	-hda $< \
	-rtc base=localtime -nographic

.PHONY: vdi
vdi: master.img
	qemu-img convert -f raw -O vdi master.img master.vdi	

.PHONY: clean
clean:
	rm -rf *.bin
