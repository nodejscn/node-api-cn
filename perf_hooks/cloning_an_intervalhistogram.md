
{IntervalHistogram} instances can be cloned via {MessagePort}. On the receiving
end, the histogram is cloned as a plain {Histogram} object that does not
implement the `enable()` and `disable()` methods.

