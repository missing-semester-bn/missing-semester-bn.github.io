---
layout: lecture
title: "Debugging and Profiling"
date: 2020-01-23
ready: true
video:
  aspect: 56.25
  id: l812pUnKxME
---

প্রোগ্রামিং-এর একটি সুবর্ণ নিয়ম হল যে কোড আপনি যা করতে চান তা করে না, বরং আপনি যা করতে বলেন তা করে।
এই ব্যবধানটি পূরণ করা কখনও কখনও বেশ কঠিন কাজ হতে পারে।
এই বক্তৃতায় আমরা বাগ এবং রিসোর্স ক্ষুধার্ত কোডের সাথে মোকাবিলা করার জন্য দরকারী কৌশলগুলি কভার করতে যাচ্ছিঃ ডিবাগিং এবং প্রোফাইলিং।

#ডিবাগিং

#প্রিন্টফ ডিবাগিং এবং লগিং

"সবচেয়ে কার্যকর ডিবাগিং টুল হল এখনও সতর্কতার সাথে চিন্তা করা, যুক্তিসঙ্গতভাবে মুদ্রণ বিবৃতি সহ"-ব্রায়ান কের্নিঘান, _ ইউনিক্স ফর বিগিনার্স।

কোনও প্রোগ্রাম ডিবাগ করার প্রথম পদ্ধতি হল যেখানে আপনি সমস্যাটি সনাক্ত করেছেন তার চারপাশে মুদ্রণ বিবৃতি যুক্ত করা এবং সমস্যার জন্য কী দায়ী তা বোঝার জন্য পর্যাপ্ত তথ্য বের না করা পর্যন্ত পুনরাবৃত্তি করা।

দ্বিতীয় পদ্ধতিটি হল অ্যাডহক প্রিন্ট স্টেটমেন্টের পরিবর্তে আপনার প্রোগ্রামে লগ ইন করা। লগিং বিভিন্ন কারণে নিয়মিত মুদ্রণ বিবৃতির চেয়ে ভালঃ

- আপনি স্ট্যান্ডার্ড আউটপুটের পরিবর্তে ফাইল, সকেট বা এমনকি দূরবর্তী সার্ভারে লগ করতে পারেন।
লগিং তীব্রতার মাত্রা (যেমন তথ্য, ডিবাগ, সতর্কতা, ত্রুটি, এবং সি) সমর্থন করে যা আপনাকে সেই অনুযায়ী আউটপুট ফিল্টার করতে দেয়।
- নতুন সমস্যাগুলির জন্য, আপনার লগগুলিতে কী ভুল হচ্ছে তা সনাক্ত করার জন্য পর্যাপ্ত তথ্য থাকার যথেষ্ট সম্ভাবনা রয়েছে।

[এখানে] (/static/files/logger. py) একটি উদাহরণ কোড যা বার্তা লগ করেঃ

```bash
$ python logger.py
# Raw output as with just prints
$ python logger.py log
# Log formatted output
$ python logger.py log ERROR
# Print only ERROR levels and above
$ python logger.py color
# Color formatted output
```

লগগুলিকে আরও পাঠযোগ্য করার জন্য আমার প্রিয় পরামর্শগুলির মধ্যে একটি হল সেগুলিকে রঙিন কোড করা।
এতদিনে আপনি সম্ভবত বুঝতে পেরেছেন যে আপনার টার্মিনালটি জিনিসগুলিকে আরও পাঠযোগ্য করে তুলতে রঙ ব্যবহার করে। কিন্তু এটা কিভাবে করা হয়?
'ls' বা 'grep' এর মতো প্রোগ্রামগুলি [ANSI পালানোর কোড] (https://en.wikpedia.org/wiki/ANSI_escape_code) ব্যবহার করছে যা আপনার শেলকে আউটপুটের রঙ পরিবর্তন করতে নির্দেশ করার জন্য অক্ষরের বিশেষ ক্রম। উদাহরণস্বরূপ, 'echo-e "এক্সিকিউট করা হচ্ছে [38; 2; 255; 0; 0mএটি লাল\e [0m "'আপনার টার্মিনালে লাল রঙে' এটি লাল 'বার্তাটি প্রিন্ট করে, যতক্ষণ না এটি [সত্য রঙ] সমর্থন করে (https://github.com/ termstandard/colors #truecolor-support-in-output-devices) যদি আপনার টার্মিনাল এটি সমর্থন করে না (e.g। macOS এর Terminal.app) আপনি 16 টি রঙ পছন্দের জন্য আরও সর্বজনীনভাবে সমর্থিত পালানোর কোডগুলি ব্যবহার করতে পারেন, উদাহরণস্বরূপ 'echo-e' \e [31; 1m]এটি লাল\e [0m "'।

নিচের স্ক্রিপ্টটি দেখায় কিভাবে আপনার টার্মিনালে অনেক আরজিবি রঙ মুদ্রণ করা যায়। (যতক্ষণ এটি true color সমর্থন করে).


```bash
#!/usr/bin/env bash
for R in $(seq 0 20 255); do
    for G in $(seq 0 20 255); do
        for B in $(seq 0 20 255); do
            printf "\e[38;2;${R};${G};${B}m█\e[0m";
        done
    done
done
```

## তৃতীয় পক্ষের লগ

আপনি যখন বৃহত্তর সফ্টওয়্যার সিস্টেম তৈরি করতে শুরু করবেন তখন আপনি সম্ভবত নির্ভরশীলতার সম্মুখীন হবেন যা পৃথক প্রোগ্রাম হিসাবে চলে।
ওয়েব সার্ভার, ডাটাবেস বা বার্তা দালাল এই ধরনের নির্ভরতার সাধারণ উদাহরণ।
এই সিস্টেমগুলির সাথে যোগাযোগ করার সময় প্রায়শই তাদের লগগুলি পড়া প্রয়োজন, কারণ ক্লায়েন্ট পার্শ্ব ত্রুটি বার্তা যথেষ্ট নাও হতে পারে।

সৌভাগ্যবশত, বেশিরভাগ প্রোগ্রাম আপনার সিস্টেমের কোথাও তাদের নিজস্ব লগ লেখে।
ইউনিক্স সিস্টেমে, প্রোগ্রামগুলির জন্য '/var/log' এর অধীনে তাদের লগ লেখা সাধারণ বিষয়।
উদাহরণস্বরূপ, [NGINX] (https://www.nginx.com/) ওয়েব সার্ভার তার লগগুলি '/var/log/nginx' এর অধীনে রাখে।
আরও সম্প্রতি, সিস্টেমগুলি একটি * * সিস্টেম লগ * * ব্যবহার করতে শুরু করেছে, যা ক্রমবর্ধমান যেখানে আপনার সমস্ত লগ বার্তা যায়।
বেশিরভাগ (তবে সবগুলি নয়) লিনাক্স সিস্টেমে 'systemd' ব্যবহার করা হয়, একটি সিস্টেম ডেমন যা আপনার সিস্টেমে অনেক কিছু নিয়ন্ত্রণ করে যেমন কোন পরিষেবাগুলি সক্রিয় এবং চলছে।
'systemd' একটি বিশেষ বিন্যাসে '/var/log/জার্নাল' এর অধীনে লগগুলি স্থাপন করে এবং আপনি ['Journalctl'] (https://www.man7.org/linux/man-pages/man1/journalctl.1.html) কমান্ডটি বার্তা প্রদর্শন করতে ব্যবহার করতে পারেন।
একইভাবে, ম্যাকোসে এখনও '/var/log/system. log' রয়েছে তবে ক্রমবর্ধমান সংখ্যক সরঞ্জাম সিস্টেম লগ ব্যবহার করে, যা ['log show'] এর সাথে প্রদর্শিত হতে পারে (https://www.manpagez.com/man/1/log/)
বেশিরভাগ ইউনিক্স সিস্টেমে আপনি কার্নেল লগ অ্যাক্সেস করতে ['dmesg'] (https://www.man7.org/linux/man-pages/man1/dmesg.1.html) কমান্ড ব্যবহার করতে পারেন।

সিস্টেম লগ অধীনে লগিং জন্য আপনি ব্যবহার করতে পারেন ['লগার'] (https://www.man7.org/linux/man-pages/man1/logger.1.html) শেল প্রোগ্রাম।
এখানে 'লগার' ব্যবহার করার একটি উদাহরণ এবং কীভাবে এন্ট্রিটি সিস্টেম লগগুলিতে তৈরি হয়েছে কিনা তা পরীক্ষা করা যায়।
অধিকন্তু, বেশিরভাগ প্রোগ্রামিং ভাষায় সিস্টেম লগ-এ বাইন্ডিং লগিং থাকে।

```bash
logger "Hello Logs"
# On macOS
log show --last 1m | grep Hello
# On Linux
journalctl --since "1m ago" | grep Hello
```

আমরা যেমন ডেটা রেঙ্গলিং বক্তৃতায় দেখেছি, লগগুলি বেশ শব্দবহুল হতে পারে এবং আপনি যে তথ্য চান তা পেতে তাদের কিছু স্তরের প্রক্রিয়াকরণ এবং ফিল্টারিং প্রয়োজন।
আপনি যদি 'জার্নালেক্টল' এবং 'লগ শো'-এর মাধ্যমে নিজেকে প্রচুর পরিমাণে ফিল্টার করতে দেখেন তবে আপনি তাদের ফ্ল্যাগগুলি ব্যবহার করার কথা বিবেচনা করতে পারেন, যা তাদের আউটপুট ফিল্টার করার প্রথম পাস সম্পাদন করতে পারে।
['lnav'] (http://lnav.org/) এর মতো কিছু সরঞ্জাম রয়েছে যা লগ ফাইলগুলির জন্য একটি উন্নত উপস্থাপনা এবং নেভিগেশন সরবরাহ করে।

##ডিবাগারস

প্রিন্টএফ ডিবাগিং যথেষ্ট না হলে আপনার একটি ডিবাগার ব্যবহার করা উচিত।
ডিবাগার হল এমন প্রোগ্রাম যা আপনাকে একটি প্রোগ্রাম সম্পাদনের সাথে যোগাযোগ করতে দেয়, যা নিম্নলিখিতগুলিকে অনুমতি দেয়ঃ

- একটি নির্দিষ্ট লাইনে পৌঁছলে প্রোগ্রামের এক্সিকিউশন বন্ধ করুন।
- প্রোগ্রামের মাধ্যমে একবারে একটি নির্দেশের মাধ্যমে পদক্ষেপ নিন।
- প্রোগ্রাম ক্র্যাশ হওয়ার পর ভেরিয়েবলের মান পরীক্ষা করুন।
- একটি নির্দিষ্ট শর্ত পূরণ হলে শর্তসাপেক্ষে মৃত্যুদণ্ড কার্যকর করা বন্ধ করুন।
- এবং আরও অনেক উন্নত বৈশিষ্ট্য

অনেক প্রোগ্রামিং ভাষা কিছু ধরনের ডিবাগার নিয়ে আসে।
পাইথনে এটি পাইথন ডিবাগার ['pdb'] (https://docs.python.org/3/library/pdb.html)

এখানে 'পিডিবি' সমর্থিত কয়েকটি কমান্ডের সংক্ষিপ্ত বিবরণ দেওয়া হলঃ

- * * l * * (IST)-বর্তমান লাইনের চারপাশে 11 টি লাইন প্রদর্শন করে বা পূর্ববর্তী তালিকাটি চালিয়ে যায়।
- * * এস * * (টেপ)-বর্তমান লাইনটি কার্যকর করুন, প্রথম সম্ভাব্য অনুষ্ঠানে থামুন।
- * * n * * (ext)-বর্তমান ফাংশনের পরবর্তী লাইনটি পৌঁছানো বা এটি ফিরে না আসা পর্যন্ত কার্যকর করা চালিয়ে যান।
- * * বি * * (রেক)-একটি ব্রেকপয়েন্ট সেট করুন (depending on the argument provided).
- * * পি * * (রিন্ট)-বর্তমান প্রসঙ্গে অভিব্যক্তিটি মূল্যায়ন করুন এবং এর মান মুদ্রণ করুন। এর পরিবর্তে ['pprint'] (https://docs.python.org/3/library/pprint.html) ব্যবহার করে প্রদর্শন করতে * * pp * * রয়েছে।
- * * r * * (eturn)-বর্তমান ফাংশন ফেরত না হওয়া পর্যন্ত মৃত্যুদন্ড কার্যকর করা চালিয়ে যান।
- * * q * * (uit)-ডিবাগার বন্ধ করুন।

আসুন নিম্নলিখিত বাগি পাইথন কোডটি ঠিক করতে 'পিডিবি' ব্যবহার করার একটি উদাহরণ দেখি। (See the lecture video).



```python
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        for j in range(n):
            if arr[j] > arr[j+1]:
                arr[j] = arr[j+1]
                arr[j+1] = arr[j]
    return arr

print(bubble_sort([4, 2, 1, 8, 7, 6]))
```


লক্ষ্য করুন যে যেহেতু পাইথন একটি ব্যাখ্যামূলক ভাষা তাই আমরা কমান্ডগুলি কার্যকর করতে এবং নির্দেশাবলী কার্যকর করতে 'পিডিবি' শেল ব্যবহার করতে পারি।
['ipdb'] (https://pypi.org/project/ipdb/) একটি উন্নত 'পিডিবি' যা ['IPython'] (https://ipython.org) আরইপিএল ট্যাব সমাপ্তি, সিনট্যাক্স হাইলাইটিং, আরও ভাল ট্রেসব্যাকস এবং আরও ভাল অন্তর্দৃষ্টি সক্ষম করে যখন 'পিডিবি' মডিউল হিসাবে একই ইন্টারফেস ধরে রাখে।

আরও নিম্ন স্তরের প্রোগ্রামিংয়ের জন্য আপনি সম্ভবত ['gdb'] (https://www.gnu.org/software/gdb/) (এবং এর জীবন পরিবর্তনের মান ['pwndbg'] (https://github.com/pwndbg/pwndbg)) এবং ['lldb'] (https://lldb.llvm.org/)
এগুলি সি-এর মতো ভাষা ডিবাগিংয়ের জন্য অপ্টিমাইজ করা হয়েছে তবে আপনাকে যে কোনও প্রক্রিয়া অনুসন্ধান করতে এবং এর বর্তমান মেশিন অবস্থা পেতে দেবেঃ রেজিস্টার, স্ট্যাক, প্রোগ্রাম কাউন্টার এবং সি।





## Specialized Tools

Even if what you are trying to debug is a black box binary there are tools that can help you with that.
Whenever programs need to perform actions that only the kernel can, they use [System Calls](https://en.wikipedia.org/wiki/System_call).
There are commands that let you trace the syscalls your program makes. In Linux there's [`strace`](https://www.man7.org/linux/man-pages/man1/strace.1.html) and macOS and BSD have [`dtrace`](http://dtrace.org/blogs/about/). `dtrace` can be tricky to use because it uses its own `D` language, but there is a wrapper called [`dtruss`](https://www.manpagez.com/man/1/dtruss/) that provides an interface more similar to `strace` (more details [here](https://8thlight.com/blog/colin-jones/2015/11/06/dtrace-even-better-than-strace-for-osx.html)).

Below are some examples of using `strace` or `dtruss` to show [`stat`](https://www.man7.org/linux/man-pages/man2/stat.2.html) syscall traces for an execution of `ls`. For a deeper dive into `strace`, [this article](https://blogs.oracle.com/linux/strace-the-sysadmins-microscope-v2) and [this zine](https://jvns.ca/strace-zine-unfolded.pdf) are good reads.

```bash
# On Linux
sudo strace -e lstat ls -l > /dev/null
# On macOS
sudo dtruss -t lstat64_extended ls -l > /dev/null
```

Under some circumstances, you may need to look at the network packets to figure out the issue in your program.
Tools like [`tcpdump`](https://www.man7.org/linux/man-pages/man1/tcpdump.1.html) and [Wireshark](https://www.wireshark.org/) are network packet analyzers that let you read the contents of network packets and filter them based on different criteria.

For web development, the Chrome/Firefox developer tools are quite handy. They feature a large number of tools, including:
- Source code - Inspect the HTML/CSS/JS source code of any website.
- Live HTML, CSS, JS modification - Change the website content, styles and behavior to test (you can see for yourself that website screenshots are not valid proofs).
- Javascript shell - Execute commands in the JS REPL.
- Network - Analyze the requests timeline.
- Storage - Look into the Cookies and local application storage.

## Static Analysis

For some issues you do not need to run any code.
For example, just by carefully looking at a piece of code you could realize that your loop variable is shadowing an already existing variable or function name; or that a program reads a variable before defining it.
Here is where [static analysis](https://en.wikipedia.org/wiki/Static_program_analysis) tools come into play.
Static analysis programs take source code as input and analyze it using coding rules to reason about its correctness.

In the following Python snippet there are several mistakes.
First, our loop variable `foo` shadows the previous definition of the function `foo`. We also wrote `baz` instead of `bar` in the last line, so the program will crash after completing the `sleep` call (which will take one minute).

```python
import time

def foo():
    return 42

for foo in range(5):
    print(foo)
bar = 1
bar *= 0.2
time.sleep(60)
print(baz)
```

Static analysis tools can identify these kinds of issues. When we run [`pyflakes`](https://pypi.org/project/pyflakes) on the code we get the errors related to both bugs. [`mypy`](http://mypy-lang.org/) is another tool that can detect type checking issues. Here, `mypy` will warn us that `bar` is initially an `int` and is then casted to a `float`.
Again, note that all these issues were detected without having to run the code.

```bash
$ pyflakes foobar.py
foobar.py:6: redefinition of unused 'foo' from line 3
foobar.py:11: undefined name 'baz'

$ mypy foobar.py
foobar.py:6: error: Incompatible types in assignment (expression has type "int", variable has type "Callable[[], Any]")
foobar.py:9: error: Incompatible types in assignment (expression has type "float", variable has type "int")
foobar.py:11: error: Name 'baz' is not defined
Found 3 errors in 1 file (checked 1 source file)
```

In the shell tools lecture we covered [`shellcheck`](https://www.shellcheck.net/), which is a similar tool for shell scripts.

Most editors and IDEs support displaying the output of these tools within the editor itself, highlighting the locations of warnings and errors.
This is often called **code linting** and it can also be used to display other types of issues such as stylistic violations or insecure constructs.

In vim, the plugins [`ale`](https://vimawesome.com/plugin/ale) or [`syntastic`](https://vimawesome.com/plugin/syntastic) will let you do that.
For Python, [`pylint`](https://github.com/PyCQA/pylint) and [`pep8`](https://pypi.org/project/pep8/) are examples of stylistic linters and [`bandit`](https://pypi.org/project/bandit/) is a tool designed to find common security issues.
For other languages people have compiled comprehensive lists of useful static analysis tools, such as [Awesome Static Analysis](https://github.com/mre/awesome-static-analysis) (you may want to take a look at the _Writing_ section) and for linters there is [Awesome Linters](https://github.com/caramelomartins/awesome-linters).

A complementary tool to stylistic linting are code formatters such as [`black`](https://github.com/psf/black) for Python, `gofmt` for Go, `rustfmt` for Rust or [`prettier`](https://prettier.io/) for JavaScript, HTML and CSS.
These tools autoformat your code so that it's consistent with common stylistic patterns for the given programming language.
Although you might be unwilling to give stylistic control about your code, standardizing code format will help other people read your code and will make you better at reading other people's (stylistically standardized) code.

# Profiling

Even if your code functionally behaves as you would expect, that might not be good enough if it takes all your CPU or memory in the process.
Algorithms classes often teach big _O_ notation but not how to find hot spots in your programs.
Since [premature optimization is the root of all evil](http://wiki.c2.com/?PrematureOptimization), you should learn about profilers and monitoring tools. They will help you understand which parts of your program are taking most of the time and/or resources so you can focus on optimizing those parts.

## Timing

Similarly to the debugging case, in many scenarios it can be enough to just print the time it took your code between two points.
Here is an example in Python using the [`time`](https://docs.python.org/3/library/time.html) module.

```python
import time, random
n = random.randint(1, 10) * 100

# Get current time
start = time.time()

# Do some work
print("Sleeping for {} ms".format(n))
time.sleep(n/1000)

# Compute time between start and now
print(time.time() - start)

# Output
# Sleeping for 500 ms
# 0.5713930130004883
```

However, wall clock time can be misleading since your computer might be running other processes at the same time or waiting for events to happen. It is common for tools to make a distinction between _Real_, _User_ and _Sys_ time. In general, _User_ + _Sys_ tells you how much time your process actually spent in the CPU (more detailed explanation [here](https://stackoverflow.com/questions/556405/what-do-real-user-and-sys-mean-in-the-output-of-time1)).

- _Real_ - Wall clock elapsed time from start to finish of the program, including the time taken by other processes and time taken while blocked (e.g. waiting for I/O or network)
- _User_ - Amount of time spent in the CPU running user code
- _Sys_ - Amount of time spent in the CPU running kernel code

For example, try running a command that performs an HTTP request and prefixing it with [`time`](https://www.man7.org/linux/man-pages/man1/time.1.html). Under a slow connection you might get an output like the one below. Here it took over 2 seconds for the request to complete but the process only took 15ms of CPU user time and 12ms of kernel CPU time.

```bash
$ time curl https://missing.csail.mit.edu &> /dev/null
real    0m2.561s
user    0m0.015s
sys     0m0.012s
```

## Profilers

### CPU

Most of the time when people refer to _profilers_ they actually mean _CPU profilers_,  which are the most common.
There are two main types of CPU profilers: _tracing_ and _sampling_ profilers.
Tracing profilers keep a record of every function call your program makes whereas sampling profilers probe your program periodically (commonly every millisecond) and record the program's stack.
They use these records to present aggregate statistics of what your program spent the most time doing.
[Here](https://jvns.ca/blog/2017/12/17/how-do-ruby---python-profilers-work-) is a good intro article if you want more detail on this topic.

Most programming languages have some sort of command line profiler that you can use to analyze your code.
They often integrate with full fledged IDEs but for this lecture we are going to focus on the command line tools themselves.

In Python we can use the `cProfile` module to profile time per function call. Here is a simple example that implements a rudimentary grep in Python:

```python
#!/usr/bin/env python

import sys, re

def grep(pattern, file):
    with open(file, 'r') as f:
        print(file)
        for i, line in enumerate(f.readlines()):
            pattern = re.compile(pattern)
            match = pattern.search(line)
            if match is not None:
                print("{}: {}".format(i, line), end="")

if __name__ == '__main__':
    times = int(sys.argv[1])
    pattern = sys.argv[2]
    for i in range(times):
        for file in sys.argv[3:]:
            grep(pattern, file)
```

We can profile this code using the following command. Analyzing the output we can see that IO is taking most of the time and that compiling the regex takes a fair amount of time as well. Since the regex only needs to be compiled once, we can factor it out of the for.

```
$ python -m cProfile -s tottime grep.py 1000 '^(import|\s*def)[^,]*$' *.py

[omitted program output]

 ncalls  tottime  percall  cumtime  percall filename:lineno(function)
     8000    0.266    0.000    0.292    0.000 {built-in method io.open}
     8000    0.153    0.000    0.894    0.000 grep.py:5(grep)
    17000    0.101    0.000    0.101    0.000 {built-in method builtins.print}
     8000    0.100    0.000    0.129    0.000 {method 'readlines' of '_io._IOBase' objects}
    93000    0.097    0.000    0.111    0.000 re.py:286(_compile)
    93000    0.069    0.000    0.069    0.000 {method 'search' of '_sre.SRE_Pattern' objects}
    93000    0.030    0.000    0.141    0.000 re.py:231(compile)
    17000    0.019    0.000    0.029    0.000 codecs.py:318(decode)
        1    0.017    0.017    0.911    0.911 grep.py:3(<module>)

[omitted lines]
```


A caveat of Python's `cProfile` profiler (and many profilers for that matter) is that they display time per function call. That can become unintuitive really fast, especially if you are using third party libraries in your code since internal function calls are also accounted for.
A more intuitive way of displaying profiling information is to include the time taken per line of code, which is what _line profilers_ do.

For instance, the following piece of Python code performs a request to the class website and parses the response to get all URLs in the page:

```python
#!/usr/bin/env python
import requests
from bs4 import BeautifulSoup

# This is a decorator that tells line_profiler
# that we want to analyze this function
@profile
def get_urls():
    response = requests.get('https://missing.csail.mit.edu')
    s = BeautifulSoup(response.content, 'lxml')
    urls = []
    for url in s.find_all('a'):
        urls.append(url['href'])

if __name__ == '__main__':
    get_urls()
```

If we used Python's `cProfile` profiler we'd get over 2500 lines of output, and even with sorting it'd be hard to understand where the time is being spent. A quick run with [`line_profiler`](https://github.com/pyutils/line_profiler) shows the time taken per line:

```bash
$ kernprof -l -v a.py
Wrote profile results to urls.py.lprof
Timer unit: 1e-06 s

Total time: 0.636188 s
File: a.py
Function: get_urls at line 5

Line #  Hits         Time  Per Hit   % Time  Line Contents
==============================================================
 5                                           @profile
 6                                           def get_urls():
 7         1     613909.0 613909.0     96.5      response = requests.get('https://missing.csail.mit.edu')
 8         1      21559.0  21559.0      3.4      s = BeautifulSoup(response.content, 'lxml')
 9         1          2.0      2.0      0.0      urls = []
10        25        685.0     27.4      0.1      for url in s.find_all('a'):
11        24         33.0      1.4      0.0          urls.append(url['href'])
```

### Memory

In languages like C or C++ memory leaks can cause your program to never release memory that it doesn't need anymore.
To help in the process of memory debugging you can use tools like [Valgrind](https://valgrind.org/) that will help you identify memory leaks.

In garbage collected languages like Python it is still useful to use a memory profiler because as long as you have pointers to objects in memory they won't be garbage collected.
Here's an example program and its associated output when running it with [memory-profiler](https://pypi.org/project/memory-profiler/) (note the decorator like in `line-profiler`).

```python
@profile
def my_func():
    a = [1] * (10 ** 6)
    b = [2] * (2 * 10 ** 7)
    del b
    return a

if __name__ == '__main__':
    my_func()
```

```bash
$ python -m memory_profiler example.py
Line #    Mem usage  Increment   Line Contents
==============================================
     3                           @profile
     4      5.97 MB    0.00 MB   def my_func():
     5     13.61 MB    7.64 MB       a = [1] * (10 ** 6)
     6    166.20 MB  152.59 MB       b = [2] * (2 * 10 ** 7)
     7     13.61 MB -152.59 MB       del b
     8     13.61 MB    0.00 MB       return a
```

### Event Profiling

As it was the case for `strace` for debugging, you might want to ignore the specifics of the code that you are running and treat it like a black box when profiling.
The [`perf`](https://www.man7.org/linux/man-pages/man1/perf.1.html) command abstracts CPU differences away and does not report time or memory, but instead it reports system events related to your programs.
For example, `perf` can easily report poor cache locality, high amounts of page faults or livelocks. Here is an overview of the command:

- `perf list` - List the events that can be traced with perf
- `perf stat COMMAND ARG1 ARG2` - Gets counts of different events related to a process or command
- `perf record COMMAND ARG1 ARG2` - Records the run of a command and saves the statistical data into a file called `perf.data`
- `perf report` - Formats and prints the data collected in `perf.data`


### Visualization

Profiler output for real world programs will contain large amounts of information because of the inherent complexity of software projects.
Humans are visual creatures and are quite terrible at reading large amounts of numbers and making sense of them.
Thus there are many tools for displaying profiler's output in an easier to parse way.

One common way to display CPU profiling information for sampling profilers is to use a [Flame Graph](http://www.brendangregg.com/flamegraphs.html), which will display a hierarchy of function calls across the Y axis and time taken proportional to the X axis. They are also interactive, letting you zoom into specific parts of the program and get their stack traces (try clicking in the image below).

[![FlameGraph](http://www.brendangregg.com/FlameGraphs/cpu-bash-flamegraph.svg)](http://www.brendangregg.com/FlameGraphs/cpu-bash-flamegraph.svg)

Call graphs or control flow graphs display the relationships between subroutines within a program by including functions as nodes and functions calls between them as directed edges. When coupled with profiling information such as the number of calls and time taken, call graphs can be quite useful for interpreting the flow of a program.
In Python you can use the [`pycallgraph`](https://pycallgraph.readthedocs.io/) library to generate them.

![Call Graph](https://upload.wikimedia.org/wikipedia/commons/2/2f/A_Call_Graph_generated_by_pycallgraph.png)


## Resource Monitoring

Sometimes, the first step towards analyzing the performance of your program is to understand what its actual resource consumption is.
Programs often run slowly when they are resource constrained, e.g. without enough memory or on a slow network connection.
There are a myriad of command line tools for probing and displaying different system resources like CPU usage, memory usage, network, disk usage and so on.

- **General Monitoring** - Probably the most popular is [`htop`](https://htop.dev/), which is an improved version of [`top`](https://www.man7.org/linux/man-pages/man1/top.1.html).
`htop` presents various statistics for the currently running processes on the system. `htop` has a myriad of options and keybinds, some useful ones  are: `<F6>` to sort processes, `t` to show tree hierarchy and `h` to toggle threads. 
See also [`glances`](https://nicolargo.github.io/glances/) for similar implementation with a great UI. For getting aggregate measures across all processes, [`dstat`](http://dag.wiee.rs/home-made/dstat/) is another nifty tool that computes real-time resource metrics for lots of different subsystems like I/O, networking, CPU utilization, context switches, &c.
- **I/O operations** - [`iotop`](https://www.man7.org/linux/man-pages/man8/iotop.8.html) displays live I/O usage information and is handy to check if a process is doing heavy I/O disk operations
- **Disk Usage** - [`df`](https://www.man7.org/linux/man-pages/man1/df.1.html) displays metrics per partitions and [`du`](http://man7.org/linux/man-pages/man1/du.1.html) displays **d**isk **u**sage per file for the current directory. In these tools the `-h` flag tells the program to print with **h**uman readable format.
A more interactive version of `du` is [`ncdu`](https://dev.yorhel.nl/ncdu) which lets you navigate folders and delete files and folders as you navigate.
- **Memory Usage** - [`free`](https://www.man7.org/linux/man-pages/man1/free.1.html) displays the total amount of free and used memory in the system. Memory is also displayed in tools like `htop`.
- **Open Files** - [`lsof`](https://www.man7.org/linux/man-pages/man8/lsof.8.html)  lists file information about files opened by processes. It can be quite useful for checking which process has opened a specific file.
- **Network Connections and Config** - [`ss`](https://www.man7.org/linux/man-pages/man8/ss.8.html) lets you monitor incoming and outgoing network packets statistics as well as interface statistics. A common use case of `ss` is figuring out what process is using a given port in a machine. For displaying routing, network devices and interfaces you can use [`ip`](http://man7.org/linux/man-pages/man8/ip.8.html). Note that `netstat` and `ifconfig` have been deprecated in favor of the former tools respectively.
- **Network Usage** -  [`nethogs`](https://github.com/raboof/nethogs) and [`iftop`](http://www.ex-parrot.com/pdw/iftop/) are good interactive CLI tools for monitoring network usage.

If you want to test these tools you can also artificially impose loads on the machine using the [`stress`](https://linux.die.net/man/1/stress) command.


### Specialized tools

Sometimes, black box benchmarking is all you need to determine what software to use.
Tools like [`hyperfine`](https://github.com/sharkdp/hyperfine) let you quickly benchmark command line programs.
For instance, in the shell tools and scripting lecture we recommended `fd` over `find`. We can use `hyperfine` to compare them in tasks we run often.
E.g. in the example below `fd` was 20x faster than `find` in my machine.

```bash
$ hyperfine --warmup 3 'fd -e jpg' 'find . -iname "*.jpg"'
Benchmark #1: fd -e jpg
  Time (mean ± σ):      51.4 ms ±   2.9 ms    [User: 121.0 ms, System: 160.5 ms]
  Range (min … max):    44.2 ms …  60.1 ms    56 runs

Benchmark #2: find . -iname "*.jpg"
  Time (mean ± σ):      1.126 s ±  0.101 s    [User: 141.1 ms, System: 956.1 ms]
  Range (min … max):    0.975 s …  1.287 s    10 runs

Summary
  'fd -e jpg' ran
   21.89 ± 2.33 times faster than 'find . -iname "*.jpg"'
```

As it was the case for debugging, browsers also come with a fantastic set of tools for profiling webpage loading, letting you figure out where time is being spent (loading, rendering, scripting, &c).
More info for [Firefox](https://profiler.firefox.com/docs/) and [Chrome](https://developers.google.com/web/tools/chrome-devtools/rendering-tools).

# Exercises

## Debugging
1. Use `journalctl` on Linux or `log show` on macOS to get the super user accesses and commands in the last day.
If there aren't any you can execute some harmless commands such as `sudo ls` and check again.

1. Do [this](https://github.com/spiside/pdb-tutorial) hands on `pdb` tutorial to familiarize yourself with the commands. For a more in depth tutorial read [this](https://realpython.com/python-debugging-pdb).

1. Install [`shellcheck`](https://www.shellcheck.net/) and try checking the following script. What is wrong with the code? Fix it. Install a linter plugin in your editor so you can get your warnings automatically.

   ```bash
   #!/bin/sh
   ## Example: a typical script with several problems
   for f in $(ls *.m3u)
   do
     grep -qi hq.*mp3 $f \
       && echo -e 'Playlist $f contains a HQ file in mp3 format'
   done
   ```

1. (Advanced) Read about [reversible debugging](https://undo.io/resources/reverse-debugging-whitepaper/) and get a simple example working using [`rr`](https://rr-project.org/) or [`RevPDB`](https://morepypy.blogspot.com/2016/07/reverse-debugging-for-python.html).
## Profiling

1. [Here](/static/files/sorts.py) are some sorting algorithm implementations. Use [`cProfile`](https://docs.python.org/3/library/profile.html) and [`line_profiler`](https://github.com/pyutils/line_profiler) to compare the runtime of insertion sort and quicksort. What is the bottleneck of each algorithm? Use then `memory_profiler` to check the memory consumption, why is insertion sort better? Check now the inplace version of quicksort. Challenge: Use `perf` to look at the cycle counts and cache hits and misses of each algorithm.

1. Here's some (arguably convoluted) Python code for computing Fibonacci numbers using a function for each number.

   ```python
   #!/usr/bin/env python
   def fib0(): return 0

   def fib1(): return 1

   s = """def fib{}(): return fib{}() + fib{}()"""

   if __name__ == '__main__':

       for n in range(2, 10):
           exec(s.format(n, n-1, n-2))
       # from functools import lru_cache
       # for n in range(10):
       #     exec("fib{} = lru_cache(1)(fib{})".format(n, n))
       print(eval("fib9()"))
   ```

   Put the code into a file and make it executable. Install prerequisites: [`pycallgraph`](https://pycallgraph.readthedocs.io/) and [`graphviz`](http://graphviz.org/). (If you can run `dot`, you already have GraphViz.) Run the code as is with `pycallgraph graphviz -- ./fib.py` and check the `pycallgraph.png` file. How many times is `fib0` called?. We can do better than that by memoizing the functions. Uncomment the commented lines and regenerate the images. How many times are we calling each `fibN` function now?

1. A common issue is that a port you want to listen on is already taken by another process. Let's learn how to discover that process pid. First execute `python -m http.server 4444` to start a minimal web server listening on port `4444`. On a separate terminal run `lsof | grep LISTEN` to print all listening processes and ports. Find that process pid and terminate it by running `kill <PID>`.

1. Limiting a process's resources can be another handy tool in your toolbox.
Try running `stress -c 3` and visualize the CPU consumption with `htop`. Now, execute `taskset --cpu-list 0,2 stress -c 3` and visualize it. Is `stress` taking three CPUs? Why not? Read [`man taskset`](https://www.man7.org/linux/man-pages/man1/taskset.1.html).
Challenge: achieve the same using [`cgroups`](https://www.man7.org/linux/man-pages/man7/cgroups.7.html). Try limiting the memory consumption of `stress -m`.

1. (Advanced) The command `curl ipinfo.io` performs a HTTP request and fetches information about your public IP. Open [Wireshark](https://www.wireshark.org/) and try to sniff the request and reply packets that `curl` sent and received. (Hint: Use the `http` filter to just watch HTTP packets).

