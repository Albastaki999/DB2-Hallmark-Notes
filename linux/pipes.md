## Pipes

### Redirection

- &gt; `redirection of output to a file`
  - creates new file if not exists
  - rewrites the content
- &gt;&gt; `Redirection with append`
  - does same thing but appends the result

#### Example

```
ls -al > testfile.txt
```

```
ls -al >> testfile.txt
```

---

### Redirect from a file

```
wc -l < testfile.txt
```

```
wc -l < testfile.txt > count.txt
```

```
sort < numbers.txt | uniq
```
