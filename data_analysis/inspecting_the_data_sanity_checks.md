# Inspecting the Data (Sanity Checks)

### Checking Data Columns

Now that our data is loaded with the variable `ms` (I chose it as an abbreviation of MakeScape), let's look at it and make sure it's sane. One of the first things I'll do is check the list of columns that our data comes with.

```python
list(ms.columns)
```

Which gives us the output

```python
[u'_id',
 u'ada_base_types',
 u'adage_version',
 u'application_name',
 u'application_version',
 u'board_mode',
 u'component_list',
 u'created_at',
 u'deviceInfo',
 u'fish',
 u'fish_list',
 u'game',
 u'game_id',
 u'key',
 u'mode_name',
 u'num_batteries',
 u'num_leds',
 u'num_resistors',
 u'num_timers',
 u'player_name',
 u'player_names',
 u'playspace_id',
 u'playspace_ids',
 u'reason',
 u'resistance',
 u'session_token',
 u'timed_out',
 u'timestamp',
 u'updated_at',
 u'user_id',
 u'virtual_context',
 u'visability_mode',
 u'voltage',
 'delta1',
 'delta2',
 'delta3',
 'delta4']
```

Whoa! That is [alot of columns](http://hyperboleandahalf.blogspot.com/2010/04/alot-is-better-than-you-at-everything.html). 33 columns, to be exact. We can check that by calling Python's function for determining the length of a collection:

```python
len(ms.columns) # returns 33
```

### Checking the First Few Rows

Now let's check the first few rows of data to make sure they look OK. Specifically, we'll want to check what types of events they were and when they happened. In our data, the event type is stored in a column named `key`, and the time is recorded in the `timestamp` column as a [UNIX Epoch timestamp](http://en.wikipedia.org/wiki/Unix_epoch) in milliseconds.

Thankfully, pandas dataframes have a handy little method called `head()`, which we can use to fetch the first $n$ rows of data. In the statement below we're calling `head()` on our `ms` dataframe, then we're indexing an additional list of columns to select just the columns we want; in this case `key` and `timestamp`

```python
columns = ['key', 'timestamp']
ms.head(n=5)[columns]
```




