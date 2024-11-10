## MPLAB.Xでのトラブル対策

### IPEでのデバイス認識＆書き込みができない

* デバイス選択後APPLYを押すこと  
![image](https://github.com/user-attachments/assets/36b4ef49-e26f-4959-83bb-d35e861cda6d)

* Adbancedモードに切り替えて電源設定を確認  
![image](https://github.com/user-attachments/assets/9882b6fb-12a1-4704-a138-28234fce670a)

### エラー "does not exist or is not an executable"

いろいろやっているうちに治った。パスの問題？  
~~~
testPic.X.debug.null does not exist or is not an executable
~~~

### エラー "24-bit floating point types are not supported"

標準で24bit浮動小数点になっている。Linker - Memory設定変更  
![image](https://github.com/user-attachments/assets/99f15c3d-877b-4d86-9bd2-026a50983f74)

