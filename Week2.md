## 과제

아래 파일 다운받고 분석 후 C언어로 바꿔보기 ( 손으로 디컴파일 해보기 )

[hw.zip](https://prod-files-secure.s3.us-west-2.amazonaws.com/8b738838-5133-4949-bf7a-1df092aa6c82/23d27755-a8fa-4859-b5d7-726fd4402bf3/hw.zip)

## 해결

### 실행

```
$ ./hw
-bash: ./hw: Permission denied
```

권한이 없어서 그렇다고 함.

```
$ chmod +x hw
$ ./hw
5
```

IDA 로 hw 파일을 열었다

<img src='https://i.ibb.co/GFjwLNj/idatest.png'>

못 알아 보겠으니까 명령어를 써봤다

### 분석

```
$ objdump -d hw
```

- `objdump -d hw` 해석
    
    `objdump` : ELF 포맷 / 실행 가능 바이너리 파일 포맷 → 내용 분석 및 표시
    
    `-d` : `--disassemble` 과 같은 뜻
    
- 결과물
    
    ```
    $ objdump -d hw
    
    hw:     file format elf64-x86-64
    
    Disassembly of section .init:
    
    0000000000401000 <_init>:
      401000:       f3 0f 1e fa             endbr64
      401004:       48 83 ec 08             sub    $0x8,%rsp
      401008:       48 8b 05 c9 2f 00 00    mov    0x2fc9(%rip),%rax        # 403fd8 <__gmon_start__@Base>
      40100f:       48 85 c0                test   %rax,%rax
      401012:       74 02                   je     401016 <_init+0x16>
      401014:       ff d0                   call   *%rax
      401016:       48 83 c4 08             add    $0x8,%rsp
      40101a:       c3                      ret
    
    Disassembly of section .plt:
    
    0000000000401020 <printf@plt-0x10>:
      401020:       ff 35 ca 2f 00 00       push   0x2fca(%rip)        # 403ff0 <_GLOBAL_OFFSET_TABLE_+0x8>
      401026:       ff 25 cc 2f 00 00       jmp    *0x2fcc(%rip)        # 403ff8 <_GLOBAL_OFFSET_TABLE_+0x10>
      40102c:       0f 1f 40 00             nopl   0x0(%rax)
    
    0000000000401030 <printf@plt>:
      401030:       ff 25 ca 2f 00 00       jmp    *0x2fca(%rip)        # 404000 <printf@GLIBC_2.2.5>
      401036:       68 00 00 00 00          push   $0x0
      40103b:       e9 e0 ff ff ff          jmp    401020 <_init+0x20>
    
    Disassembly of section .text:
    
    0000000000401040 <_start>:
      401040:       f3 0f 1e fa             endbr64
      401044:       31 ed                   xor    %ebp,%ebp
      401046:       49 89 d1                mov    %rdx,%r9
      401049:       5e                      pop    %rsi
      40104a:       48 89 e2                mov    %rsp,%rdx
      40104d:       48 83 e4 f0             and    $0xfffffffffffffff0,%rsp
      401051:       50                      push   %rax
      401052:       54                      push   %rsp
      401053:       45 31 c0                xor    %r8d,%r8d
      401056:       31 c9                   xor    %ecx,%ecx
      401058:       48 c7 c7 26 11 40 00    mov    $0x401126,%rdi
      40105f:       ff 15 63 2f 00 00       call   *0x2f63(%rip)        # 403fc8 <__libc_start_main@GLIBC_2.34>
      401065:       f4                      hlt
      401066:       66 2e 0f 1f 84 00 00    cs nopw 0x0(%rax,%rax,1)
      40106d:       00 00 00
    
    0000000000401070 <_dl_relocate_static_pie>:
      401070:       f3 0f 1e fa             endbr64
      401074:       c3                      ret
      401075:       66 2e 0f 1f 84 00 00    cs nopw 0x0(%rax,%rax,1)
      40107c:       00 00 00
      40107f:       90                      nop
      401080:       b8 18 40 40 00          mov    $0x404018,%eax
      401085:       48 3d 18 40 40 00       cmp    $0x404018,%rax
      40108b:       74 13                   je     4010a0 <_dl_relocate_static_pie+0x30>
      40108d:       48 8b 05 3c 2f 00 00    mov    0x2f3c(%rip),%rax        # 403fd0 <_ITM_deregisterTMCloneTable@Base>
      401094:       48 85 c0                test   %rax,%rax
      401097:       74 07                   je     4010a0 <_dl_relocate_static_pie+0x30>
      401099:       bf 18 40 40 00          mov    $0x404018,%edi
      40109e:       ff e0                   jmp    *%rax
      4010a0:       c3                      ret
      4010a1:       66 66 2e 0f 1f 84 00    data16 cs nopw 0x0(%rax,%rax,1)
      4010a8:       00 00 00 00
      4010ac:       0f 1f 40 00             nopl   0x0(%rax)
      4010b0:       be 18 40 40 00          mov    $0x404018,%esi
      4010b5:       48 81 ee 18 40 40 00    sub    $0x404018,%rsi
      4010bc:       48 89 f0                mov    %rsi,%rax
      4010bf:       48 c1 ee 3f             shr    $0x3f,%rsi
      4010c3:       48 c1 f8 03             sar    $0x3,%rax
      4010c7:       48 01 c6                add    %rax,%rsi
      4010ca:       48 d1 fe                sar    %rsi
      4010cd:       74 19                   je     4010e8 <_dl_relocate_static_pie+0x78>
      4010cf:       48 8b 05 0a 2f 00 00    mov    0x2f0a(%rip),%rax        # 403fe0 <_ITM_registerTMCloneTable@Base>
      4010d6:       48 85 c0                test   %rax,%rax
      4010d9:       74 0d                   je     4010e8 <_dl_relocate_static_pie+0x78>
      4010db:       bf 18 40 40 00          mov    $0x404018,%edi
      4010e0:       ff e0                   jmp    *%rax
      4010e2:       66 0f 1f 44 00 00       nopw   0x0(%rax,%rax,1)
      4010e8:       c3                      ret
      4010e9:       0f 1f 80 00 00 00 00    nopl   0x0(%rax)
      4010f0:       f3 0f 1e fa             endbr64
      4010f4:       80 3d 1d 2f 00 00 00    cmpb   $0x0,0x2f1d(%rip)        # 404018 <__TMC_END__>
      4010fb:       75 13                   jne    401110 <_dl_relocate_static_pie+0xa0>
      4010fd:       55                      push   %rbp
      4010fe:       48 89 e5                mov    %rsp,%rbp
      401101:       e8 7a ff ff ff          call   401080 <_dl_relocate_static_pie+0x10>
      401106:       c6 05 0b 2f 00 00 01    movb   $0x1,0x2f0b(%rip)        # 404018 <__TMC_END__>
      40110d:       5d                      pop    %rbp
      40110e:       c3                      ret
      40110f:       90                      nop
      401110:       c3                      ret
      401111:       66 66 2e 0f 1f 84 00    data16 cs nopw 0x0(%rax,%rax,1)
      401118:       00 00 00 00
      40111c:       0f 1f 40 00             nopl   0x0(%rax)
      401120:       f3 0f 1e fa             endbr64
      401124:       eb 8a                   jmp    4010b0 <_dl_relocate_static_pie+0x40>
    
    0000000000401126 <main>:
      401126:       55                      push   %rbp
      401127:       48 89 e5                mov    %rsp,%rbp
      40112a:       48 83 ec 10             sub    $0x10,%rsp
      40112e:       c7 45 f8 02 00 00 00    movl   $0x2,-0x8(%rbp)
      401135:       c7 45 f4 03 00 00 00    movl   $0x3,-0xc(%rbp)
      40113c:       83 7d f8 03             cmpl   $0x3,-0x8(%rbp)
      401140:       7e 0b                   jle    40114d <main+0x27>
      401142:       8b 45 f8                mov    -0x8(%rbp),%eax
      401145:       2b 45 f4                sub    -0xc(%rbp),%eax
      401148:       89 45 fc                mov    %eax,-0x4(%rbp)
      40114b:       eb 0b                   jmp    401158 <main+0x32>
      40114d:       8b 55 f8                mov    -0x8(%rbp),%edx
      401150:       8b 45 f4                mov    -0xc(%rbp),%eax
      401153:       01 d0                   add    %edx,%eax
      401155:       89 45 fc                mov    %eax,-0x4(%rbp)
      401158:       8b 45 fc                mov    -0x4(%rbp),%eax
      40115b:       89 c6                   mov    %eax,%esi
      40115d:       bf 04 20 40 00          mov    $0x402004,%edi
      401162:       b8 00 00 00 00          mov    $0x0,%eax
      401167:       e8 c4 fe ff ff          call   401030 <printf@plt>
      40116c:       b8 00 00 00 00          mov    $0x0,%eax
      401171:       c9                      leave
      401172:       c3                      ret
    
    Disassembly of section .fini:
    
    0000000000401174 <_fini>:
      401174:       f3 0f 1e fa             endbr64
      401178:       48 83 ec 08             sub    $0x8,%rsp
      40117c:       48 83 c4 08             add    $0x8,%rsp
      401180:       c3                      ret
    ```
    

### main

```
0000000000401126 <main>:
  401126:       55                      push   %rbp
  401127:       48 89 e5                mov    %rsp,%rbp
  40112a:       48 83 ec 10             sub    $0x10,%rsp
  40112e:       c7 45 f8 02 00 00 00    movl   $0x2,-0x8(%rbp)
  401135:       c7 45 f4 03 00 00 00    movl   $0x3,-0xc(%rbp)
  40113c:       83 7d f8 03             cmpl   $0x3,-0x8(%rbp)
  401140:       7e 0b                   jle    40114d <main+0x27>
  401142:       8b 45 f8                mov    -0x8(%rbp),%eax
  401145:       2b 45 f4                sub    -0xc(%rbp),%eax
  401148:       89 45 fc                mov    %eax,-0x4(%rbp)
  40114b:       eb 0b                   jmp    401158 <main+0x32>
  40114d:       8b 55 f8                mov    -0x8(%rbp),%edx
  401150:       8b 45 f4                mov    -0xc(%rbp),%eax
  401153:       01 d0                   add    %edx,%eax
  401155:       89 45 fc                mov    %eax,-0x4(%rbp)
  401158:       8b 45 fc                mov    -0x4(%rbp),%eax
  40115b:       89 c6                   mov    %eax,%esi
  40115d:       bf 04 20 40 00          mov    $0x402004,%edi
  401162:       b8 00 00 00 00          mov    $0x0,%eax
  401167:       e8 c4 fe ff ff          call   401030 <printf@plt>
  40116c:       b8 00 00 00 00          mov    $0x0,%eax
  401171:       c9                      leave
  401172:       c3                      ret
```

함수 시작 부분에서 스택 프레임 설정
로켤 변수 공간 생성

```
  401126:       55                      push   %rbp
  401127:       48 89 e5                mov    %rsp,%rbp
```

스택 포인터에서 0x10만큼 뺀 후 로컬 변수 공간 할당

```
  40112a:       48 83 ec 10             sub    $0x10,%rsp
```

rbp로 부터 8칸(0x8) 뒤에 상수 2 저장, 12칸(0x12)뒤에 상수 3 저장

아마 int a=2; int b=3;

```
  40112e:       c7 45 f8 02 00 00 00    movl   $0x2,-0x8(%rbp)
  401135:       c7 45 f4 03 00 00 00    movl   $0x3,-0xc(%rbp)
```

`cmpl` : rbp-0x8의 값과 정수 3을 비교
`jle` : Jump Less or Equal / 만족시 해당 주소로 jump

아마 if(a <= 3) 인 것 같음

```
  40113c:       83 7d f8 03             cmpl   $0x3,-0x8(%rbp)
  401140:       7e 0b                   jle    40114d <main+0x27>
```

### if

❕이 시점에 조건을 만족하므로 해당 코드 블록으로 넘어갑니다❕

```
  40114d:       8b 55 f8                mov    -0x8(%rbp),%edx
  401150:       8b 45 f4                mov    -0xc(%rbp),%eax
  401153:       01 d0                   add    %edx,%eax
  401155:       89 45 fc                mov    %eax,-0x4(%rbp)
```

rbp-0x8의 값(상수 2)을 edx에 저장
rbp-0xc의 값(상수 3)을 eax에 저장

```
  40114d:       8b 55 f8                mov    -0x8(%rbp),%edx
  401150:       8b 45 f4                mov    -0xc(%rbp),%eax
```

edx(상수 2)와 eax(상수 3) 을 더해서 eax에 저장

eax = edx+eax;

```
  401153:       01 d0                   add    %edx,%eax
```

eax의 값을 rbp-0x4에 저장

```
  401155:       89 45 fc                mov    %eax,-0x4(%rbp)
```

### else

⚠️조건을 만족하지 않으면 점프하지 않으므로 계속 진행⚠️

```
  401142:       8b 45 f8                mov    -0x8(%rbp),%eax
  401145:       2b 45 f4                sub    -0xc(%rbp),%eax
  401148:       89 45 fc                mov    %eax,-0x4(%rbp)
  40114b:       eb 0b                   jmp    401158 <main+0x32>
```

rbp-0x8의 값(상수 2)을 eax에 저장

```
  401142:       8b 45 f8                mov    -0x8(%rbp),%eax
```

eax(상수 2)에서 -0xc(%rbp)(상수 3)를 빼서 eax에 저장

AT&T 문법으로 보고 있어서 source와 destination이 다

```
  401145:       2b 45 f4                sub    -0xc(%rbp),%eax
```

eax의 값을 rbp-0x4에 저장

```
  401148:       89 45 fc                mov    %eax,-0x4(%rbp)
```

401158 <main+0x32> 로 점프

```
  40114b:       eb 0b                   jmp    401158 <main+0x32>
```

### ~main

```
  401158:       8b 45 fc                mov    -0x4(%rbp),%eax
  40115b:       89 c6                   mov    %eax,%esi
  40115d:       bf 04 20 40 00          mov    $0x402004,%edi
  401162:       b8 00 00 00 00          mov    $0x0,%eax
  401167:       e8 c4 fe ff ff          call   401030 <printf@plt>
```

rbp-0x4의 값을 eax에 저장
eax의 값을 esi에 저장

```
  401158:       8b 45 fc                mov    -0x4(%rbp),%eax
  40115b:       89 c6                   mov    %eax,%esi
```

`$0x402004` 를 edi에 저장

```
  40115d:       bf 04 20 40 00          mov    $0x402004,%edi
```

`$0x402004` 가 뭔지 몰라서 `$ objdump -x hw` 로 확인해봤다

```
$ objdump -x hw

...
Sections:
Idx Name          Size      VMA               LMA               File off  Algn
  0 .interp       0000001c  0000000000400318  0000000000400318  00000318  2**0
                  CONTENTS, ALLOC, LOAD, READONLY, DATA
...
15 .rodata       00000008  0000000000402000  0000000000402000  00002000  2**2
                  CONTENTS, ALLOC, LOAD, READONLY, DATA
...
```

그래도 모르겠어서 `$ objdump -D hw` 로 전부 디어셈블했다

```
$ objdump -D hw
...
Disassembly of section .rodata:

0000000000402000 <_IO_stdin_used>:
  402000:       01 00                   add    %eax,(%rax)
  402002:       02 00                   add    (%rax),%al
  402004:       25                      .byte 0x25
  402005:       64 0a 00                or     %fs:(%rax),%al
...
```

402004 : 25 64 0a → 출력할 문자열임 ( .rodata 이기 때문에 명령어 말고 16진수 데이터를 봐야함) → 아스키 코드로 % d \n 

eax의 값을 상수 0으로 저장

401030 에 있는 함수(printf)를 호출함

```
  401162:       b8 00 00 00 00          mov    $0x0,%eax
  401167:       e8 c4 fe ff ff          call   401030 <printf@plt>
```

### printf

❕printf 함수로 넘어갑니다❕

```
0000000000401030 <printf@plt>:
  401030:       ff 25 ca 2f 00 00       jmp    *0x2fca(%rip)        # 404000 <printf@GLIBC_2.2.5>
  401036:       68 00 00 00 00          push   $0x0
  40103b:       e9 e0 ff ff ff          jmp    401020 <_init+0x20>
```

*0x2fca(%rip) 로 점프

주석에서 `*0x2fca(%rip)` 가  `# 404000 <printf@GLIBC_2.2.5>` 라는 거 같다

```
  401030:       ff 25 ca 2f 00 00       jmp    *0x2fca(%rip)        # 404000 <printf@GLIBC_2.2.5>
```

```
Disassembly of section .got.plt:

0000000000403fe8 <_GLOBAL_OFFSET_TABLE_>:
  403fe8:       f8                      clc
  403fe9:       3d 40 00 00 00          cmp    $0x40,%eax
        ...
  403ffe:       00 00                   add    %al,(%rax)
  404000:       36 10 40 00             ss adc %al,0x0(%rax)
  404004:       00 00                   add    %al,(%rax)
        ...
```

???

0x0 을 스택에 push 하고
401020 <_init+0x20> 으로 점프

```
  401036:       68 00 00 00 00          push   $0x0
  40103b:       e9 e0 ff ff ff          jmp    401020 <_init+0x20>
```

```
0000000000401020 <printf@plt-0x10>:
  401020:       ff 35 ca 2f 00 00       push   0x2fca(%rip)        # 403ff0 <_GLOBAL_OFFSET_TABLE_+0x8>
  401026:       ff 25 cc 2f 00 00       jmp    *0x2fcc(%rip)        # 403ff8 <_GLOBAL_OFFSET_TABLE_+0x10>
  40102c:       0f 1f 40 00             nopl   0x0(%rax)
```

스택에 0x2fca(%rip) 값을 push

이번에는 `# 403ff0 <_GLOBAL_OFFSET_TABLE_+0x8>`

```
  401020:       ff 35 ca 2f 00 00       push   0x2fca(%rip)        # 403ff0 <_GLOBAL_OFFSET_TABLE_+0x8>
```

*0x2fcc(%rip) 로 점프

이번에는 `# 403ff8 <_GLOBAL_OFFSET_TABLE_+0x10>`

```
  401026:       ff 25 cc 2f 00 00       jmp    *0x2fcc(%rip)        # 403ff8 <_GLOBAL_OFFSET_TABLE_+0x10>
```

_GLOBAL_OFFSET_TABLE_ : 컴파일 할때 include 한 라이브러리에 있는 게 담기는? ? 그래서 `.got.plt` 에 담겨있다고함

### ~~main

eax 에 상수 0 저장
leave ret 하여 main 함수에서 생성된 스택프레임을 정리하고 이전 함수의 호출 위치로 돌아감

→0을 리턴하고 종료

```
  40116c:       b8 00 00 00 00          mov    $0x0,%eax
  401171:       c9                      leave
  401172:       c3                      ret
```

### 디컴파일 결과

```c
#include<stdio.h>
int main(){
	int a=2;
	int b=3;
	int c;
	if(a<=3) c=a+b;
	else c=a-b;
	printf("%d\n",c);
	return 0
}
```

### 참고자료

`chmod +x filename` 

https://velog.io/@sungmo738/리눅스에서-허가-거부-Permission-denied

`objdump -d /path/to/binary`

[How to disassemble a binary executable in Linux to get the assembly code?](https://stackoverflow.com/questions/5125896/how-to-disassemble-a-binary-executable-in-linux-to-get-the-assembly-code)

`objdump -D /path/to/binary`

[[Hack #10] objdump - (2) 오브젝트 파일 역어셈블](https://devanix.tistory.com/188)

Intel AT&T

[Intel 과 AT&T 차이점](https://hardner.tistory.com/22)
