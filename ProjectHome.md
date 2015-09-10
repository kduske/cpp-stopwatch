# Introduction #
Not surprisingly, Stopwatch is a class representing a stopwatch.

```
Stopwatch swatch;
```

A Stopwatch object can be used to measure execution time of code, algorithms, etc., the Stopwatch can be initialized in two time-taking modes, CPU time and real time (wall-clock time):

```
swatch.set_mode(REAL_TIME);
```

CPU time is the time spent by the processor on a certain piece of code, while real time is the real amount of time taken by a certain piece of code to execute (i.e. in general if you are doing hard work such as image or video editing on a different process the measured time will probably increase).

How does it work? Basically, one wraps the code to be measured with the following method calls:

```
swatch.start("My astounding algorithm");
// Hic est code
swatch.stop("My astounding algorithm");
```

A string representing the code ID is provided so that nested portions of code can be profiled separately:

```
swatch.start("My astounding algorithm");
		
swatch.start("My astounding algorithm - Super smart init");

// Initialization
swatch->stop("My astounding algorithm - Super smart init");
		
swatch.start("My astounding algorithm - Main loop");
// Loop
swatch.stop("My astounding algorithm - Main loop");
		
swatch.stop("My astounding algorithm");
```

Note: ID strings can be whatever you like, in the previous example I have used "My astounding algorithm - 

&lt;subpart&gt;

" only to enforce the fact that the measured code portions are part of My astounding algorithm, but there's no	connection between the three measurements.

If the code for a certain task is scattered through different files or portions of the same file one can use the start-pause-stop method:

```
swatch.start("Setup");
// First part of setup
swatch.pause("Setup");
		
swatch.start("Main logic");
// Main logic
swatch.stop("Main logic");
		
swatch.start("Setup");
// Cleanup (part of the setup)
swatch.stop("Setup");
```

Finally, to report the results of the measurements just run:

```
swatch.report("Code ID");
```

Thou can also provide an additional std::ostream& parameter to report() to redirect the logging on a different output. Also, you can use the get\_total/min/max/average\_time() methods to get the individual numeric data, without all the details of the logging. You can also extend Stopwatch to implement your own logging syntax.

To report all the measurements:

```
swatch.report_all();
```

Same as above, you can redirect the output by providing a std::ostream& parameter.

# Build #
The source code includes a Visual Studio 9 solution and an Xcode Project to build it. Linux users will know how to compile it, but a simple Makefile might be ready soon.

# License #
The software is provided under the GPLv3 license, read the LICENSE file in the source code for more details.

# Implementation notes #
The Stopwatch can be used in CPU\_TIME or REAL\_TIME modes. In the first mode it calculates the clock time which is spent on the process, i.e. CPU time spent on other processes is not considered, in the second mode the real-world time is used (and thus if you profile your code while editing a picture in Photoshop and ripping a DVD, those activities will affect the measured performance as well).

# Keep in touch #
I decided to release this code after letting it aging into my development directories for more than a year. Please note that this code is way not the best profiling tool available, there are more sophisticated ways to profile code around (see [this page](http://en.wikipedia.org/wiki/Profiling_%28computer_programming%29), but this just worked fine for me and I wanted to share it because I had to do some search before having it working both on Unix and on Windows. So if you have any suggestions on how to improve it, or you find it interesting and you decide to use it in your code, please just let me know. More details about how to contact me in the source code. :)

Tommaso Urli
