# mql4-redis

远程连接redis需要在redis.window.conf 文件中修改以下配置
1、bind 127.0.0.1 改为 bind 0.0.0.0  
2、protected-mode yes 改为 protected no  
3、#reuquirepass password，去掉注释，修改密码
4、客户端连接redis命令：redis-cli.exe -h hiiboy.com -p 6379 -a password
5、mt4连接redis的时候：  
   RedisContext *c=RedisContext::connect("hiiboy.com",6379);  
   c.appendCommand("AUTH password");  //增加此行


## Introduction

This is a redis client for MQL4 based on the hiredis C client. I used
Microsoft Open Tech version of the library and made some modifications
to the source to make it compile on Visual Studio 2015.

The binding is non-trivial: it can handle mql4 wide strings or any
binary data. It supports all redis commands, though not all commands
are wrapped in a user friendly way.

## Files 

The MQL4 part of the library is open sourced and licenced under
GPL3. It includes the main headers and testing scripts.  In `Library`
folder, there is a precompiled dll, which is the C/C++ part of the
binding. This dll wraps hiredis, and is compatible with latest
MetaTrader4 terminal (32bit). The dll requires that you have the
latest Visual C++ runtime (2015).

## About string encoding

MQL4 strings are Win32 UNICODE strings (basically 2-byte UTF-16). In
the C++ wrapper, all strings are converted to utf-8 before sending to
redis.

## Usage

You can find useage samples in the Scripts/Test directory. Since MQL4
is very limited as a programming language, you will find that code
written with the library is a little verbose, especially you want to
handle errors comprehensively.

## Changes

2016-12-09: Release 0.2. Add a Redis module that implements most commonly used
key management, string, hash, and connection commands.

2016-07-23: Released 0.1.
