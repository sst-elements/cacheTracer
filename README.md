# cacheTracer

cacheTracer can be used to generate a trace of events between any CPU and  memHierarchy components. It has two ports
namely "northBus" (connects to the  component on CPU side) and "southBus" (connects to the component towards the 
memory). This component also keeps track of the addresses of the messages  (memEvents) passing through from its one port
to another. It then performs  following tasks:

1. Count number of events occurring from one port to another.

2. Generates a histogram of addresses of memEvents passing through it.

3. It assumes first message with a given event-ID would pass from northBus to  southBus and response message would go
from southBus to northBus. With this  assumption, for every event-ID it calculates the time between the event-ID 
appears on northBus and its response on southBus. The difference time is  defined as "Access Latency". The access
latencies are recorded in  nanoseconds (ns). At the end of the simulation, a histogram is build for all  the memEvents
passing through it.

## Input parameters for cacheTracer

- __clock__: Frequency of operation (should be set to be same as CPU frequency).

- __debug__: Print out debug info with increasing verbosity. To generate an  address tracer of events, set debug=8 and
provide filename in tracePrefix.

- __tracePrefix__: Filename for output trace-file generated when debug=8 is set.  If no value is set, trace would NOT be
written. The trace is NOT dumped to  stdout. Depending on the simulation time, the trace file can become very  large in
GB's. At this point, compression on the trace file is not implemented. It is basically a txt file.

- __statistics__: Flag indicates whether to print stats at the end of the  execution. 1= print stats, 0-don't print
stats.

- __statsPrefix__: Filename for output file where statistics would be dumped if  "statistics" is set. If filename is NOT
provided and "statistics" is set,  stats would be printed to stdout.

- __pageSize__: This value is used to set size of an individual bin in address  histogram. Default value is set to 4096
(4k).

- __accessLatencyBins__: This value is used to set total number of bins for  access-latency histogram. Default value is
10. 

Note that the use of pageSize and accessLatencyBins are different, pageSize  indicates the size of one individual bin of
histogram, and can result in large  number of bins in the actual histogram (provides an ability to count how many 
references occured to a particular memory page); whereas accessLatencyBins  indicates total number of bins that can be
there in the histogram.

