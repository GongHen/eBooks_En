* 数组求和
```
.386
.model flat, stdcall
.stack 4096

ExitProcess PROTO, dwExitCode:DWORD

.data
intarray DWORD 10000h,20000h,30000h,40000h

.code
main PROC
    mov edi,OFFSET intarray   ;EDI=intarray地址，OFFEST运算符返回的是变量与其所在段首地址的距离
    mov ecx,LENGTHOF intarray ;循环计数器初始化，LENGTHOF运算符返回的是数组元素的个数
    mov eax,0                 ;sum=0

L1:
    add eax,[edi]             ;加一个整数      
    add edi,TYPE intarray     ;指向下一个元素
    LOOP L1                   ;重复，直到ECX=0

  INVOKE ExitProcess, 0
main ENDP
END main        ;specify the program's entry point
```
* 字符串复制
```
;复制字符串
.386
.model flat, stdcall
.stack 4096

ExitProcess PROTO, dwExitCode:DWORD

.data
source BYTE "This is the source string",0
target BYTE SIZEOF source DUP(0)

.code
main PROC
    mov esi,0
    mov ecx,SIZEOF source ;SIZEOF运算符返回的是，数组初始化的字节数
    mov eax,0

L1:
    add al,source[esi]
    add target[esi],al
    inc esi
    LOOP L1

  INVOKE ExitProcess, 0
main ENDP
END main      
```
