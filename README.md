## EX. NO:2 IMPLEMENTATION OF PLAYFAIR CIPHER
PAVITHRA S
212223220072
 ## AIM:
To write a C program to implement the Playfair Substitution technique.
## DESCRIPTION:
The Playfair cipher starts with creating a key table. The key table is a 5×5 grid of letters that will act as the key for encrypting your plaintext. Each of the 25 letters must be unique and one letter of the alphabet is omitted from the table (as there are 25 spots and 26 letters in the alphabet).
To encrypt a message, one would break the message into digrams (groups of 2 letters) such that, for example, "HelloWorld" becomes "HE LL OW OR LD", and map them out on the key table. The two letters of the diagram are considered as the opposite corners of a rectangle in the key table. Note the relative position of the corners of this rectangle. Then apply the following 4 rules, in order, to each pair of letters in the plaintext:
1.	If both letters are the same (or only one letter is left), add an "X" after the first letter
2.	If the letters appear on the same row of your table, replace them with the letters to their immediate right respectively
3.	If the letters appear on the same column of your table, replace them with the letters immediately below respectively
4.	If the letters are not on the same row or column, replace them with the letters on the same row respectively but at the other pair of corners of the rectangle defined by the original pair.
## EXAMPLE:
![image](https://github.com/Hemamanigandan/EX-NO-2-/assets/149653568/e6858d4f-b122-42ba-acdb-db18ec2e9675)
## ALGORITHM:
STEP-1: Read the plain text from the user.
STEP-2: Read the keyword from the user.
STEP-3: Arrange the keyword without duplicates in a 5*5 matrix in the row order and fill the remaining cells with missed out letters in alphabetical order. Note that ‘i’ and ‘j’ takes the same cell.
STEP-4: Group the plain text in pairs and match the corresponding corner letters by forming a rectangular grid.
STEP-5: Display the obtained cipher text.
Program:
#include <stdio.h>
#include <string.h>
#define SIZE 5
char key[SIZE][SIZE] = 
{
    {'M','O','N','A','R'}, {'C','H','Y','B','D'},
    {'E','F','G','I','K'}, {'L','P','Q','S','T'},
    {'U','V','W','X','Z'}
};

void find(char ch, int *r, int *c) 
{
    for (int i = 0; i < SIZE*SIZE; i++)
        if (key[i/SIZE][i%SIZE] == ch) { *r = i/SIZE; *c = i%SIZE; return; }
}

void playfair(char *in, char *out, int enc) 
{
    int r1, c1, r2, c2, s = enc ? 1 : -1;
    for (int i = 0; in[i]; i += 2) 
    {
        find(in[i], &r1, &c1); find(in[i+1], &r2, &c2);
        if (r1 == r2)
            out[i] = key[r1][(c1 + s + SIZE) % SIZE],
            out[i+1] = key[r2][(c2 + s + SIZE) % SIZE];
        else if (c1 == c2)
            out[i] = key[(r1 + s + SIZE) % SIZE][c1],
            out[i+1] = key[(r2 + s + SIZE) % SIZE][c2];
        else
            out[i] = key[r1][c2], out[i+1] = key[r2][c1];
    }
    out[strlen(in)] = '\0';
}

int main() 
{
    char encrypted[100], decrypted[100];
    char text[] = "VARSHA";
    playfair(text, encrypted, 1);
    printf("Encrypted: %s\n", encrypted);
    playfair(encrypted, decrypted, 0);
    printf("Decrypted: %s\n", decrypted);
}
Output:
![446648831-bfdb8d5c-9958-477c-b518-87914a259c27](https://github.com/user-attachments/assets/b00874e2-ea2c-4781-8d66-4ca84f45bf0f)

