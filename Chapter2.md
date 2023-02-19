Exercise 2-4. Write an alternate version of squeeze(s1, s2) that defines each character in s1 that matches any character in the string s2.
```c
void sequeeze(char s[], char c[]) {
    int i, j;

    for (i = j = 0; s[i] != '\0'; i++) {
        int match = 0;

        for (int k = 0; c[k] != '\0'; k++) {
            if (s[i] == c[k]) {
                match = 1;
            }
        }
        if (!match) {
            s[j++] = s[i];
        }
    }
    s[j++] = '\0';
}
```

Exercise 2-5. Write the function any(s1, s2), which returns the first location in the string s1 where any character from the string s2 occurs, or -1 if s1 contains no characters from s2. (The standard library function strpbrk does the same job but returns a pointer to the location.)
```c
int any(char s1[], char s2[]) {
    for (int i, j = 0; s1[i] != '\0' && s2[j] != '\0'; i++, j++) {
        if (s1[i] == s2[j]) {
            return i;
        }
    }

    return -1;
}
```