# Ex-4 Rail-Fence-Program

# IMPLEMENTATION OF RAIL FENCE – ROW & COLUMN TRANSFORMATION TECHNIQUE

# AIM:
# To write a C program to implement the rail fence transposition technique.

# DESCRIPTION:

In the rail fence cipher, the plain text is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

# ALGORITHM:

STEP-1: Read the Plain text.
STEP-2: Arrange the plain text in row columnar matrix format.
STEP-3: Now read the keyword depending on the number of columns of the plain text.
STEP-4: Arrange the characters of the keyword in sorted order and the corresponding columns of the plain text.
STEP-5: Read the characters row wise or column wise in the former order to get the cipher text.

# PROGRAM
```
#include <stdio.h>
#include <string.h>

int main()
{
    char text[100], cipher[100], decrypt[100];
    char rail[10][100];
    int rails, len, i, j, row, dir, index;

    printf("Enter the Plain Text : ");
    fgets(text, sizeof(text), stdin);
    text[strcspn(text, "\n")] = '\0';
    printf("Enter the Number of Rails : ");
    scanf("%d", &rails);

    len = strlen(text);

    for(i = 0; i < rails; i++)
        for(j = 0; j < len; j++)
            rail[i][j] = '\n';
    row = 0;
    dir = 1;
    for(i = 0; i < len; i++)
    {
        rail[row][i] = text[i];

        if(row == 0)
            dir = 1;
        else if(row == rails - 1)
            dir = -1;

        row += dir;
    }
    index = 0;
    for(i = 0; i < rails; i++)
        for(j = 0; j < len; j++)
            if(rail[i][j] != '\n')
                cipher[index++] = rail[i][j];

    cipher[index] = '\0';
    printf("\nCipher Text : %s\n", cipher);

    for(i = 0; i < rails; i++)
        for(j = 0; j < len; j++)
            rail[i][j] = '\n';

    row = 0;
    dir = 1;
    for(i = 0; i < len; i++)
    {
        rail[row][i] = '*';

        if(row == 0)
            dir = 1;
        else if(row == rails - 1)
            dir = -1;

        row += dir;
    }
    index = 0;
    for(i = 0; i < rails; i++)
        for(j = 0; j < len; j++)
            if(rail[i][j] == '*')
                rail[i][j] = cipher[index++];

    row = 0;
    dir = 1;
    index = 0;
    for(i = 0; i < len; i++)
    {
        decrypt[index++] = rail[row][i];

        if(row == 0)
            dir = 1;
        else if(row == rails - 1)
            dir = -1;

        row += dir;
    }
    decrypt[index] = '\0';
    printf("Decrypted Text : %s\n", decrypt);
    return 0;
}
```

# OUTPUT

<img width="1590" height="730" alt="image" src="https://github.com/user-attachments/assets/49854678-90a2-4a01-987d-fd3e8b011d71" />


# RESULT

Thus the above C program for Rail Fence Cipher is executed successfully.
