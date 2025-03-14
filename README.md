# Rail Fence Cipher
Rail Fence Cipher using with different key values

# AIM:

To develop a simple C program to implement Rail Fence Cipher.

## DESIGN STEPS:

### Step 1:

Design of Rail Fence Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 
ALGORITHM DESCRIPTION:
In the rail fence cipher, the plaintext is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

## PROGRAM
```
Developed by : Karan A
Register number: 212223230099
```
```c
#include <stdio.h>
#include <string.h>

void encryptRailFence(char *text, int rails, char *cipher) {
    int len = strlen(text);
    char rail[rails][len];

    for (int i = 0; i < rails; i++)
        for (int j = 0; j < len; j++)
            rail[i][j] = '\0';

    int row = 0, step = 1;

    for (int i = 0; i < len; i++) {
        rail[row][i] = text[i];

        if (row == 0)
            step = 1;
        else if (row == rails - 1)
            step = -1;

        row += step;
    }

    int index = 0;
    for (int i = 0; i < rails; i++)
        for (int j = 0; j < len; j++)
            if (rail[i][j] != '\0')
                cipher[index++] = rail[i][j];
    
    cipher[index] = '\0';

    printf("Encrypted text: %s\n", cipher);
}

void decryptRailFence(char *cipher, int rails, char *plain) {
    int len = strlen(cipher);
    char rail[rails][len];

    for (int i = 0; i < rails; i++)
        for (int j = 0; j < len; j++)
            rail[i][j] = '\0';

    int row = 0, step = 1;

    for (int i = 0; i < len; i++) {
        rail[row][i] = '*';

        if (row == 0)
            step = 1;
        else if (row == rails - 1)
            step = -1;

        row += step;
    }

    int index = 0;
    for (int i = 0; i < rails; i++)
        for (int j = 0; j < len; j++)
            if (rail[i][j] == '*' && index < len)
                rail[i][j] = cipher[index++];

    row = 0, step = 1;
    for (int i = 0; i < len; i++) {
        plain[i] = rail[row][i];

        if (row == 0)
            step = 1;
        else if (row == rails - 1)
            step = -1;

        row += step;
    }
    plain[len] = '\0';

    printf("Decrypted text: %s\n", plain);
}

int main() {
    char str[1000], cipher[1000], decrypted[1000];
    int rails;

    printf("Enter a Secret Message: ");
    fgets(str, sizeof(str), stdin);
    str[strcspn(str, "\n")] = '\0';

    printf("Enter number of rails: ");
    scanf("%d", &rails);

    if (rails < 2) {
        printf("Number of rails must be at least 2.\n");
        return 1;
    }

    encryptRailFence(str, rails, cipher);
    decryptRailFence(cipher, rails, decrypted);

    return 0;
}
}
```
## OUTPUT:
![image](https://github.com/user-attachments/assets/a801e5ff-120c-4a17-bb7f-a5e104dc0300)

## RESULT:
The program is executed successfully
