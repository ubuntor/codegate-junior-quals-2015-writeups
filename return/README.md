# Return

We note that the program compares your input with the flag, and returns with the value.
We can check whether the return code is negative (in this case, >= 128), positive, or zero, and binary search.

Final code:

```python
import subprocess
charset = sorted('0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ!"#$%&\'()+,-./:;?@[\\]^_`{|}~ ')
print(charset)
prefix = ""
left = 0
right = len(charset)-1
middle = right/2
while True:
    i = middle
    s = prefix + charset[i]
    ret = subprocess.call(["/home/return/return",s])
    print ret, charset[i]
    if ret == 0:
        print "right"
        print s
        prefix += charset[i]
        left = 0
        right = len(charset)-1
        middle = right/2
    elif ret <= 127:
        print "low",left,middle,right
        left = middle+1
        middle = (left+right)/2
        print "low",left,middle,right
    else:
        print "high",left,middle,right
        right = middle-1
        middle = (left+right)/2
        print "high",left,middle,right
    if right < left:
        break
print(prefix)
```
