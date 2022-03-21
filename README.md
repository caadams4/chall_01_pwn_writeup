# chall_01_pwn_writeup

Welcome to the UD Secure Software Design aka x86Exploit course challenge one. Course contents avalible at https://sec.prof.ninja/.

  Course Author: Professor Andy Novocin
  
# chall_01

We begin by performing some recon on the binary. We run 'file a.out' and 'checksec a.out'

![image](https://user-images.githubusercontent.com/79220528/159262426-53376527-902a-41ac-b0e7-03439de11934.png)

Observe the following:
  1. file command output states it's **dynamically** linked and **64bit**
  2. checksec reports there is no stack canary, meaning we are free to smash the stack with a buffer overflow.

Next, we open the file using radare2. Entering the command 'r2 -Ad a.out', observe main:

![image](https://user-images.githubusercontent.com/79220528/159262683-687b72e1-dbff-431b-a871-cfeefe693482.png)

Observe that there are three variables: var_4 = 0x1337, var_8 = 0x69696969 and var_110, which value comes from user input. 

We must smash into var 4 and 8 and overwrite their values to swap. to make the system call, var_4 must 0x69696969 and var_8 must be 0x1337

![image](https://user-images.githubusercontent.com/79220528/159263660-2c4beb21-faf1-44d0-aedc-507906983f3b.png)

