range2nums
==========

This is a sub-project of [py-ifilters](https://github.com/kkew3/py-ifilters.git).


Installation
------------

```bash
python3 -m virtualenv rt
. rt/bin/activate
pip install -r requirements.txt
./make-launch-scripts range2nums
deactivate
```

The launch script can be found under `dist/`, and can be moved to wherever you want.


Detailed help
-------------

> Copied from `range2nums --help`

```plain
usage: range2nums [-h] [-v] [-d DELIMITER] [-L] pattern

Delete integers passed from stdin that don't match against the provided
pattern. For example, use with `seq' in coreutils to output a list of integers
satisfying the provided pattern. Return code: 0) success; 1) pattern parsing
error; 2) error parsing input from stdin; 4) integer sequence length not
matching the pattern.

positional arguments:
  pattern               the integer pattern

optional arguments:
  -h, --help            show this help message and exit
  -v, --invert-match    delete integers matching the pattern instead
  -d DELIMITER, --delimiter DELIMITER
                        the field delimiter to separate fields in an integer
                        tuple; should not contain `\r' or `\n'; default to
                        whitespace characters
  -L, --suppress-length-mismatch
                        do not raise error on length mismatch, e.g. expecting
                        two integers as per pattern `[2],[4]' but got only one
                        integer per line, and instead treat it as a normal
                        match failure
```

Example usage
-------------

Assuming that `range2nums` is in PATH. Denote the prompt as `prompt> `.

```bash
prompt> seq 1 10 | range2nums -v 3,4,7
1
2
5
6
8
9
10
prompt> printf '%s\n' {1..3},{2..4} | range2nums -d, '[3],[3:]'
3,3
3,4
```
