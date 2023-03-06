Exercise 7-1. Write a program that converts upper case to lower or lower case to upper, depending on the name it is invoked with, as found in ``argv[0]``.
```c
#include <stdio.h>
#include <ctype.h>
#include <string.h>

int main(int argc, char* argv[]) {
    int c;

    /* The binary should only be installed as toupper and tolower */
    int (*f)(int) = strcmp("toupper", argv[0]) == 0 ? toupper : tolower; 

    while ((c = getchar()) != EOF) {
        putchar(f(c));
    }

    return 0;
}
```