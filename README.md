# with-b3

## Install

You need to install the [`b3sum` binary](https://github.com/BLAKE3-team/BLAKE3#the-b3sum-utility) to use this executable.

## Usage

`with-b3` appends [BLAKE3](https://github.com/BLAKE3-team/BLAKE3) checksum to a file path.

Usage: `with-b3` `file_path`(required) `separator`(optional, default: `-`)

Examples:

```
$ with-b3 a/b.txt 
a/b.txt-b3-fb856ed0d5d880eb8a49f75e66f7c519c3376b8d7e3e7a08641beeeb4c225db9

$ with-b3 a/b.txt /
a/b.txt/b3-fb856ed0d5d880eb8a49f75e66f7c519c3376b8d7e3e7a08641beeeb4c225db9

```

## Use case

You can turn an object storage (like Amazon S3 or MinIO) into a content addressable storage. For example:

```
mcli cp some-file some-host/some-bucket/$(with-b3 some-file /)
```

will copy the local file `some-file` to `some-bucket/some-file/b3-xxxxx` on `some-host`, where `xxxxx` is the blake3 checksum of `some-file`.
