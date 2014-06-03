# Visualizing Time Deltas

So, we know the *distribution* of `MakeConnectComponent` events is uneven. We know that because in the last section we plotted the cumulative distribution function and saw it had a widely variable slope. What I'd like to do now is get an idea of just what that distribution of elapsed event times looks like.

To do that, we're going to use a visualization called a [kernel density estimate](http://en.wikipedia.org/wiki/Kernel_density_estimate). Essentially, what we're doing is creating a smoothed empirical approximation of what the distributions of events look like. 

We're also going to use another powerful feature of graphical analysis: what statistician [Bill Cleveland][http://cm.bell-labs.com/cm/ms/departments/sia/wsc/] and [Edward Tufte](http://www.amazon.com/The-Visual-Display-Quantitative-Information/dp/0961392142/ref=sr_1_1?ie=UTF8&qid=1401770677&sr=8-1&keywords=visual+display+of+quantitative+information) call "[small multiples](http://www.juiceanalytics.com/writing/better-know-visualization-small-multiples)." We're actually going to take a look at the distributions of time deltas for the top 5 most frequent kinds of events and graphically compare them. 

```python
topFive = loadDataSortedByTimestamp(filepath)
topFiveMostFrequentEvents = list(ms.groupby('key').count().sort(columns=['timestamp']).index)[-5:]
frequencyFilter = topFive.key.apply(lambda x: x in topFiveMostFrequentEvents)
topFive['delta1'] = topFive.timestamp.diff()
topFive = topFive[frequencyFilter]


p = ggplot(aes(x = 'delta1', 
               group='key'), 
           data=topFive)
p = p + geom_density() # a Kernel Density Estimate
p = p + scale_x_continuous(limits=[-1000, 20000])
p = p + facet_wrap(y='key', 
                   ncol=1, 
                   scales='free_y')
p = p + xlab('Time Between Successive Events (ms)')
p = p + ggtitle('Smoothed Kernel Density Estimates')

print(p)
ggsave(plot=p,
       filename='kernelDensityEstimate.png')
```

![Small multiples of kernel density estimates](../assets/kernelDensityEstimate.png)