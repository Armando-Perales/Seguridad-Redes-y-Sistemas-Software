## Objetivo
This vault uses ASCII encoding for the password. The source code for this vault is here: [VaultDoor4.java](https://jupiter.challenges.picoctf.org/static/09d3002ae349631324a17e2255ae8df2/VaultDoor4.java)
## Solución 1

```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/vaultDoor4]
└─$ ls
VaultDoor4.java

┌──(armando㉿kali)-[~/picoCTF/reversing/vaultDoor4]
└─$ mousepad VaultDoor4.java 
```

```java
import java.util.*;

class VaultDoor4 {
    public static void main(String args[]) {
        VaultDoor4 vaultDoor = new VaultDoor4();
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter vault password: ");
        String userInput = scanner.next();
	String input = userInput.substring("picoCTF{".length(),userInput.length()-1);
	if (vaultDoor.checkPassword(input)) {
	    System.out.println("Access granted.");
	} else {
	    System.out.println("Access denied!");
        }
    }

    // I made myself dizzy converting all of these numbers into different bases,
    // so I just *know* that this vault will be impenetrable. This will make Dr.
    // Evil like me better than all of the other minions--especially Minion
    // #5620--I just know it!
    //
    //  .:::.   .:::.
    // :::::::.:::::::
    // :::::::::::::::
    // ':::::::::::::'
    //   ':::::::::'
    //     ':::::'
    //       ':'
    // -Minion #7781
    public boolean checkPassword(String password) {
        byte[] passBytes = password.getBytes();
        byte[] myBytes = {
            106 , 85  , 53  , 116 , 95  , 52  , 95  , 98  ,
            0x55, 0x6e, 0x43, 0x68, 0x5f, 0x30, 0x66, 0x5f,
            0142, 0131, 0164, 063 , 0163, 0137, 0143, 061 ,
            '9' , '4' , 'f' , '7' , '4' , '5' , '8' , 'e' ,
        };
        for (int i=0; i<32; i++) {
            if (passBytes[i] != myBytes[i]) {
                return false;
            }
        }
        return true;
    }
}
```
- Con ayuda de `CyberChef` y transformar las líneas modificando para cada línea el tipo de decodificación:
`From Decimal` : 106 , 85  , 53  , 116 , 95  , 52  , 95  , 98
`From Hexa`    : 0x55, 0x6e, 0x43, 0x68, 0x5f, 0x30, 0x66, 0x5f
`From Octal`   : 0142, 0131, 0164, 063 , 0163, 0137, 0143, 061
- Y la ultima línea es el texto tal cual, por lo que juntamos las partes y ya obtendremos la bandera:
```bash
jU5t_4_b
UnCh_0f_
bYt3s_c1
94f7458e

jU5t_4_bUnCh_0f_bYt3s_c194f7458e
```

```bash
picoCTF{jU5t_4_bUnCh_0f_bYt3s_c194f7458e}
```

## Solución 2
- Modificamos el código para que quede de la siguiente forma para que por si sola produsca la bandera:
```java
public boolean checkPassword(String password) {
	byte[] passBytes = password.getBytes();
	byte[] myBytes = {
		106 , 85  , 53  , 116 , 95  , 52  , 95  , 98  ,
		0x55, 0x6e, 0x43, 0x68, 0x5f, 0x30, 0x66, 0x5f,
		0142, 0131, 0164, 063 , 0163, 0137, 0143, 061 ,
		'9' , '4' , 'f' , '7' , '4' , '5' , '8' , 'e' ,
	};
	//for (int i=0; i<32; i++) {
	//    if (passBytes[i] != myBytes[i]) {
	//        return false;
	//    }
	//}
	String s = new String(myBytes);
	System.out.println(s);
	return true;
}
```
- Y ya solo ejecutamos el programa:
```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/vaultDoor4]
└─$ javac VaultDoor4.java
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true

┌──(armando㉿kali)-[~/picoCTF/reversing/vaultDoor4]
└─$ java VaultDoor4      
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
Enter vault password: holaasdasdsa
jU5t_4_bUnCh_0f_bYt3s_c194f7458e
Access granted.

┌──(armando㉿kali)-[~/picoCTF/reversing/vaultDoor4]
└─$
```

```bash
picoCTF{jU5t_4_bUnCh_0f_bYt3s_c194f7458e}
```

## Notas Adicionales
## Referencias