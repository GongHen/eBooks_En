### Assembly Language for x86 Processors,Seventh Edition
---
> **第13章 高级语言接口--P438**</br>
如何从高级语言调用汇编？`内嵌汇编代码(inline assembly code)`是指直接插入高级语言程序中的汇编源代码。
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
* 字符串翻转
```
;字符串翻转
.386
.model flat, stdcall
.stack 4096

ExitProcess PROTO, dwExitCode:DWORD

.data
aName BYTE "Abraham Lincoln",0
nameSize =($ - aName) - 1

.code
main PROC
;将名字压入栈
    mov ecx,nameSize
    mov esi,0

L1:
    movzx eax,aName[esi];获取字符
    push eax            ;压入堆栈
    inc esi
    LOOP L1

;将名字按逆序弹出堆栈
;并存入aName数组
    mov ecx,nameSize
    mov esi,0

L2:
    pop eax
    mov aName[esi],al;获取字符串
    inc esi          ;存入字符串
    LOOP L2

  INVOKE ExitProcess, 0
main ENDP
END main 
```
