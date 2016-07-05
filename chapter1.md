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
url1 = 'https://s3.amazonaws.com/assets.datacamp.com/production/course_1273/datasets/df1.csv'
url2 = 'https://s3.amazonaws.com/assets.datacamp.com/production/course_1273/datasets/df2.csv'
url3 = 'https://s3.amazonaws.com/assets.datacamp.com/production/course_1273/datasets/messy.csv'

df1 = pd.read_csv(url1, sep = ',')
df2 = pd.read_csv(url2, sep = ',')
messy = pd.read_csv(url3, sep=',')
```

*** =sct
```{r}
# SCT written with pythonwhat: https://github.com/datacamp/pythonwhat/wiki

msg_bad = "That is not correct!"
msg_success = "Exactly!"
test_mc(4, [msg_bad, msg_bad, msg_bad, msg_success])
```

--- type:NormalExercise lang:python xp:100 skills:1 key:431ad8bd98
## Melt

In df2, avg\_free, avg\_reduced, and avg\_full, each representing the number of students that pay for a particular meal plan on an average day, are three different observations and should be in three different rows. A great tool to achieve this is the melt function in pandas package. Its basic syntax is `df.melt(df, id_vars=l)`, where df is the name of the dataframe we're dealing with and l is a list of all the columns that we want to maintain. All the other columns will be "molten" together in different rows. To get a more concrete idea, try melt yourself!

*** =instructions
- Import `pandas` as `pd`
- Melt df2! We want to maintain the `year` column and melt all the rest.

*** =hint
- `id_vars` should be `['year']`

*** =pre_exercise_code
```{python}
import pandas as pd
url2 = 'https://s3.amazonaws.com/assets.datacamp.com/production/course_1273/datasets/df2.csv'
df2 = pd.read_csv(url2, sep = ',')
```

*** =sample_code
```{python}
# Import pandas as pd


# Melt df2 into df2_tidy
df2_tidy = 

# print df2_tidy
print(df2_tidy)

```

*** =solution
```{python}
# Import pandas as pd
import pandas as pd

# Melt df2 into df2_tidy
df2_tidy = pd.melt(df2, id_vars=['year'])

# print df2_tidy
print(df2_tidy)

```

*** =sct
```{python}
test_import("pandas")
test_data_frame("df2_tidy", columns = ["year", "variable", "value"])
success_msg("Great job!")
```

--- type:NormalExercise lang:python xp:100 skills:1 key:3be71779cd
## Renaming Columns

Did you see how easy it was? In one command you already tidied up your dataset! Now we just need a bit more decorations. Change the column names with pandas' rename function. Its syntax is `df.rename(columns = {'$column1':'column1','$column2':'column2'}, inplace = True)`, where `$column 1`, `$column 2` etc. are original column names and `column 1`, `column 2` etc. are new column names.


*** =instructions
- `pandas` is already imported
- Rename the `variable` of df2_tidy to `meal plan` and `value` to `number` 

*** =hint
- `columns` should be `{'variable':'meal plan','value':'number'}`

*** =pre_exercise_code
```{python}
import pandas as pd
url2 = 'https://s3.amazonaws.com/assets.datacamp.com/production/course_1273/datasets/df2.csv'
df2 = pd.read_csv(url2, sep = ',')
df2_tidy = pd.melt(df2, id_vars=['year'])
```

*** =sample_code
```{python}
import pandas as pd

# Rename the columns of df2_tidy


# print out df2_tidy again
print(df2_tidy)

```

*** =solution
```{python}
import pandas as pd

# Rename the columns of df2_tidy
df2_tidy.rename(columns = {'variable':'lunch option','value':'people'}, inplace = True)

# print out df2_tidy again
print(df2_tidy)

```

*** =sct
```{python}
test_import("pandas")
test_data_frame("df2_tidy", columns = ["year", "lunch option", "people"])
success_msg("Great job!")
```



--- type:MultipleChoiceExercise lang:python xp:50 skills:1 key:d40684ea0d
## More messiness

Great job! Now that you're familier with messy and tidy data, take a look at another dataset. Enter `eye_color` in your shell. What problem does this dataset have?

*** =instructions
- It violates rule #1: there are several columns that represent the same variable
- It violates rule #1: there are several variables represented in the same column
- It violates rule #2: there are several rows that represent the same observation
- It violates rule #2: there are several observations represented in the same row

*** =hint
Try again!

*** =pre_exercise_code
```{r}
# The pre exercise code runs code to initialize the user's workspace.
# You can use it to load packages, initialize datasets and draw a plot in the viewer

import pandas as pd
url4 = 'https://s3.amazonaws.com/assets.datacamp.com/production/course_1273/datasets/eye_color.csv'
eye_color = pd.read_csv(url4,sep=',')

```

*** =sct
```{r}
# SCT written with pythonwhat: https://github.com/datacamp/pythonwhat/wiki

msg_bad = "That is not correct!"
msg_success = "Exactly!"
test_mc(1, [msg_success, msg_bad, msg_bad, msg_bad])
```

--- type:NormalExercise lang:python xp:100 skills:1 key:5d0f6f3efd
## Deal with it!

The three columns, `black`, `blue`, and `brown`, essentially represent the same variable: eye color. It would make much more sense to merge them into one column. Use melt to do it!

*** =instructions
- Melt `black`, `blue`, and `brown` into one column
- Rename the `variable` column to `Eye Color`

*** =hint
- The basic syntax for melt is `df.melt(df, id_vars=l)`
- The basic syntax for rename is  `df.rename(columns = {'$column1':'column1','$column2':'column2'}, inplace = True)`


*** =pre_exercise_code
```{python}
import pandas as pd
url4 = 'https://s3.amazonaws.com/assets.datacamp.com/production/course_1273/datasets/eye_color.csv'
eye_color = pd.read_csv(url4,sep=',')
```

*** =sample_code
```{python}
# Melt the `black`, `blue` and `brown` columns of eye_color and save it to eye_color_tidy
eye_color_tidy = 

# Rename the `variable` column


# print out eye_color_tidy
print(eye_color_tidy)

```

*** =solution
```{python}
# Melt the `black`, `blue` and `brown` columns of eye_color and save it to eye_color_tidy
eye_color_tidy = pd.melt(eye_color, id_vars = ['Name'])

# Rename the `variable` column
eye_color_tidy.rename(columns = {'variable':'Eye Color'}, inplace = True)

# print out eye_color_tidy
print(eye_color_tidy)

```

*** =sct
```{python}
test_import("pandas")
test_data_frame("eye_color_tidy", columns = ["Name", "Eye Color", "value"])
success_msg("Great job!")
```

--- type:NormalExercise lang:python xp:100 skills:1 key:99639b8387
## Further Cleaning

What did you notice? Why the three columns melt into one, the dataset still has some problems. First of all, when we know Elizabeth has brown eyes, it's redundant to keep record that she doesn't have blue or black eyes. Therefore, what we waht to do is to get rid of all rows whose value in the `value` column is 0. It is very easy to do so in pandas, just use the following command:

`df = df[df.column == value]`

where `column` is the name of the column we are examining and `value` is the value we want to keep. This step will give us one row for each girl that tells us only her correct eye color. Now the `value` column is no longer necessary and let's delete it:

`del df['column1', 'column2'...]`

This command does exactly what we want.


*** =instructions
- Filter the dataset to keep only the rows where `value` is 1 
- Delete the `value` column

*** =hint
Take a closer look at the syntax of the two commands!

*** =pre_exercise_code
```{python}
import pandas as pd
url4 = 'https://s3.amazonaws.com/assets.datacamp.com/production/course_1273/datasets/eye_color.csv'
eye_color = pd.read_csv(url4,sep=',')
eye_color_tidy = pd.melt(eye_color, id_vars = ['Name'])
```

*** =sample_code
```{python}
# Filter eye_color_tidy 
eye_color_tidy = 

# Delete the `value` column


# print eye_color_tidy again
print(eye_color_tidy)
```

*** =solution
```{python}
# Filter eye_color_tidy 
eye_color_tidy = eye_color_tidy[eye_color_tidy.value == 1]

# Delete the `value` column
del eye_color_tidy['value']

# print eye_color_tidy again
print(eye_color_tidy)
```

*** =sct
```{python}
test_import("pandas")
test_function("del", args=[eye_color_tidy['value']])
test_data_frame("eye_color_tidy", columns = ["Name", "Eye Color"])
success_msg("Great job!")
```

