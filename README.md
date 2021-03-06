Tim: Timed iteration monitor
============================

A common pattern I have when writing code to import or treat large chunk of data is to do some printing to track the progress and some timing to monitor the speed.
So I often end up with some variation of this in my code:

```python
from datetime import datetime
start = datetime.now()
n = 0
for i in my_iter:
    n+=1
    print "\r", i,
    # do stuff
print start - datetime.now()
print (start - datetime.now()) / n / 100
```


which is a lot to remember and type which in turn make it easy to introduce bugs in some edge case which you need then to debug.

So I wrote tim to help me do just that, so I have this pattern ready for use and working and can spend my time coding my data treatment instead of debbugging my helper code.

*WARNING* : This is alpha level stuff, I'm still working out the proper way to do stuff so the API may still change a bit.

How to use tim
--------------

Common usage pattern would probably be:

```python
import tim

tim.start()
for i in my_iter:
    tim.pulse_print() # print current progress
    # do stuff
tim.stop() # print overall stats and reset counter
```

If you just need to monitor start and stop you can use:

```python
tim.start()
# calculation
tim.stop() # print elapsed time and reset
```
