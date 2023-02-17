Exercise 1-2. Experiment to find out what happens when printf’s argument string contains \c, where c is some character not listed above.
```c
int main() {
    printf("hello\c, world\n");
}
```

Exercise 1-8. Write a program to count blanks, tabs, and newlines.
```c
#include <stdio.h>

int main() {
    int nb, nt, nl, nc, c;
    
    nb = nt = nl = nc = 0;
    while ((c = getchar()) != EOF) {
        nc++;
        if (c == ' ') {
            nb++;
        } 
        if (c == '\t') {
            nt++;
        } 
        if (c == '\n') {
            nl++;
        }
    }

    printf("spaces: \d\n", nb);
    printf("tabs: \d\n", nt);
    printf("newlines: \d\n", nl);
    printf("chars: \d\n", nc);    
}
```

Exercise 1-9. Write a program to copy its input to its output, replacing each string of one or more blanks by a single blank.
```c
#include <stdio.h>

int main() {
    int c, space;
    
    space = 0;
    while ((c = getchar()) != EOF) {
        if (c != ' ') {
            if (space != 0) {
                putchar(' ');
            }
            space = 0;
            putchar(c);
        } else {
            if (space == 0) {
                space = 1;
            } 
        }
    }
}
```

Exercise 1-10. Write a program to copy its input to its output, replacing each tab by \t, each backspace by \b, and each backslash by \\. This makes tabs and backspaces visible in an unambiguous way.
```c
#include <stdio.h>

int main() {
    int c;
    while ((c = getchar()) != EOF) {
        if ('\t' == c) {
            printf("\\t");
        } else if (' ' == c)  {
            printf("\\b");
        } else if ('\\' == c) {
            printf("\\\\");
        } else {
            putchar(c);
        }
    }
}
```

Exercise 1-12. Write a program that prints its input one word per line.
```c
#include <stdio.h>

#define WRD 0
#define SPC 1

int main() {
    int state, c;
    
    while ((c = getchar()) != EOF) {
        if (c != ' ' && c != '\t' && c != '\n') {
            state = WRD;
            putchar(c);
        } else {
            if (state == WRD) {
                putchar('\n');
            }
            state = SPC;
        }
    }
}
```

Exercise 1-13. Write a program to print a histogram of the lengths of words in its input. It is easy to draw the histogram with the bars horizontal; a vertical orientation is more challenging.
```c
#include <stdio.h>

#define MAXLEN 20

int main() {
    int c, len, wc, word[MAXLEN+1];

    for (int i = 1; i <= MAXLEN; i++) {
        word[i] = 0;
    }

    wc = 0;
    len = 0;
    while ((c = getchar()) != EOF) {
        if (c != ' ' && c != '\t' && c != '\n') { 
            len++;
        } else {
            if (len > 0) {
                word[len]++;
                len = 0;
                wc++;
            }
        }
    }

    // Since it's nonsense to talk about word of length zero, it can be used to represent total count
    word[0] = wc;

    for (int i = wc; i >= 0; i--) {
        if (i != 0) {
            printf("%3d ", i);            
        } else {
            putchar(' ');
            putchar(' ');
            putchar(' ');
            putchar(' ');
        }

        for (int j = 0; j <= MAXLEN; j++) {
            if (i != 0) {
                putchar(' ');
                putchar(' ');
                if (i > word[j]) {
                    putchar(' ');
                } else {
                    putchar('*');
                }
            } else {
                printf("%3d", j);
            }
            if (j == MAXLEN) {
                putchar('\n');
            }
             
        } 
    }
}
```
