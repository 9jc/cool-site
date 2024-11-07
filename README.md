
______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

 EXCERCISE 3 - WRITE A PROGRAM TO IMPLEMENT RABIN-MILLER PRIMALITY TESTING ALGORITHM IN C
______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________


```c
#include<stdio.h>
#include <stdlib.h>
#include<conio.h>

int power(int x, unsigned int y, int p) 
{
    int res = 1;
    x = x % p;
    while (y > 0) 
    {
        if (y & 1)
            res = (res * x) % p;
        y = y >> 1;
        x = (x * x) % p;
    }
    return res;
}

int millerTest(int d, int n) 
{
    int a = rand() % (n - 4) + 2;
    int x = power(a, d, n);
    if (x == 1 || x == n - 1)
        return 1;

    while (d != n - 1) 
    {
        x = (x * x) % n;
        d *= 2;

        if (x == 1) return 0;
        if (x == n - 1) return 1;
    }
    return 0;
}

int IsPrime(int n, int k) 
{
    int d, i;

    if (n < 1 || n == 4) return 0;
    if (n <= 3) return 1;

    d = n - 1;
    while (d % 2 == 0)
        d /= 2;

    for (i = 0; i < k; i++)
        if (!millerTest(d, n))
            return 0;

    return 1;
}

void main() 
{
    int k = 4;
    int n;
    printf("Enter the number: ");
    scanf("%d", &n);
    if (IsPrime(n, k))
        printf("Given number is Prime\n");
    else
        printf("Given number is not Prime\n");

    getch();
}
```


_______________

SAMPLE OUTPUT  :
_______________

Enter the number: 17
Given number is Prime


______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

EXCERCISE 4 - WRITE A PROGRAM TO IMPLEMENT THE EUCLID ALGORITHM TO GENERATE THE GCD OF AN ARRAY OF 10 INTEGERS IN C 
______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________


```c
#include<stdio.h>
#include<conio.h>

int gcd (int a,int b)
{
	if(a==0)
		return b;
	return gcd (b%a,a);
}

void main()
{
	int a[10],i,result;
	clrscr();
    
	for (i=0;i<10;i++)
	{
		printf("Enter the %d term",i+1);
		scanf("%d",&a[i]);
		
		if(i==0)
			result=a[0];
		result=gcd(result,a[i]);
	}
    
	printf(" The GCD of the Number is %d",result);
	getch();
}
```


_______________

SAMPLE OUTPUT  :
_______________

Enter the 1st term: 12
Enter the 2nd term: 6
Enter the 3rd term: 9
Enter the 4th term: 15
Enter the 5th term: 3
Enter the 6th term: 6
Enter the 7th term: 9
Enter the 8th term: 12
Enter the 9th term: 3
Enter the 10th term: 15

The GCD of the Numbers is 3


____________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

EXCERCISE 5.B - WRITE A JAVA PROGRAM TO PERFORM ENCRYPTION AND DECRYPTION USING THE ALGORITHM: B) SUBSTITUTION CIPHER 
__________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________


```java
import java.io.*;
import java.util.*;

public class substituteCipher
{
	public static void main(String args[])
	{
		Scanner sc = new Scanner(System.in);
		
		String a = "abcdefghijklmnopqrstuvwxyz";
		String b = "zyxwvutsrqponmlkjihgfedcba";
		
		System.out.print("Enter the data: ");
		String  str = sc.next();
		
		String encrypt = "";
		String decrypt = "";
		
		char c;
		
		for(int i=0; i<str.length(); i++)
		{
			c = str.charAt(i);
			int j = a.indexOf(c);
			encrypt = encrypt + b.charAt(j);
		}
		
		System.out.println("Encrypted data is: " +encrypt);
		
		for(int i=0; i<encrypt.length(); i++)
		{
			c = encrypt.charAt(i);
			int j = b.indexOf(c);
			decrypt = decrypt + a.charAt(j);
		}
		
		System.out.println("decrypted data is: " +decrypt);

	}
}
```


_______________

SAMPLE OUTPUT  :
_______________

>>  javac substituteCipher.java
>>  java substituteCipher

Enter the message: security
Encrypted message is: hvxfirgb
Decrypted message is: security


__________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

EXCERCISE 9 - WRITE A JAVA PROGRAM TO IMPLEMENT THE RIJNDAEL ALGORITHM LOGIC
__________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________-


```java
import javax.crypto.*;
import java.io.*;
import javax.crypto.spec.*;
import java.util.Scanner;

class RIJalgorithm 
{ 
    private static String asHex(byte buf[]) 
    {
        StringBuffer strbuf = new StringBuffer(buf.length * 2);
		
        int i;
		
	for (i = 0; i < buf.length; i++)
        {
            if (((int) buf[i] & 0xff) < 0x10)
            {
                strbuf.append("0");
            }
            strbuf.append(Long.toString((int) buf[i] & 0xff, 16));
        }
        return strbuf.toString();
    }

    public static void main(String[] args) throws Exception
    {
        String msg = "Helloworld";
        String a = msg.toString();

        KeyGenerator kgen = KeyGenerator.getInstance("AES");
        kgen.init(128); 
        
        SecretKey skey = kgen.generateKey();
        byte[] raw = skey.getEncoded();
        SecretKeySpec skeySpec = new SecretKeySpec(raw, "AES");
        Cipher cipher = Cipher.getInstance("AES");
        
        cipher.init(Cipher.ENCRYPT_MODE, skeySpec);
        byte[] encrypted = cipher.doFinal((args.length == 0 ? a : args[0]).getBytes());
        System.out.println("Encrypted String: --------> " + asHex(encrypted));
        
        cipher.init(Cipher.DECRYPT_MODE, skeySpec);
        byte[] original = cipher.doFinal(encrypted);
        String originalString = new String(original);
        System.out.println("Original String in Hexadecimal: ------> " + asHex(original));
        System.out.println("Original String: ----> " + originalString);
    }
}
```


_______________

SAMPLE OUTPUT  :
_______________

>>  javac RIJalgorithm.java
>>  java RIJalgorithm 

Encrypted String: --------> 97e6e73d9f50e2637fa503217adc43e9
Original String in Hexadecimal: ------> 48656c6c6f776f726c64
Original String: ----> Helloworld


__________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

EXCERCISE 11 - WRITE A JAVA PROGRAM TO IMPLEMENT RSA ALGORITHM 
__________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________


```java
import java.util.*;
import java.math.*;

class RSA 
{
    public static void main(String args[]) 
    {
        Scanner sc = new Scanner(System.in);

        int p, q, n, z, d = 0, e, i;
        double c;
        BigInteger msgback;

        System.out.print("Enter the Number to be Encrypted and Decrypted : ");
        int msg = sc.nextInt();

        System.out.print("Enter 1st prime number p : ");
        p = sc.nextInt();
        System.out.print("Enter 2nd prime number q : ");
        q = sc.nextInt();

        n = p * q;
        z = (p - 1) * (q - 1);
        System.out.println("The value of z : " + z);

        for (e = 2; e < z; e++) 
        {
            if (gcd(e, z) == 1) 
            {
                break;
            }
        }
        System.out.println("The value of e : " + e);

        for (i = 0; i <= 9; i++) 
        {
            int x = 1 + (i * z);
            if (x % e == 0) 
            {
                d = x / e;
                break;
            }
        }
        System.out.println("The value of d : " + d);

        c = (Math.pow(msg, e)) % n;
        System.out.print("Encrypted message is : ");
        System.out.println(c);

        BigInteger N = BigInteger.valueOf(n);
        BigInteger C = BigDecimal.valueOf(c).toBi4gInteger();
        msgback = (C.pow(d)).mod(N);
        System.out.print("Decrypted message is : ");
        System.out.println(msgback);

    }

    static int gcd(int e, int z) 
    {
        if (e == 0)
            return z;
        else
            return gcd(z % e, e);
    }
}
```


_______________

SAMPLE OUTPUT  :
_______________

>> javac RSA.java
>> java RSA

Enter the number to be encrypted and decrypted : 4
Enter 1st prime number p : 3
Enter 2nd prime number q : 7

The value of z : 12
The value of e : 5
The value of d : 5

Encrypted message is : 16.0
Decrypted message is : 4


__________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

EXCERCISE 12 - CALCULATE THE MESSAGE DIGEST OF A TEXT USING THE SHA - 1 ALGORITHM IN JAVA 
__________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

 
```java
import java.math.BigInteger;
import java.security.MessageDigest;
import java.security.NoSuchAlgorithmException;

public class SHA 
{
    public static String encryptThisString(String input) 
    {
        try 
	{
            MessageDigest md = MessageDigest.getInstance("SHA-1");

            byte[] messageDigest = md.digest(input.getBytes());

            BigInteger no = new BigInteger(1, messageDigest);

            String hashtext = no.toString(16);

            while (hashtext.length() < 32) 
	    {
                hashtext = "0" + hashtext;
            }

            return hashtext;
        } 
        catch (NoSuchAlgorithmException e) 
        {
            throw new RuntimeException(e);
        }
    }


    public static void main(String args[]) throws NoSuchAlgorithmException 
    {
        System.out.println("Hash Code Generated by SHA-1 for: ");
        String s1 = "cybersecurity ";
        System.out.println("\n" + s1 + " : " + encryptThisString(s1));

        String s2 = "computerscience ";
        System.out.println("\n" + s2 + " : " + encryptThisString(s2));
    }
}
```


_______________

SAMPLE OUTPUT  :
_______________


>> javac SHA.java
>> java SHA

Hash Code Generated by SHA-1 For:

cybersecurity  : b09e29e4377e9442c7e9a81aa8e4cf4fca105668

computerscience  : c602fc3cecd5cdab092e4a6695aaf1ce2f97d012


__________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________




