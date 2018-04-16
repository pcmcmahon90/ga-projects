### ***Project 2 Feedback***

***Nico Van de Bovenkamp***

***

**Overall:**  
Great work on this assignment! You made great use of various pandas, matplotlib, and seaborn functionality. The only direct advice that I have is to keep on practicing and take note of some of the 'tricks' and best practices that you see in class.

For example, in your bonus **part 2** you use a `for` loop, when you could do a slightly more efficient operation. For loops operate in native python code and perform tasks entirely sequentially. There are some handy functions in numpy and in Pandas that perform vector based operations and are considerably more efficient. You could have re-writtin the code to be:

```python
df['gre_log'] = df['gre'].apply(np.log)
```

You can actually perform applys on dataframes too!

```python
df.loc[:,['gre_log','gpa_log']] = df.loc[:,['gre','gpa']].apply(np.log)
```

`apply()` can take any method and apply it across an axis (1 or 0, though usually per column). So you can even write your own functions too! Or a lambda function, ie. `df['gre_log'] = df['gre'].apply(lambda x: 1+np.log(x))`

In general: *applys are good, numpy is good, and straight Python is not so great.**

https://engineering.upside.com/a-beginners-guide-to-optimizing-pandas-code-for-speed-c09ef2c6a4d6
