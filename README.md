# comp_bench
A bash script which runs compression and decompression benchmarks on the following terminal utilities: `gzip bzip2 zstd lz4 xz`

Outputs compression time, compressed size, compression ratio, and decompression time.

The target can either be a folder, in which case the folder will be archived into a tar, or a tar file itself.

Default, fast, and slow options can be applied. All options are single threaded even if the utility happens to support multithreading.
- **Default**: Uses the default compression level according to each utility's man page. This option is used when no option is specified.
- **Fast**: Uses the lowest compression level available. For some utilities, this is the same as the default (i.e. lz4).
- **Slow**: Uses the highest compression level available. For some utilities, this is the same as the default (i.e. bzip2). This excludes any kind of special "extreme" compression that utilities like `xz` offer.

#### Warning
The benchmark could take a while to run or use a significant amount of disk space depending on the size of the target archive. Be mindful of how large the target directory or archive is.

## Usage
```./comp_bench [file or dir] {def,fast,slow}```

### Example

```bash
~$ git clone https://github.com/jacobkoiner/comp_bench
~$ cd comp_bench

~/comp_bench$ git clone https://github.com/git/git
~/comp_bench$ ./comp_bench git/

~/comp_bench$ tar cf git.tar git/
~/comp_bench$ ./comp_bench git.tar fast
```

### Output

```bash
$ ./comp_bench git/
--- Archiving git into git.tar for the benchmark target.

tar
  size: 295912 289M

--- Beginning benchmarks...
--- Default Compression

gzip
  time: 6.30s
  size: 258360 253M
  ratio: 0.8731
bzip2
  time: 19.45s
  size: 256428 251M
  ratio: 0.8666
zstd
  time: 0.47s
  size: 256468 251M
  ratio: 0.8667
lz4
  time: 0.23s
  size: 266464 261M
  ratio: 0.9005
xz
  time: 68.92s
  size: 247824 243M
  ratio: 0.8375

--- Decompression

gzip
  time: 1.25s
bzip2
  time: 9.52s
zstd
  time: 0.15s
lz4
  time: 0.14s
xz
  time: 8.33s

--- Benchmarks complete. Cleaning up.

$ ./comp_bench git.tar fast
--- Using git.tar as the benchmark target.

tar
  size: 295912 289M

--- Beginning benchmarks...
--- Fast Compression

gzip
  time: 5.41s
  size: 261012 255M
  ratio: 0.8821
bzip2
  time: 18.14s
  size: 260056 254M
  ratio: 0.8788
zstd
  time: 0.27s
  size: 260412 255M
  ratio: 0.8800
lz4
  time: 0.23s
  size: 266464 261M
  ratio: 0.9005
xz
  time: 26.88s
  size: 257208 252M
  ratio: 0.8692

--- Decompression

gzip
  time: 1.28s
bzip2
  time: 7.61s
zstd
  time: 0.14s
lz4
  time: 0.14s
xz
  time: 5.01s

--- Benchmarks complete. Cleaning up.
```

## License
`comp_bench` is licensed under the MIT license. See [LICENSE](/LICENSE) for the full license text.
