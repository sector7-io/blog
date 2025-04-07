---
layout: post
title: "Welcome to Sector7"
date: 2025-04-07
---

Welcome to **Sector7**, my corner of the internet. This is where I’ll share things I’m building, breaking, and learning — especially compilers, code generation, and obscure tech experiments.

### Example: Hello World in x86 Assembly

```nasm
section .data
    msg db "Hello, Sector7!", 0Ah

section .text
    global _start

_start:
    mov eax, 4
    mov ebx, 1
    mov ecx, msg
    mov edx, 16
    int 0x80

    mov eax, 1
    xor ebx, ebx
    int 0x80

