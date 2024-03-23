%.bin: %.asm
	nasm -f bin $< -o $@

loader.bin: loader.asm
	nasm -f bin loader.asm -o loader.bin

master.img: boot.bin loader.bin
	dd if=/dev/zero of=master.img bs=1M count=4
	dd if=boot.bin of=master.img bs=512 count=1
	dd if=loader.bin of=master.img bs=512 count=1 seek=2
	qemu-system-x86_64 master.img

clean:
	del boot.bin
	del master.img
