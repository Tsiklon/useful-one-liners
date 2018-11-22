## Useful SED stuff

### useful sed things

Note: sed statements can be combined into a single process with a semi-colon.

- Print between two patterns

``` # sed -n '/patterna/,/patternb/p' /file ```

- add a prefix and a suffix to any line matching a pattern in a file or stream

``` # sed '/PatternToMatch/s/.*/Prefix & Suffix/' ```


