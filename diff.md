
### Diffing multiple files with the same prefix but differing suffixes
` # for i in $(find ./ -type f | sort | awk -F . '{print $2}' | sed 's/^.//'| uniq); do diff $i.pre $i.post; done `

