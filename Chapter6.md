Exercise 6-5. Write a function ``undef`` that will remove a name and definition from the table maintained by ``lookup`` and ``install``.
```c
void undef(char *name) {
    struct nlist *np, *pre;
    for (pre = NULL, np= hashtab[hash(name)]; np != NULL; pre = np, np = np->next) {
        if (strcmp(np->name, name) == 0) {
            if (pre != NULL) {
                pre->next = np->next;
            } else {
                hashtab[hash(name)] = np->next;
            }
            free((void *) np->name);
            free((void *) np->defn);
            free((void *) np);

            break;
        }
    }   
}
```