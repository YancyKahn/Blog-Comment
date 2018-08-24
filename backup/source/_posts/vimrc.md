---
title: .vimrc
toc: true
date: 2018-08-23 15:59:10
tags: [vim, configure]
categories: [vim, configure]
---

# 一个优雅的vim配置

### **集成功能**

> * **F6 = c/c++文件编译运行**
> * **F2 = 显示头信息**
> * **F5 = 一键生成c++头文件**
> * **自动补全括号**
> * **代码智能对齐**

### vim配置的repo
[Beautiful-vim](https://github.com/YancyKahn/Beautiful-VIM)

### 效果图
![vimrc效果图](/assert/vimrc/vimrc.jpg)

```
"set number
set nu

"set tab width 4
set tabstop=4
set expandtab
set shiftwidth=4
set smarttab

"c indnet
set cindent

"smart indent
set smartindent

"auto indent
set autoindent

"ruler
set ruler
"colorscheme peachpuff
"colorscheme default
"colorscheme koehler
"colorscheme desert
"colorscheme morning
"colorscheme pablo
"remove vi

set nocompatible

"set last status
set laststatus=2

"mouse enable
set mouse=a

"no backup
set nobackup

"set size
set lines=46
set columns=90

"syntax on
syntax on

"set backspace
set backspace=indent,eol,start

"keymap
"auto
inoremap ' ''<ESC>i
inoremap " ""<ESC>i
"inoremap < <><ESC>i
inoremap { {<CR>}<ESC>i
inoremap ( ()<ESC>i
inoremap [ []<ESC>i

"share clipboard
set clipboard+=unnamed

"Lang & Enconding
set fileencodings=utf-8,gbk2312,gbk,gb18030,cp936
set encoding=utf-8
set langmenu=zh_CN

"Function
"compileRunCPP
map <F6> :call CompileRunCPP()<cr>
func! CompileRunCPP()
    exec "w"
    exec "!g++ -g2 % -o %<"
    exec "!./%<"
endfun
"setInfo
if !exists("*SetTitlea")
map <F2> :call SetInfo()<CR>
func SetInfo()
let l = 0
let l = l + 1 | call setline(l,'/************************************************')
let l = l + 1 | call setline(l,' *Author*        : YancyKahn')
let l = l + 1 | call setline(l,' *Created Time*  : '.strftime('%c'))
let l = l + 1 | call setline(l,'**Problem**:')
let l = l + 1 | call setline(l,'**Analyse**:')
let l = l + 1 | call setline(l,'**Get**:')
let l = l + 1 | call setline(l,'**Code**:')
let l = l + 1 | call setline(l,'*********************************************/')
let l = l + 1 | call setline(l,'')
endfunc
endif
"setCode
if !exists("*SetTitlea")
map <F5> :call SetCode()<CR>
func SetCode()
let l = 10
let l = l + 1 | call setline(l,'#include <cstdio>')
let l = l + 1 | call setline(l,'#include <cstring>')
let l = l + 1 | call setline(l,'#include <iostream>')
let l = l + 1 | call setline(l,'#include <algorithm>')
let l = l + 1 | call setline(l,'#include <vector>')
let l = l + 1 | call setline(l,'#include <queue>')
let l = l + 1 | call setline(l,'#include <set>')
let l = l + 1 | call setline(l,'#include <map>')
let l = l + 1 | call setline(l,'#include <string>')
let l = l + 1 | call setline(l,'#include <cmath>')
let l = l + 1 | call setline(l,'#include <cstdlib>')
let l = l + 1 | call setline(l,'#include <ctime>')
let l = l + 1 | call setline(l,'#include <stack>')
let l = l + 1 | call setline(l,'using namespace std;')
let l = l + 1 | call setline(l,'typedef pair<int, int> pii;')
let l = l + 1 | call setline(l,'typedef long long ll;')
let l = l + 1 | call setline(l,'typedef unsigned long long ull;')
let l = l + 1 | call setline(l,'typedef vector<int> vi;')
let l = l + 1 | call setline(l,'#define pr(x) cout << #x << ": " << x << "  " ')
let l = l + 1 | call setline(l,'#define pl(x) cout << #x << ": " << x << endl;')
let l = l + 1 | call setline(l,'#define pri(a) printf("%d\n",(a))')
let l = l + 1 | call setline(l,'#define xx first')
let l = l + 1 | call setline(l,'#define yy second')
let l = l + 1 | call setline(l,'#define sa(n) scanf("%d", &(n))')
let l = l + 1 | call setline(l,'#define sal(n) scanf("%lld", &(n))')
let l = l + 1 | call setline(l,'#define sai(n) scanf("%I64d", &(n))')
let l = l + 1 | call setline(l,'#define vep(c) for(decltype((c).begin() ) it = (c).begin(); it != (c).end(); it++) ')
let l = l + 1 | call setline(l,'const int mod = int(1e9) + 7, INF = 0x3f3f3f3f;')
let l = l + 1 | call setline(l,'const int maxn = 1e5 + 13;')
let l = l + 1 | call setline(l,'')
let l = l + 1 | call setline(l,'')
let l = l + 1 | call setline(l,'')
let l = l + 1 | call setline(l,'int main(void)')
let l = l + 1 | call setline(l,'{')
let l = l + 1 | call setline(l,'#ifdef LOCAL')
let l = l + 1 | call setline(l,'    //freopen("in.txt", "r", stdin);')
let l = l + 1 | call setline(l,'    //freopen("out.txt", "w", stdout);')
let l = l + 1 | call setline(l,'#endif')
" let l = l + 1 | call setline(l,'    ios_base::sync_with_stdio(false),cin.tie(0),cout.tie(0);')
let l = l + 1 | call setline(l,'    ')
let l = l + 1 | call setline(l,'    return 0;')
let l = l + 1 | call setline(l,'}')
endfunc
endif

```
