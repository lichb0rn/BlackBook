---
aliases: ["xor", "исключающее или"]
---
MOC:  [[Software Development MOC]]

---

Исключающее ИЛИ работает так:
- если оба бита идентичны, то возвращает $0$.
- если биты различные - $1$.

| a | b | XOR
| :-:  | :-: | :-:
| 0 | 0 | 0
| 1 |  0|  1
| 0 | 1 | 1
| 1 | 1 | 0

Повторное применение XOR возвращает значение переменной:
```c
char *binbin(int n);

int main()
{
    int a, b, r;
    a = 73;
    b = 170;
    r = a ^ b;

    printf("  \t%s\t%d\n", binbin(a), a);
    printf("^ \t%s\t%d\n", binbin(b), b);
    printf("= \t%s\t%d\n", binbin(r), r);

    a = r ^ b;
    printf("^ \t%s\t%d\n", binbin(b), b);
    printf("= \t%s\t%d\n", binbin(a), a);
    return 0;
}

char *binbin(int n)
{
    static char bin[17];
    int x;
    for (x = 0; x < 8; x++)
    {
        bin[x] = n & 0x80 ? '1' : '0';
        n <<= 1;
    }
    bin[x] = '\0';
    return bin;
}

        01001001        73
^       10101010        170
=       11100011        227
^       10101010        170
=       01001001        73

```

