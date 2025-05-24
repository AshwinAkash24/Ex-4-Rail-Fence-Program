# Ex-5 Rail-Fence-Program
## Submitted By: Ashwin Akash M
## Reference Number: 212223230024
# AIM:
To write a C program to implement the rail fence transposition technique.

# DESCRIPTION:

In the rail fence cipher, the plain text is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

# ALGORITHM:

1. Input the plaintext message: Collect the secret message from the user (ignoring
spaces).
2. Set the number of rails: Input the number of rails (rows) for the zigzag pattern.
3. Initialize a 2D matrix (rail grid): Create a 2D array (matrix) to represent the rails,
initially filling it with spaces.
4. Fill the matrix in a zigzag pattern: Place the characters of the message into the
matrix in a zigzag pattern, alternating between downward and upward movements
across the rails.
5. Read the ciphertext row by row: Extract the characters from the matrix row by row
to form the encrypted message.
6. Output the ciphertext: Print the resulting encrypted message.

# PROGRAM
```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
void decrypt(char str[], int rails, int len) {
char code[rails][len];
int count = 0;
int i, j;
for(i = 0; i < rails; i++) {
for(j = 0; j < len; j++) {
code[i][j] = ' ';
}
}
int cycle = 2 * rails - 2;
for(i = 0; i < len; i++) {
int pos = i % cycle;
if (pos < rails) {
code[pos][i] = 'X';
} else {
code[cycle - pos][i] = 'X';
}
}
int k = 0;
for(i = 0; i < rails; i++) {
for(j = 0; j < len; j++) {
if (code[i][j] == 'X' && k < len) {
code[i][j] = str[k++];
}
}
}
char decrypted[len + 1];
int idx = 0;
for(count = 0; count < cycle; count++) {
int row = (count < rails) ? count : cycle - count;
for(i = 0; i < len; i++) {
if (code[row][i] != ' ') {
decrypted[idx++] = code[row][i];
}
}
}
decrypted[len] = '\0';
printf("Decrypted Message: %s\n", decrypted);
}
int main() {
int i, j, len, rails;
char str[1000];
printf("Enter a Secret Message: ");
fgets(str, sizeof(str), stdin);
str[strcspn(str, "\n")] = 0;
len = strlen(str);
printf("Enter number of rails: ");
scanf("%d", &rails);
char code[rails][len];
for(i = 0; i < rails; i++) {
for(j = 0; j < len; j++) {
code[i][j] = ' ';
}
}
int count = 0;
j = 0;
while (j < len) {
if (count % 2 == 0) {
for(i = 0; i < rails && j < len; i++) {
code[i][j] = str[j];
j++;
}
} else {
for(i = rails - 2; i > 0 && j < len; i--) {
code[i][j] = str[j];
j++;
}
}
count++;
}
printf("Ciphered Message: ");
for(i = 0; i < rails; i++) {
for(j = 0; j < len; j++) {
if (code[i][j] != ' ') {
printf("%c", code[i][j]);
}
}
}
printf("\n");
decrypt(str, rails, len);
return 0;
}
```
# OUTPUT
![Screenshot 2025-03-17 203810](https://github.com/user-attachments/assets/70a55632-484d-4c5c-9bd5-9a1854249b1e)
![Screenshot 2025-03-17 203829](https://github.com/user-attachments/assets/41a759b4-3473-4873-8398-2f049917c106)

# RESULT
The program is executed successfully
