# cryptography_19CS412_classical_techni
## CEASER CIPHER:

AIM : 

To implement the simple substitution technique named Caesar cipher using C
language.


ALGORITHM :

Step 1 : 

Read the plain text from the user.

Step 2 :
 Read the key value from the user

Step 3 :

If the key is positive then encrypt the text by adding the key with
each character in the plain text

Step 4 :

Else subtract the key from the plain text.

Step 5 :

Display the cipher text obtained above.


PROGRAM : 

```
#include<stdio.h>
#include <string.h>
#include<conio.h>
#include <ctype.h>
int main()
{
char plain[10], cipher[10];
int key,i,length;
int result;
printf("\n Enter the plain text:");
scanf("%s", plain);
printf("\n Enter the key value:");
scanf("%d", &key);
printf("\n \n \t PLAIN TEXt: %s",plain);
printf("\n \n \t ENCRYPTED TEXT: ");
for(i = 0, length = strlen(plain); i < length; i++)
{
cipher[i]=plain[i] + key;
if (isupper(plain[i]) && (cipher[i] > 'Z'))
cipher[i] = cipher[i] - 26;
if (islower(plain[i]) && (cipher[i] > 'z'))
cipher[i] = cipher[i] - 26;
printf("%c", cipher[i]);
}
printf("\n \n \t AFTER DECRYPTION : ");
for(i=0;i<length;i++)
{
plain[i]=cipher[i]-key;
if(isupper(cipher[i])&&(plain[i]<'A'))
plain[i]=plain[i]+26;
if(islower(cipher[i])&&(plain[i]<'a'))
plain[i]=plain[i]+26;
printf("%c",plain[i]);
}
return 0;
}
```
OUTPUT :

![image](https://github.com/manikandan26052004/cryptography_19CS412_classical_techni/assets/121999845/22af8f1f-e114-42b8-b673-d55ef22c2ba9)



RESULT : 

Thus the implementation of Caesar cipher had been executed successfully


## PLAYFAIR CIPHER: 

AIM :

To write a C program to implement the Playfair Substitution technique.

ALGORITHM :

Step 1 :

Read the plain text from the user

Step 2 :

Read the keyword from the user 

Step 3 :

Arrange the keyword without duplicates in a 5*5 matrix in the row
 
order and fill the remaining cells with missed out letters in

alphabetical order. Note that ‘i’ and ‘j’ takes the same cell. 

Step 4 :

Group the plain text in pairs and match the corresponding corner

letters by forming a rectangular grid.

step 5 :

Display the obtained cipher text

PROGRAM : 

```
def prepare_input_text(text):
    # Remove spaces and convert to uppercase
    text = text.replace(" ", "").upper()
    # If text length is odd, add a trailing 'X' to make it even
    if len(text) % 2 != 0:
        text += 'X'
    return text

def generate_key_matrix(key):
    # Remove spaces and convert to uppercase
    key = key.replace(" ", "").upper()
    # Initialize key matrix with 5x5 dimension
    key_matrix = []
    # Populate key matrix with unique characters from the key
    for char in key:
        if char not in key_matrix and char != 'J':
            key_matrix.append(char)
    # Fill remaining matrix positions with other characters
    alphabet = 'ABCDEFGHIKLMNOPQRSTUVWXYZ'
    for char in alphabet:
        if char not in key_matrix:
            key_matrix.append(char)
    return key_matrix

def generate_playfair_table(key_matrix):
    # Generate 5x5 playfair table
    table = [key_matrix[i:i+5] for i in range(0, 25, 5)]
    return table

def find_char_position(matrix, char):
    # Find position of character in the playfair table
    for i in range(5):
        for j in range(5):
            if matrix[i][j] == char:
                return i, j

def playfair_encrypt(plaintext, key):
    # Prepare input text and generate key matrix
    plaintext = prepare_input_text(plaintext)
    key_matrix = generate_key_matrix(key)
    table = generate_playfair_table(key_matrix)
    ciphertext = ''
    # Encrypt pairs of letters
    for i in range(0, len(plaintext), 2):
        char1, char2 = plaintext[i], plaintext[i+1]
        row1, col1 = find_char_position(table, char1)
        row2, col2 = find_char_position(table, char2)
        # Case 1: Same row, shift to the right
        if row1 == row2:
            ciphertext += table[row1][(col1+1)%5] + table[row2][(col2+1)%5]
        # Case 2: Same column, shift downwards
        elif col1 == col2:
            ciphertext += table[(row1+1)%5][col1] + table[(row2+1)%5][col2]
        # Case 3: Form a rectangle, swap column positions
        else:
            ciphertext += table[row1][col2] + table[row2][col1]
    return ciphertext

def playfair_decrypt(ciphertext, key):
    # Prepare input text and generate key matrix
    ciphertext = prepare_input_text(ciphertext)
    key_matrix = generate_key_matrix(key)
    table = generate_playfair_table(key_matrix)
    plaintext = ''
    # Decrypt pairs of letters
    for i in range(0, len(ciphertext), 2):
        char1, char2 = ciphertext[i], ciphertext[i+1]
        row1, col1 = find_char_position(table, char1)
        row2, col2 = find_char_position(table, char2)
        # Case 1: Same row, shift to the left
        if row1 == row2:
            plaintext += table[row1][(col1-1)%5] + table[row2][(col2-1)%5]
        # Case 2: Same column, shift upwards
        elif col1 == col2:
            plaintext += table[(row1-1)%5][col1] + table[(row2-1)%5][col2]
        # Case 3: Form a rectangle, swap column positions
        else:
            plaintext += table[row1][col2] + table[row2][col1]
    return plaintext

# Test the functions
plaintext = "MANIKANDAN"
key = "PLAYFAIR EXAMPLE"
ciphertext = playfair_encrypt(plaintext, key)
print("Encrypted text:", ciphertext)
decrypted_text = playfair_decrypt(ciphertext, key)
print("Decrypted text:", decrypted_text)


```
OUTPUT :


![Screenshot 2024-03-01 135932](https://github.com/manikandan26052004/Cryptography---19CS412-classical-techqniques/assets/121999845/a818393f-950a-4992-94f8-2bf21ccb734d)



RESULT :
 Thus the Playfair cipher substitution technique had been implemented successfully.



## HILL CIPHER 

AIM : 

To write a C program to implement the hill cipher substitution techniques.

ALGORITHM :

Step 1 :

Read the plain text and key from the user.

Step 2 :

Split the plain text into groups of length three


Step 3 :

Arrange the keyword in a 3*3 matrix.

Step 4 :

Multiply the two matrices to obtain the cipher text of length three.

Step 5 :

Combine all these groups to get the complete cipher text.


PROGRAM :

```
#include<stdio.h>
#include<conio.h>
#include<string.h>
int main(){
unsigned int a[3][3]={{6,24,1},{13,16,10},{20,17,15}};
unsigned int b[3][3]={{8,5,10},{21,8,21},{21,12,8}};
int i,j, t=0;
unsigned int c[20],d[20];
char msg[20];
printf("Enter plain text: ");
scanf("%s",msg);
for(i=0;i<strlen(msg);i++)
{
c[i]=msg[i]-65;
unsigned int a[3][3]={{6,24,1},{13,16,10},{20,17,15}};
unsigned int b[3][3]={{8,5,10},{21,8,21},{21,12,8}};
printf("%d ",c[i]);
}
for(i=0;i<3;i++)
{ t=0;
for(j=0;j<3;j++)
{
t=t+(a[i][j]*c[j]);
}
d[i]=t%26;
}
printf("\nEncrypted Cipher Text :");
for(i=0;i<3;i++)
printf(" %c",d[i]+65);
for(i=0;i<3;i++)
{
t=0;
for(j=0;j<3;j++)
{
t=t+(b[i][j]*d[j]);
}
c[i]=t%26;
}
printf("\nDecrypted Cipher Text :");
for(i=0;i<3;i++)
printf(" %c",c[i]+65);
getch();
return 0;
}
```

OUTPUT :

![image](https://github.com/manikandan26052004/cryptography_19CS412_classical_techni/assets/121999845/1c004e63-87d7-4419-8061-ad53a351cd8a)



RESULT :

 Thus the hill cipher substitution technique had been implemented successfully


## Vigenere Cipher 


AIM : 

To implement the Vigenere Cipher substitution technique using C program


ALGORITHM :

Step 1 :

Arrange the alphabets in row and column of a 26*26 matrix

Step 2 : 

Circulate the alphabets in each row to position left such that the first letter

is attached to last.

Step 3 :

Repeat this process for all 26 rows and construct the final key matrix.

Step 4 :

The keyword and the plain text is read from the user.

Step 5 :

The characters in the keyword are repeated sequentially so as to

match with that of the plain text.

Step  6 :

 Pick the first letter of the plain text and that of the keyword as the row
 
indices and column indices respectively.

Step 7 :

The junction character where these two meet forms the cipher character

Step 8 :

Repeat the above steps to generate the entire cipher text.

PROGRAM :

```
#include <stdio.h>
#include<conio.h>
#include <ctype.h>
#include <string.h>
void encipher();
void decipher();
int main()
{
int choice;
while(1)
{
printf("\n1. Encrypt Text");
printf("\n2. Decrypt Text");
printf("\n3. Exit");
printf("\n\nEnter Your Choice : ");
scanf("%d",&choice);
if(choice == 3)
exit(0);
else if(choice == 1)
encipher();
else if(choice == 2)
decipher();
else
printf("Please Enter Valid Option.");
}
}
void encipher()
{
unsigned int i,j;
char input[50],key[10];
printf("\n\nEnter Plain Text: ");
scanf("%s",input);
printf("\nEnter Key Value: ");
scanf("%s",key);
printf("\nResultant Cipher Text: ");
for(i=0,j=0;i<strlen(input);i++,j++)
{
if(j>=strlen(key))
{ j=0;
}
printf("%c",65+(((toupper(input[i])-65)+(toupper(key[j])-
65))%26));
}}
void decipher()
{
unsigned int i,j;
char input[50],key[10];
int value;
printf("\n\nEnter Cipher Text: ");
scanf("%s",input);
printf("\n\nEnter the key value: ");
scanf("%s",key);
for(i=0,j=0;i<strlen(input);i++,j++)
{
if(j>=strlen(key))
{ j=0; }
value = (toupper(input[i])-64)-(toupper(key[j])-64);
if( value < 0)
{ value = value * -1;
}
printf("%c",65 + (value % 26));
}
return 0;
}
```

OUTPUT :

![image](https://github.com/manikandan26052004/cryptography_19CS412_classical_techni/assets/121999845/cadb5c98-a6a3-48bc-9950-50c990c9b3df)


RESULT :

Thus , The program is executed perfectly and output is verified.


## Rail Fence Cipher

AIM :

To write a C program to implement the rail fence transposition technique.


ALGORRITHM :

Step 1 :

Read the Plain text.


Step 2 :

Arrange the plain text in row columnar matrix format

Step 3 :

Now read the keyword depending on the number of columns of the plain text

Step 4 :

Arrange the characters of the keyword in sorted order and the

corresponding columns of the plain text.

Step 5 :

Read the characters row wise or column wise in the former order to get the

cipher text.

PROGRAM :

```
#include<stdio.h>
#include<conio.h>
#include<string.h>
int main()
{
int i,j,k,l;
char a[20],c[20],d[20];
printf("\n\t\t RAIL FENCE TECHNIQUE");
printf("\n\nEnter the input string : ");
gets(a);
l=strlen(a);
/Ciphering/
for(i=0,j=0;i<l;i++)
{
if(i%2==0)
c[j++]=a[i];
}
for(i=0;i<l;i++)
{
if(i%2==1)
c[j++]=a[i];
}
c[j]='\0';
printf("\nCipher text after applying rail fence :");
printf("\n%s",c);
/Deciphering/
if(l%2==0)
k=l/2;
else
k=(l/2)+1;
for(i=0,j=0;i<k;i++)
{
d[j]=c[i];
j=j+2;
}
for(i=k,j=1;i<l;i++)
{
d[j]=c[i];
j=j+2;
}
d[l]='\0';
printf("\nText after decryption : ");
printf("%s",d);
return 0;
}
```


OUTPUT :
![image](https://github.com/manikandan26052004/cryptography_19CS412_classical_techni/assets/121999845/ca3ca0cd-d841-4ad7-aa10-302db70efeb9)



RESULT :

Thus the rail fence algorithm had been executed successfully

