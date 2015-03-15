# Cheip

Source of the program:

```c
#include <stdio.h>
#include <stdlib.h>

void backdoor() {
	execl("/bin/cat", "/bin/cat", "/home/cheip/flag", 0);
}

void bof(char *str) {
	char buf[256];
	strcpy(buf, str);
}

int main(int argc, char *argv[]) {
	char cmp[]="can_you_do_bof";
	if(argc != 2) {
		exit(0);
	}
	if(strncmp(argv[1], cmp, strlen(cmp))!=0) {
		exit(0);
	}
	bof(argv[1]);
}
```

To get past the first check, we start the argument with "can_you_do_bof".
Getting the address of `backdoor` with `x/x backdoor` in `gdb` and overwriting
the return address with the buffer overflow gets us the flag.
