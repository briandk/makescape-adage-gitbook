# Conclusion

We're not done analyzing this data; not even close. But, in doing our analyses we've done some really useful things:

1. In [Section 1](../data_analysis/loading_and_cleaning_the_data.html) we were able to load our data and sort it by timestamp.
2. [Section 2](../data_analysis/inspecting_the_data.html) helped us make sure our data were relatively clean, meaning they were well-formatted and loading the way we hoped
3. We then explored events by type in [Section 3](../data_analysis/exploring_events_by_type.html), where we found histograms and and the pandas `groupby()` function were powerful allies in understanding our data.
4. Exploring led to a problem, and in [Section 4](../data_analysis/why_are_there_so_many_makeconnectcomponent_events.html) we figured out we'd have to snap our fingers to the beat of [The Lion Sleeps Tonight ](https://www.youtube.com/watch?v=cU-eAzNp5Hw) by The Tokens 17 times to account for the number of connection events we witnessed.
5. In [Section 5](../data_analysis/visualizing_events_over_time.html) we introduced the Grammar of Graphics and the `ggplot` package to help us visualize the cumulative distribution of connection events.
6. In [Section 6](../data_analysis/working_with_time_deltas.html) we introduced `time deltas`: a way of seeing how much time elapsed between successive events. With their help we got a better sense of where the most active parts of our dataset were.
7. Finally, in [Section 7](../data_analysis/visualizing_time_deltas.html) we leveraged the power of small multiples and histograms to confirm our worst fears: either our players have superhuman speed or something is deeply wrong with how we detect and log connection events.

What remains, for starters, is to figure out exactly what's wrong. But look at how far we've come! Using open source tools, expressive scripting, and powerful graphics we've unearthed some really important things about our data. Ultimately, I hope this book has given you a taste of what's possible with a game data collection framework and scripted, reproducible analyses. 

Python on, my friends.
