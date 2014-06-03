# Inspecting the Data

### How Much Data Is There?

One of the first things I'll do is check the list of columns that our data comes with.

```python
ms.columns
```

Which gives us the output

```python
Index([u'_id', u'ada_base_types', u'adage_version', u'application_name', u'application_version', u'board_mode', u'component_list', u'created_at', u'deviceInfo', u'fish', u'fish_list', u'game', u'game_id', u'key', u'mode_name', u'num_batteries', u'num_leds', u'num_resistors', u'num_timers', u'player_name', u'player_names', u'playspace_id', u'playspace_ids', u'reason', u'resistance', u'session_token', u'timed_out', u'timestamp', u'updated_at', u'user_id', u'virtual_context', u'visability_mode', u'voltage', u'human-readable-timestamps', u'human-readable-timestamp'], dtype='object')
```

Whoa! That is [alot of columns](http://hyperboleandahalf.blogspot.com/2010/04/alot-is-better-than-you-at-everything.html). 33 columns, to be exact. You might be wondering why each column name starts with a "u," as in `u'num_leds'` and `u'_id`. That's actually because internally, [Python is representing those strings as Unicode strings](http://www.diveintopython3.net/strings.html#one-ring-to-rule-them-all) and it's [letting us know](https://docs.python.org/2/howto/unicode.html#the-unicode-type).

We can double-check exactly how many columns are in our data by calling Python's function for determining the length of a collection:

```python
len(ms.columns) # returns 33
```

But we should also check how many rows (in this case, how many distinct gameplay events) we have in our dataset.

```python
len(ms) # returns 8505
```

Phew! 8505 rows of data.

### Checking the First Few Rows

Now let's check the first few rows of data to make sure they look OK. Specifically, we'll want to check what types of events they were and when they happened. In our data, the event type is stored in a column named `key`, and the time is recorded in the `timestamp` column as a [UNIX Epoch timestamp](http://en.wikipedia.org/wiki/Unix_epoch) in milliseconds.

Thankfully, pandas dataframes have a handy little method called `head()`, which we can use to fetch the first $n$ rows of data. In the statement below we're calling `head()` on our `ms` dataframe, then we're indexing an additional list of columns to select just the columns we want; in this case `key` and `timestamp`

```python
columns = ['key', 'timestamp']
ms.head(n=5)[columns]
```

<table>
<colgroup>
<col style="text-align:left;"/>
<col style="text-align:left;"/>
<col style="text-align:left;"/>
</colgroup>

<thead>
<tr>
	<th style="text-align:left;"></th>
	<th style="text-align:left;">key</th>
	<th style="text-align:left;">timestamp</th>
</tr>
</thead>

<tbody>
<tr>
	<td style="text-align:left;">0</td>
	<td style="text-align:left;">ADAGEStartSession</td>
	<td style="text-align:left;">1398178271860</td>
</tr>
<tr>
	<td style="text-align:left;">1</td>
	<td style="text-align:left;">ADAGEStartSession</td>
	<td style="text-align:left;">1398190767768</td>
</tr>
<tr>
	<td style="text-align:left;">2</td>
	<td style="text-align:left;">ADAGEStartSession</td>
	<td style="text-align:left;">1398191616469</td>
</tr>
<tr>
	<td style="text-align:left;">3</td>
	<td style="text-align:left;">ADAGEStartSession</td>
	<td style="text-align:left;">1398192512628</td>
</tr>
<tr>
	<td style="text-align:left;">4</td>
	<td style="text-align:left;">ADAGEStartSession</td>
	<td style="text-align:left;">1398192887546</td>
</tr>
</tbody>
</table>

What's less-than-helpful right now is that those timestamps are just raw integers. We want to make sure those integers actually represent times when data could reasonably have been collected (and not, say, January of the year 47532, which actually happened once).

Thankfully, pandas comes with a function that can convert UNIX Epoch Time integers into human-recognizable dates. In this case, what we'll do is create a new column called `human-readable-timestamps` by applying the pandas `Timestamp()` function to our existing integers. Then we'll check the data.

```python
ms['human-readable-timestamp'] = ms.timestamp.apply(lambda x: pd.Timestamp(x, unit='ms'))
columns = ['key', 'timestamp', 'human-readable-timestamp']
ms[columns].head()
```

<table>
<colgroup>
<col style="text-align:left;"/>
<col style="text-align:left;"/>
<col style="text-align:left;"/>
<col style="text-align:left;"/>
</colgroup>

<thead>
<tr>
	<th style="text-align:left;"></th>
	<th style="text-align:left;">key</th>
	<th style="text-align:left;">timestamp</th>
	<th style="text-align:left;">human-readable-timestamp</th>
</tr>
</thead>

<tbody>
<tr>
	<td style="text-align:left;">0</td>
	<td style="text-align:left;">ADAGEStartSession</td>
	<td style="text-align:left;">1398178271860</td>
	<td style="text-align:left;">2014&#8211;04&#8211;22 14:51:11.860000</td>
</tr>
<tr>
	<td style="text-align:left;">1</td>
	<td style="text-align:left;">ADAGEStartSession</td>
	<td style="text-align:left;">1398190767768</td>
	<td style="text-align:left;">2014&#8211;04&#8211;22 18:19:27.768000</td>
</tr>
<tr>
	<td style="text-align:left;">2</td>
	<td style="text-align:left;">ADAGEStartSession</td>
	<td style="text-align:left;">1398191616469</td>
	<td style="text-align:left;">2014&#8211;04&#8211;22 18:33:36.469000</td>
</tr>
<tr>
	<td style="text-align:left;">3</td>
	<td style="text-align:left;">ADAGEStartSession</td>
	<td style="text-align:left;">1398192512628</td>
	<td style="text-align:left;">2014&#8211;04&#8211;22 18:48:32.628000</td>
</tr>
<tr>
	<td style="text-align:left;">4</td>
	<td style="text-align:left;">ADAGEStartSession</td>
	<td style="text-align:left;">1398192887546</td>
	<td style="text-align:left;">2014&#8211;04&#8211;22 18:54:47.546000</td>
</tr>
</tbody>
</table>

Looking good! Our data seems to have loaded sensibly, and now it's time for some basic analysis.


