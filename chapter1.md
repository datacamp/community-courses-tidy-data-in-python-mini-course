---
title       : Tidy Data in Python
description : It is often said that data scientists spend only 20% of their time analyzing their data, and 80% of time cleaning the data. Indeed, maintaining a tidy, easy-to-use dataset is crucial in our age of big data. In Tidy Data, veteran statistician Hadley Wickham gives standards of tidy and messy data so that all data scientists can keep their work organized. In this mini-course, you'll learn to transform messy datasets to tidy datasets using the pandas package in python. Let's get started!

attachments :

--- type:MultipleChoiceExercise lang:python xp:50 skills:1 key:7ad68bd87f
## Tidy Data and Messy Data

What exactly marks the difference between tidy data and messy data? It is not only how organized and intuitive the datasets look in our human eyes, but also how easily and efficiently they can be processed by computers. In Tidy Data, Hadley Wickham proposed three standards for tidy data:

1. Each variable forms a column
2. Each observation forms a row
3. Each type of observation forms a unit

In this course, we'll focus on the first two rules and show you how we can use pandas to deal with datasets violating them. To get started, enter "messy" in the ipython shell to see a preloaded dataset. Observe its struture in comparison with Wickham's rules. This dataset is messy because it violates rule #2: it combines Treatment A and Treatment B, two distinct observations, in a single row. While this may look more succinct, it would, for instance, take unnecessary time and space for a data scientist that only wants to study Treatment A. 

Now let's look at two more datasets. Enter "df1" and "df2" in your shell to check out two other preloaded datasets. Which one of them is messy, and why?

*** =instructions
- df1 is messy because it violates rule #1
- df1 is messy because it violates rule #2
- df2 is messy because it violates rule #1
- df2 is messy because it violates rule #2
 
*** =hint
What are the observations and variables in these two datasets?

*** =pre_exercise_code
```{r}
# The pre exercise code runs code to initialize the user's workspace.
import pandas as pd
messy = pd.read_csv('datasets/messy.csv', sep=',')
df1 = pd.read_csv('datasets/df1.csv', sep = ',')
df2 = pd.read_csv('datasets/df2.csv', sep = ',')
```

*** =sct
```{r}
# SCT written with pythonwhat: https://github.com/datacamp/pythonwhat/wiki

msg_bad = "That is not correct!"
msg_success = "Exactly! The correlation is very weak though."
test_mc(4, [msg_bad, msg_bad, msg_bad, msg_success])
```

--- type:NormalExercise lang:python xp:100 skills:1 key:431ad8bd98
## Plot the movies yourself

Do you remember the plot of the last exercise? Let's make an even cooler plot!

A dataset of movies, `movies`, is available in the workspace.

*** =instructions
- The first function, `np.unique()`, uses the `unique()` function of the `numpy` package to get integer values for the movie genres. You don't have to change this code, just have a look!
- Import `pyplot` in the `matplotlib` package. Set an alias for this import: `plt`.
- Use `plt.scatter()` to plot `movies.runtime` onto the x-axis, `movies.rating` onto the y-axis and use `ints` for the color of the dots. You should use the first and second positional argument, and the `c` keyword.
- Show the plot using `plt.show()`.

*** =hint
- You don't have to program anything for the first instruction, just take a look at the first line of code.
- Use `import ___ as ___` to import `matplotlib.pyplot` as `plt`.
- Use `plt.scatter(___, ___, c = ___)` for the third instruction.
- You'll always have to type in `plt.show()` to show the plot you created.

*** =pre_exercise_code
```{python}
import pandas as pd
movies = pd.read_csv("http://s3.amazonaws.com/assets.datacamp.com/course/introduction_to_r/movies.csv")

import numpy as np
```

*** =sample_code
```{python}
# Get integer values for genres
_, ints = np.unique(movies.genre, return_inverse = True)

# Import matplotlib.pyplot


# Make a scatter plot: runtime on  x-axis, rating on y-axis and set c to ints


# Show the plot

```

*** =solution
```{python}
# Get integer values for genres
_, ints = np.unique(movies.genre, return_inverse = True)

# Import matplotlib.pyplot
import matplotlib.pyplot as plt

# Make a scatter plot: runtime on  x-axis, rating on y-axis and set c to ints
plt.scatter(movies.runtime, movies.rating, c=ints)

# Show the plot
plt.show()
```

*** =sct
```{python}
# SCT written with pythonwhat: https://github.com/datacamp/pythonwhat/wiki

test_function("numpy.unique",
              not_called_msg = "Don't remove the call of `np.unique` to define `ints`.",
              incorrect_msg = "Don't change the call of `np.unique` to define `ints`.")

test_object("ints",
            undefined_msg = "Don't remove the definition of the predefined `ints` object.",
            incorrect_msg = "Don't change the definition of the predefined `ints` object.")

test_import("matplotlib.pyplot", same_as = True)

test_function("matplotlib.pyplot.scatter",
              incorrect_msg = "You didn't use `plt.scatter()` correctly, have another look at the instructions.")

test_function("matplotlib.pyplot.show")

success_msg("Great work!")
```

--- type:MultipleChoiceExercise lang:python xp:50 skills:1 key:d40684ea0d
## More messiness

Have a look at the plot that showed up in the viewer to the right. Which type of movies have the worst rating assigned to them?

*** =instructions
- Long movies, clearly
- Short movies, clearly
- Long movies, but the correlation seems weak
- Short movies, but the correlation seems weak

*** =hint
Have a look at the plot. Do you see a trend in the dots?

*** =pre_exercise_code
```{r}
# The pre exercise code runs code to initialize the user's workspace.
# You can use it to load packages, initialize datasets and draw a plot in the viewer

import pandas as pd
import matplotlib.pyplot as plt

movies = pd.read_csv("http://s3.amazonaws.com/assets.datacamp.com/course/introduction_to_r/movies.csv")

plt.scatter(movies.runtime, movies.rating)
plt.show()
```

*** =sct
```{r}
# SCT written with pythonwhat: https://github.com/datacamp/pythonwhat/wiki

msg_bad = "That is not correct!"
msg_success = "Exactly! The correlation is very weak though."
test_mc(4, [msg_bad, msg_bad, msg_bad, msg_success])
```
