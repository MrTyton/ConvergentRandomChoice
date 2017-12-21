# ConvergentRandomChoice

Random walk choice, based off of numpy.choice. Requires numpy.

Every time an item is selected, it redistributes some of that item's probability into the other items. This means that the more times an item is selected, the less likey it is to be chosen in the future, while an item that isn't chosen very often is more likely to be chosen.

There are two functions.

`ConvergentRandomChoice(1d array-like, pchange='uniform', initials=None)`
Initializer function.
: The list of items to be selected from
: pchange: either 'uniform', which means that they probability decay will be equal to 1/len(items), or a float from 0-1 signifying the percentage decay. Defaults to uniform.
: initials: list of initial probabilities for the items. Must be the same length as the list of items and sum to approximately 1. Default is None, which means that it will assume uniform probability.

`ConvergentRandomChoice.choice(num=1)`
Returns random selection from items and updates probabilities.
: num: the number of items to return. Default is 1. Calling with any number above 1 is equivalent to calling this function multiple times.

Example:

```
In [1]: from ConvergentRandomChoice.ConvergentRandomChoice import ConvergentRandomChoice

In [2]: a = list(range(5))

In [3]: crc = ConvergentRandomChoice(a)

In [4]: print(crc)
Decay: 0.2
Items:
        0 : 0.2
        1 : 0.2
        2 : 0.2
        3 : 0.2
        4 : 0.2

In [5]: crc.choice()
Out[5]: [1]

In [6]: print(crc)
Decay: 0.2
Items:
        0 : 0.21000000000000002
        1 : 0.16
        2 : 0.21000000000000002
        3 : 0.21000000000000002
        4 : 0.21000000000000002

In [7]: crc = ConvergentRandomChoice(a, pchange=.5)

In [8]: print(crc)
Decay: 0.5
Items:
        0 : 0.2
        1 : 0.2
        2 : 0.2
        3 : 0.2
        4 : 0.2

In [9]: crc.choice()
Out[9]: [2]

In [10]: print(crc)
Decay: 0.5
Items:
        0 : 0.225
        1 : 0.225
        2 : 0.1
        3 : 0.225
        4 : 0.225

In [11]: crc.choice(5)
Out[11]: [1, 2, 2, 0, 4]

In [12]: print(crc)
Decay: 0.5
Items:
        0 : 0.1775482177734375
        1 : 0.2101409912109375
        2 : 0.1056488037109375
        3 : 0.3507659912109375
        4 : 0.15589599609375
```