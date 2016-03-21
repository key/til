# BITCODEの確認

2016/03/21

静的ライブラリを確認するには`otool`を使う。

```bash
otool -arch armv7 -l ./lib.a
```

bitcodeセクションが含まれてsizeが1以上になる。

```
Section
  sectname __bitcode
   segname __LLVM
      addr 0x00000fc0
      size 0x000020a0
    offset 6556
     align 2^4 (16)
    reloff 0
    nreloc 0
     flags 0x00000000
 reserved1 0
 reserved2 0
 ```
 
 bitcodeが含まれない場合はこんなかんじ。
 
 ```
Section
  sectname __bitcode
   segname __LLVM
      addr 0x00000fb8
      size 0x00000001
    offset 6548
     align 2^0 (1)
    reloff 0
    nreloc 0
     flags 0x00000000
 reserved1 0
 reserved2 0
  ```

## Xcodeでビルド

XcodeでビルドするときはBuild Settings -> Other C Flagsに `-fembed-bitcode` を付ける。

## xcodebuildコマンドでビルド

xcodebuildでビルドする際に`OTHER_CFLAGS="-fembed-bitcode"`を付ける。
