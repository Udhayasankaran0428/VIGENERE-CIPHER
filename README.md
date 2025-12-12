# EX. NO: 4 IMPLEMETATION OF VIGENERE CIPHER
 
## AIM:
To implement the Vigenere Cipher substitution technique using C program.

## DESCRIPTION:

To encrypt, a table of alphabets can be used, termed a tabula recta, Vigenère square,or Vigenère table. It consists of the alphabet written out 26 times in differnt rows, each alphabet shifted cyclically to the left compared to the previous alphabet, corresponding to the 26 possible Caesar ciphers. At different points in the encryption process, the cipher uses adifferent alphabet from one of the rows. The alphabet used at each point repeating keyword.depends on a Each row starts with a key letter. The remainder of the row holds the letters A to Z. Although there are 26 key rows shown, you will only use as many keys as there are unique letters in the key string, here just 5 keys, {L, E, M, O, N}. For successive letters of the message, we are going to take successive letters of the key string, and encipher each message letter using its corresponding key row. Choose the next letter of the key, go along that row to find the column heading that	atches the message character; the letter at the intersection of
[key-row, msg-col] is the enciphered letter.

## ALGORITHM:

STEP-1: Arrange the alphabets in row and column of a 26*26 matrix.

STEP-2: Circulate the alphabets in each row to position left such that the first letter is attached to last.

STEP-3: Repeat this process for all 26 rows and construct the final key matrix.

STEP-4: The keyword and the plain text is read from the user.

STEP-5: The characters in the keyword are repeated sequentially so as to match with that of the plain text.

STEP-6: Pick the first letter of the plain text and that of the keyword as the row indices and column indices respectively.

STEP-7: The junction character where these two meet forms the cipher character.

STEP-8: Repeat the above steps to generate the entire cipher text.

## PROGRAM:
```
#include <stdio.h>
#include <ctype.h>
#include <string.h>

static void strip(char *s){ size_t n=strcspn(s,"\n"); s[n]=0; }

int main(void){
    int choice;
    char t[128], k[128];
    for(;;){
        puts("\n1. Encrypt Text 2. Decrypt Text 3. Exit");
        printf("\nEnter Your Choice : ");
        if (scanf("%d",&choice)!=1) break;
        while(getchar()!='\n');              /* flush newline */

        if(choice==3) break;

        if(choice==1){
            printf("\nEnter Plain Text: ");
            if(!fgets(t,sizeof t,stdin)) break; strip(t);
            printf("\nEnter Key Value: ");
            if(!fgets(k,sizeof k,stdin)) break; strip(k);

            printf("\nResultant Cipher Text: ");
            for(size_t i=0,j=0;i<strlen(t);++i){
                char p = toupper((unsigned char)t[i]);
                if(p<'A'||p>'Z'){ putchar(t[i]); continue; }
                char key = toupper((unsigned char)k[j++%strlen(k)]);
                putchar((char)(((p-'A') + (key-'A'))%26 + 'A'));
            }
            putchar('\n');
        }
        else if(choice==2){
            printf("\nEnter Cipher Text: ");
            if(!fgets(t,sizeof t,stdin)) break; strip(t);
            printf("\n\nEnter the key value: ");
            if(!fgets(k,sizeof k,stdin)) break; strip(k);

            for(size_t i=0,j=0;i<strlen(t);++i){
                char c = toupper((unsigned char)t[i]);
                if(c<'A'||c>'Z'){ putchar(t[i]); continue; }
                char key = toupper((unsigned char)k[j++%strlen(k)]);
                putchar((char)(((c-'A') + 26 - (key-'A'))%26 + 'A'));
            }
            putchar('\n');
        }
        else puts("Please Enter Valid Option.");
    }
    return 0;
}
```
## OUTPUT:
<img width="457" height="650" alt="image" src="https://github.com/user-attachments/assets/46f8d0c4-1f7c-44af-8bec-ca94d4bbf491" />

## RESULT:
The program is executed successfully
