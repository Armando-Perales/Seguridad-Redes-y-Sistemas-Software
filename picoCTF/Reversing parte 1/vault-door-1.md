## Objetivo
This vault uses some complicated arrays! I hope you can make sense of it, special agent. The source code for this vault is here: [VaultDoor1.java](https://jupiter.challenges.picoctf.org/static/29b91e638ccbd76aaa8c0462d1c64d8d/VaultDoor1.java)
## Solución

```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/vaultDoor1]
└─$ ls
VaultDoor1.java

┌──(armando㉿kali)-[~/picoCTF/reversing/vaultDoor1]
└─$ cat VaultDoor1.java       
import java.util.*;

class VaultDoor1 {
    public static void main(String args[]) {
        VaultDoor1 vaultDoor = new VaultDoor1();
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

    // I came up with a more secure way to check the password without putting
    // the password itself in the source code. I think this is going to be
    // UNHACKABLE!! I hope Dr. Evil agrees...
    //
    // -Minion #8728
    public boolean checkPassword(String password) {
        return password.length() == 32 &&
               password.charAt(0)  == 'd' &&
               password.charAt(29) == '3' &&
               password.charAt(4)  == 'r' &&
               password.charAt(2)  == '5' &&
               password.charAt(23) == 'r' &&
               password.charAt(3)  == 'c' &&
               password.charAt(17) == '4' &&
               password.charAt(1)  == '3' &&
               password.charAt(7)  == 'b' &&
               password.charAt(10) == '_' &&
               password.charAt(5)  == '4' &&
               password.charAt(9)  == '3' &&
               password.charAt(11) == 't' &&
               password.charAt(15) == 'c' &&
               password.charAt(8)  == 'l' &&
               password.charAt(12) == 'H' &&
               password.charAt(20) == 'c' &&
               password.charAt(14) == '_' &&
               password.charAt(6)  == 'm' &&
               password.charAt(24) == '5' &&
               password.charAt(18) == 'r' &&
               password.charAt(13) == '3' &&
               password.charAt(19) == '4' &&
               password.charAt(21) == 'T' &&
               password.charAt(16) == 'H' &&
               password.charAt(27) == 'f' &&
               password.charAt(30) == 'b' &&
               password.charAt(25) == '_' &&
               password.charAt(22) == '3' &&
               password.charAt(28) == '6' &&
               password.charAt(26) == 'f' &&
               password.charAt(31) == '0';
    }
}

┌──(armando㉿kali)-[~/picoCTF/reversing/vaultDoor1]
└─$ mousepad VaultDoor1.java 
```
- Pasamos las variables que contienen las partes de la bandera.
```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/vaultDoor1]
└─$ cat flag           
		       password.charAt(0)  == 'd' &&
               password.charAt(29) == '3' &&
               password.charAt(4)  == 'r' &&
               password.charAt(2)  == '5' &&
               password.charAt(23) == 'r' &&
               password.charAt(3)  == 'c' &&
               password.charAt(17) == '4' &&
               password.charAt(1)  == '3' &&
               password.charAt(7)  == 'b' &&
               password.charAt(10) == '_' &&
               password.charAt(5)  == '4' &&
               password.charAt(9)  == '3' &&
               password.charAt(11) == 't' &&
               password.charAt(15) == 'c' &&
               password.charAt(8)  == 'l' &&
               password.charAt(12) == 'H' &&
               password.charAt(20) == 'c' &&
               password.charAt(14) == '_' &&
               password.charAt(6)  == 'm' &&
               password.charAt(24) == '5' &&
               password.charAt(18) == 'r' &&
               password.charAt(13) == '3' &&
               password.charAt(19) == '4' &&
               password.charAt(21) == 'T' &&
               password.charAt(16) == 'H' &&
               password.charAt(27) == 'f' &&
               password.charAt(30) == 'b' &&
               password.charAt(25) == '_' &&
               password.charAt(22) == '3' &&
               password.charAt(28) == '6' &&
               password.charAt(26) == 'f' &&
               password.charAt(31) == '0'

┌──(armando㉿kali)-[~/picoCTF/reversing/vaultDoor1]
└─$ cat flag | sort | awk '{print($3)}' | tr -d "'" | tr -d "\n"
d35cr4mbl3_tH3_cH4r4cT3r5_ff63b0                                                                                                                
┌──(armando㉿kali)-[~/picoCTF/reversing/vaultDoor1]
└─$ 
```

```bash
picoCTF{d35cr4mbl3_tH3_cH4r4cT3r5_ff63b0}
```
## Notas Adicionales
cat flag | sort | awk '{print($3)}' | tr -d "'" | tr -d "\n"
	sort - Ordena los renglones en este caso por el número que se encuentra en el `charAt()`
	awk '{print($3)}' - Elimina todo dejando solo lo que se encuentra en la tercera columna.
	tr -d "'" - Cambia las comillas simples sustituyéndolas por un campo vacío.
	tr -d "\n" - Cambia los saltos de línea sustituyéndolas por un campo vacío.

## Referencias