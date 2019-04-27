---
layout: post
title: "写操作系统之U盘启动"
category:
- 写操作系统 
- 汇编编程
tags: ["写操作系统","操作系统开发","汇编编程","U盘启动"]
---
* content
{:toc}

这篇文章探讨了FAT32格式化后的U盘，如何写MBR的：

<!-- more -->
<!-- TOC -->
```asm
org 07c00h   
jmp short LABEL_START   
nop   
  
OEM                   db  'Dirichet'            ;//8Bytes   
Bytes_per_sector      dw   512   
Sectors_per_cluster   db   8   
Reserved_sectors      dw   584   
Number_of_FATs        db   2   
Root_entries          dw   0   
Sectors_small         dw   0   
Media_descriptor      db   0f8h   
Sectors_per_FAT_small dw   0   
Sectors_per_track     dw   63   
Heads                 dw   255   
Hidden_sectors        dd   63   
Sectors               dd   3902913   
  
Sectors_per_FAT       dd   3804   
Extended_flags        dw   0   
Version               dw   0   
Root_dir_1st_cluster  dd   2   
FSInfo_sector         dw   1   
Backup_boot_sector    dw   6   
times 12 db 0   
  
BIOS_drive            db   80h   
db 0   
Ext_boot_signature    db   29h   
Volume_serial_number  dd   15329558   
Volume_label          db   'Dirichlet09'       ;//11个字节   
File_system           db   'FAT32   '          ;//8个字节              
  
LABEL_START:   
  mov  ax,cs   
  mov  ds,ax    
  mov  es,ax   
  call DispStr   
  jmp  $   
  
DispStr:   
  mov ax,BootMessage   
  mov bp,ax   
  mov cx,15   
  mov ax,01301h   
  mov bx,000ch   
  mov dl,0   
  int 10h   
    
  BootMessage:  db  'hello, kitty!', 13, 10, '$'    
  times 510-($-$$) db 0   
  dw 0xaa55  
```

那么编译完成以上代码之后，如何把编译好的boot.bin写入到U盘的MBR里去呢？


我想到了BIOS的int 13中断。
使用该中断可以实现读写磁盘扇区的功能（ah=2读扇区，ah=3写扇区）。

于是，我用U盘启动，进入到纯DOS下，使用Debug执行以下代码：

```asm
-n boot.bin  //取文件“boot.bin”
-l 300  //将“boot.bin“读到内存0300H处
-a 100  //开始汇编
xxxx:xxxx mov ah,03  //指定INT 13的3号功能，即写磁盘扇区
xxxx:xxxx mov al,01  //扇区数为1
xxxx:xxxx mov dh,00  //磁头号
xxxx:xxxx mov ch,00  //0磁道
xxxx:xxxx mov cl,01  //1扇区
xxxx:xxxx mov bx,0300  //指定boot.bin导入到内存中的起始区域
xxxx:xxxx mov dl,80  //驱动器号，C盘80h,D盘81h
xxxx:xxxx int 13
xxxx:xxxx int 3 //返回Debug
xxxx:xxxx 回车
g=100
```
以上代码执行完成后，重启电脑，实现U盘启动。