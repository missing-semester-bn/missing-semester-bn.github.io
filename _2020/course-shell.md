---
layout: lecture
title: "কোর্স ওভারভিউ  + the shell"
date: 2020-01-13
ready: true
video:
  aspect: 56.25
  id: Z56Jmr9Z34Q
---

# মোটিভেশন

Computer scientist হিসেবে আমরা জানি যে কম্পিউটার খুবই দক্ষ repetitive
কাজে সাহায্য করতে।  কিন্তু অনেক সময় আমরা ভুলে যাই যে ইটা যতটা আমাদের computer
_ব্যাবহারের_ জন্য প্রযোজ্য ততটা ইটা প্রযোজ্য কম্পিউটেশন এর উপর যেটা আমরা
আমাদের প্রোগ্রাম দ্বারা করতে চাই।

আমাদের কাছে অনেক tools উপলব্ধ আছে যেটা আমাদের বেশি productive করে আর বেশি জটিল problem সমাধান করার জন্য সাহায্য করে যখন আমরা যেকোনো computer সংক্রান্ত problem এর উপর কাজ করি। 

তবুও আমাদের মধ্যে অনেকেই এই tools গুলোর মধ্যে খুব অল্প পরিমানের tools ব্যবহার করি। 

আমরা যতটা জানি তা শুধু আমাদের কোনোরকমে প্রয়োজন মেটায় আর যখন আমরা আটকে যাই তখন আমরা অন্ধর মতো internet
থেকে command copy-paste করি। 
 

এই ক্লাস তা হচ্ছে ইটা নিয়েই কথা বলার এক প্রচেষ্টা। 

আমরা শেখাতে চাই কিভাবে যে টুলস গুলো তোমরা জানো  সবচেয়ে ভালো ভাবে ব্যবহার করতে হয় ,
আমরা দেখাব নতুন টুলস, তোমার টুল বাক্স  তে অ্যাড করার জন্য, এবং আশাকরি তোমার মধ্যে একটা এক্সসাইটমেন্ট দেওয়ার আরো টুলস এক্সপ্লোর করার জন্য নিজের থেকে আর সম্ভবত নিজে বানাবে। এটাই আমরা মনে করি মিসিং সেমেস্ত্র অধিকাংশ কম্পিউটার সাইন্স পাঠ্যক্রম থেকে। 

# Class structure

এই ক্লাস এর মধ্যে ১১ তা  ১-ঘন্টার  lecture রয়েছে , প্রত্যেকটি একটি নির্দিষ্ট [বিষয়ের উপর](/2020/।  
lecture গুলো স্বাধীন,
যদিও সেমিস্টার চলাকালীন আমরা ধরে নেব যে আপনি 
আগের লেকচারের বিষয়বস্তু সম্বন্দে পরিচিত। আমাদের লেকচার নোট আছে
অনলাইনে, কিন্তু ক্লাসে অনেক কন্টেন্ট কভার করা হবে (ডেমো হিসেবে ) যা নোটে নাও থাকতে পারে। আমরা lecture  রেকর্ডিং করবো  এবং অনলাইনে রেকর্ডিং পোস্ট করা হবে।

আমরা মাত্র 11 1-ঘন্টা জুড়ে অনেক কিছু কভার করার চেষ্টা করছি, তাই বক্তৃতা মোটামুটি ঘন হয়. আপনাকে কিছু সময় দেওয়ার জন্য
আপনার নিজস্ব গতিতে বিষয়বস্তুর সাথে পরিচিত হন, প্রতিটি বক্তৃতায় একটি অন্তর্ভুক্ত থাকে
ব্যায়ামের সেট যা আপনাকে বক্তৃতার মূল পয়েন্টগুলির মাধ্যমে গাইড করে। পরে
প্রতিটি বক্তৃতা, আমরা অফিসের সময় হোস্ট করছি যেখানে আমরা উপস্থিত থাকব
আপনার যে কোনো প্রশ্নের উত্তর দিতে সাহায্য করুন। আপনি যদি ক্লাসে উপস্থিত হন
অনলাইন, আপনি আমাদের প্রশ্ন পাঠাতে পারেন
[missing-semester@mit.edu](mailto:missing-semester@mit.edu)।

কম সময় থাকার জন্য আমরা সমস্ত টুলস গুলো সমান ডিটেলস এ কভার করতে পারবো না যেটা 
একটা full-স্কেল ক্লাস করতে পারবে।  যেখানে সম্ভব আমরা তোমাকে আরো রিসোর্স দেওয়ার চেষ্টা
করবো কোনো একটা টুলস বা টপিক কে আরো ভালো করে জানতে, কিন্তু যদি কিছু বিশেষভাবে আপনার অভিনব আঘাত করে, আমাদের কাছে পৌঁছাতে এবং পয়েন্টার চাইতে দ্বিধা নেই! 

# Topic 1: The Shell

## shell  কি জিনিস?

কম্পিউটার আজকাল তাদের দেওয়ার জন্য বিভিন্ন ইন্টারফেস রয়েছে
আদেশ; কল্পনাপ্রসূত গ্রাফিকাল ইউজার ইন্টারফেস, ভয়েস ইন্টারফেস এবং
এমনকি AR/VR সব জায়গায় আছে। এগুলি 80% ব্যবহারের ক্ষেত্রে দুর্দান্ত, তবে
তারা আপনাকে যা করতে দেয় তাতে তারা প্রায়শই মৌলিকভাবে সীমাবদ্ধ থাকে —
আপনি সেখানে নেই এমন একটি বোতাম টিপতে পারবেন না বা ভয়েস কমান্ড দিতে পারবেন না
প্রোগ্রাম করা হয় নি। টুলস আপনার সম্পূর্ণ সুবিধা নিতে
কম্পিউটার প্রদান করে, আমাদের পুরানো স্কুলে যেতে হবে এবং পাঠ্যতে নেমে যেতে হবে
ইন্টারফেস: শেল।

প্রায় সব প্ল্যাটফর্মে আপনি আপনার হাত পেতে পারেন একটি শেল একটি ফর্ম বা
আরেকটি, এবং তাদের অনেকের কাছে আপনার থেকে বেছে নেওয়ার জন্য বেশ কয়েকটি শেল রয়েছে।
যদিও সেগুলি বিশদ বিবরণে পরিবর্তিত হতে পারে, তবে তাদের মূলে সেগুলি মোটামুটি
একই: তারা আপনাকে প্রোগ্রাম চালানোর অনুমতি দেয়, তাদের ইনপুট দেয় এবং পরিদর্শন করে
একটি আধা-গঠিত উপায়ে তাদের আউটপুট।

এই বক্তৃতায়, আমরা Bourne Again SHell বা "bash" এর উপর আলোকপাত করব
সংক্ষিপ্ত এটি সবচেয়ে ব্যাপকভাবে ব্যবহৃত শেলগুলির মধ্যে একটি এবং এর সিনট্যাক্স হল
আপনি অন্যান্য অনেক শেল দেখতে পাবেন কি অনুরূপ. একটি শেল খুলতে
_prompt_ (যেখানে আপনি কমান্ড টাইপ করতে পারেন), আপনার প্রথমে একটি _terminal_ প্রয়োজন।
আপনার ডিভাইস সম্ভবত একটি ইনস্টল সহ পাঠানো হয়েছে, অথবা আপনি একটি ইনস্টল করতে পারেন
মোটামুটি সহজে।

## শেল ব্যবহার করা

যখন আপনি আপনার টার্মিনাল চালু করেন, আপনি একটি _prompt_ দেখতে পাবেন যা প্রায়শই দেখায়
এই মত একটু:

```console
missing:~$ 
```

এটি শেলের প্রধান পাঠ্য ইন্টারফেস। এটা আপনাকে বলে যে আপনি
মেশিনে আছে `missing` এবং আপনার "current working directory",
অথবা আপনি বর্তমানে যেখানে আছেন, তা হল `~` ("home" এর জন্য সংক্ষিপ্ত)। `$` আপনাকে বলে
যে আপনি root ব্যবহারকারী নন (পরে আরও বেশি)। এই প্রম্পট আপনি
একটি _command_ টাইপ করতে পারে, যা শেল দ্বারা ব্যাখ্যা করা হবে। দ্য
সবচেয়ে মৌলিক কমান্ড হল একটি প্রোগ্রাম চালানো:

```console
missing:~$ date
Fri 10 Jan 2020 11:49:31 AM EST
missing:~$ 
```

এখানে, আমরা 'date' প্রোগ্রামটি কার্যকর করেছি, যা (সম্ভবত আশ্চর্যজনকভাবে)
বর্তমান তারিখ এবং সময় প্রিন্ট করে। শেলটি তখন আমাদের কাছে অন্যটির জন্য জিজ্ঞাসা করে
কার্যকর করার আদেশ। আমরা _arguments_ দিয়ে একটি কমান্ডও চালাতে পারি:

```console
missing:~$ echo hello
hello
```

এই ক্ষেত্রে, আমরা শেলকে বলেছিলাম প্রোগ্রামটি  'echo' এর সাথে চালাতে
যুক্তি `hello`। 'echo' প্রোগ্রামটি কেবল তার আর্গুমেন্টগুলি প্রিন্ট করে।
শেল হোয়াইটস্পেস দ্বারা বিভক্ত করে কমান্ডটি পার্স করে এবং তারপরে
প্রথম শব্দ দ্বারা নির্দেশিত প্রোগ্রাম চালায়, প্রতিটি পরবর্তী সরবরাহ করে
একটি যুক্তি হিসাবে শব্দ যে প্রোগ্রাম অ্যাক্সেস করতে পারে. দিতে চাইলে দিতে পারেন
একটি আর্গুমেন্ট যাতে স্পেস বা অন্যান্য বিশেষ অক্ষর থাকে (যেমন, ক
"My Photos" নামের ডিরেক্টরি), আপনি হয় `'` দিয়ে আর্গুমেন্ট উদ্ধৃত করতে পারেন
বা `"` (`"My Photos"`), অথবা `\` দিয়ে শুধু প্রাসঙ্গিক অক্ষরগুলি এড়িয়ে যান
('My\ Photos')।

কিন্তু কিভাবে শেল জানে কিভাবে `date` বা `echo` প্রোগ্রাম খুঁজে বের করতে হয়?
ঠিক আছে, শেল হল একটি প্রোগ্রামিং পরিবেশ, যেমন পাইথন বা রুবি,
এবং তাই এটির ভেরিয়েবল, কন্ডিশনাল, লুপ এবং ফাংশন রয়েছে (পরবর্তী
বক্তৃতা!) আপনি যখন আপনার শেলে কমান্ড চালান, আপনি সত্যিই একটি লিখছেন
কোডের একটি ছোট বিট যা আপনার শেল ব্যাখ্যা করে। যদি শেল বলা হয়
একটি কমান্ড চালান যা তার প্রোগ্রামিং কীওয়ার্ডগুলির একটির সাথে মেলে না, এটি
একটি _environment variable_ এর সাথে পরামর্শ করে যাকে তালিকা দেয় `$PATH`
ডিরেক্টরীতে শেলকে প্রোগ্রাম অনুসন্ধান করা উচিত যখন এটি একটি দেওয়া হয়
আদেশ:

```console
missing:~$ echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
missing:~$ which echo
/bin/echo
missing:~$ /bin/echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

যখন আমরা `echo` কমান্ড চালাই, শেল দেখতে পায় যে এটি কার্যকর করা উচিত
প্রোগ্রাম `echo`, এবং তারপর `:`-এর পৃথক তালিকার মাধ্যমে অনুসন্ধান করে
সেই নামের একটি ফাইলের জন্য `$PATH`-এ ডিরেক্টরি। যখন এটি এটি খুঁজে পায়, এটি
এটি চালায় (অনুমান করা হচ্ছে ফাইলটি _executable_; পরে আরও বেশি)। আমরা পারি
ব্যবহার করে একটি প্রদত্ত প্রোগ্রাম নামের জন্য কোন ফাইলটি নির্বাহ করা হয় তা খুঁজে বের করুন
`which` প্রোগ্রাম। আমরা প্রদানের মাধ্যমে `$PATH` সম্পূর্ণভাবে বাইপাস করতে পারি
_path_ ফাইলটিতে আমরা চালাতে চাই।

## শেলে নেভিগেট করা

শেলের একটি পথ হল ডিরেক্টরিগুলির একটি সীমাবদ্ধ তালিকা; `/` দ্বারা বিভক্ত
Linux এবং macOS এ এবং `\` উইন্ডোজে। Linux এবং macOS-এ, পাথ `/`
এটি ফাইল সিস্টেমের "রুট", যার অধীনে সমস্ত ডিরেক্টরি এবং ফাইল
মিথ্যা, যেখানে উইন্ডোজে প্রতিটি ডিস্ক পার্টিশনের জন্য একটি রুট রয়েছে (যেমন,
`C:\`)। আমরা সাধারণত ধরে নেব যে আপনি একটি লিনাক্স ফাইল সিস্টেম ব্যবহার করছেন
এই ক্লাসে যে পথটি `/` দিয়ে শুরু হয় তাকে বলা হয় _পরম_পথ।
অন্য কোন পথ একটি _আত্মীয়_পথ। আপেক্ষিক পাথ আপেক্ষিক
বর্তমান কাজের ডিরেক্টরি, যা আমরা `pwd` কমান্ড দিয়ে দেখতে পারি এবং
'cd' কমান্ড দিয়ে পরিবর্তন করুন। একটি পথে, `.` কারেন্টকে বোঝায়
ডিরেক্টরি, এবং `..` এর মূল ডিরেক্টরিতে:

```console
missing:~$ pwd
/home/missing
missing:~$ cd /home
missing:/home$ pwd
/home
missing:/home$ cd ..
missing:/$ pwd
/
missing:/$ cd ./home
missing:/home$ pwd
/home
missing:/home$ cd missing
missing:~$ pwd
/home/missing
missing:~$ ../../bin/echo hello
hello
```

লক্ষ্য করুন যে আমাদের শেল প্রম্পট আমাদের বর্তমান কী সম্পর্কে আমাদের অবহিত করেছে
কাজের ডিরেক্টরি ছিল। আপনি সব দেখানোর জন্য আপনার প্রম্পট কনফিগার করতে পারেন
বিভিন্ন ধরণের দরকারী তথ্য, যা আমরা পরবর্তী বক্তৃতায় কভার করব।

সাধারণভাবে, যখন আমরা একটি প্রোগ্রাম চালাই, তখন এটি কারেন্টে কাজ করবে
ডিরেক্টরি যদি না আমরা অন্যথায় বলি। উদাহরণস্বরূপ, এটি সাধারণত হবে
সেখানে ফাইল অনুসন্ধান করুন, এবং প্রয়োজন হলে সেখানে নতুন ফাইল তৈরি করুন।

একটি প্রদত্ত ডিরেক্টরিতে কী থাকে তা দেখতে, আমরা `ls` কমান্ড ব্যবহার করি:

```console
missing:~$ ls
missing:~$ cd ..
missing:/home$ ls
missing
missing:/home$ cd ..
missing:/$ ls
bin
boot
dev
etc
home
...
```

একটি ডিরেক্টরিকে তার প্রথম যুক্তি হিসাবে দেওয়া না হলে, `ls` মুদ্রণ করবে
বর্তমান ডিরেক্টরির বিষয়বস্তু। বেশিরভাগ কমান্ড পতাকা গ্রহণ করে এবং
বিকল্পগুলি (মান সহ পতাকা) যেগুলি পরিবর্তন করতে `-` দিয়ে শুরু হয়
আচরণ সাধারণত, `-h` বা `--help` পতাকা সহ একটি প্রোগ্রাম চালানো
কিছু হেল্প টেক্সট প্রিন্ট করবে যা আপনাকে বলে যে কোন পতাকা
এবং বিকল্প উপলব্ধ। উদাহরণস্বরূপ, `ls --help` আমাদের বলে:

```
  -l                         use a long listing format
```

```console
missing:~$ ls -l /home
drwxr-xr-x 1 missing  users  4096 Jun 15  2019 missing
```

এটি আমাদের প্রতিটি ফাইল বা ডিরেক্টরি সম্পর্কে আরও তথ্য দেয়
বর্তমান প্রথমত, লাইনের শুরুতে 'd' আমাদেরকে বলে
`missing` একটি ডিরেক্টরি। তারপর তিনটি অক্ষরের তিনটি গ্রুপ অনুসরণ করুন
(`rwx`)। এই ফাইলের মালিক কি অনুমতি নির্দেশ করে
(`missing'), মালিকানার গোষ্ঠী (`user), এবং যথাক্রমে অন্য সবাই
প্রাসঙ্গিক আইটেম আছে. A `-` নির্দেশ করে যে প্রদত্ত প্রধান তা করে
প্রদত্ত অনুমতি নেই। উপরে, শুধুমাত্র মালিক অনুমোদিত
`missing` ডিরেক্টরিটি পরিবর্তন (`w`) করুন (অর্থাৎ, এতে ফাইল যোগ করুন/সরান)। প্রতি
একটি ডিরেক্টরি লিখুন, একজন ব্যবহারকারীর অবশ্যই "অনুসন্ধান" থাকতে হবে ("চালনা" দ্বারা উপস্থাপিত:
সেই ডিরেক্টরিতে `x`) অনুমতি (এবং এর পিতামাতা)। তার তালিকা
বিষয়বস্তু, একজন ব্যবহারকারীর অবশ্যই সেই ডিরেক্টরিতে পড়ার (`r`) অনুমতি থাকতে হবে। জন্য
ফাইল, অনুমতি আপনি আশা করা হয় হিসাবে হয়. লক্ষ্য করুন যে প্রায় সব
`/bin` এর ফাইলে শেষ গ্রুপের জন্য `x` অনুমতি সেট করা আছে,
"অন্য সবাই", যাতে যে কেউ সেই প্রোগ্রামগুলি চালাতে পারে।


এই মুহুর্তে জানার জন্য আরও কিছু সহজ প্রোগ্রাম হল `mv` ( থেকে
একটি ফাইলের নাম পরিবর্তন/সরান), `cp` (একটি ফাইল অনুলিপি করতে), এবং `mkdir` (একটি নতুন করতে
ডিরেক্টরি)।

আপনি যদি কখনও একটি প্রোগ্রামের আর্গুমেন্ট, ইনপুট সম্পর্কে _আরো_ তথ্য চান,
আউটপুট, বা এটি সাধারণভাবে কীভাবে কাজ করে, `ম্যান` প্রোগ্রামটি চেষ্টা করে দেখুন। এটা
একটি যুক্তি হিসাবে একটি প্রোগ্রামের নাম নেয়, এবং আপনাকে এর _ম্যানুয়াল দেখায়
পৃষ্ঠা_ প্রস্থান করতে `q` টিপুন।

```console
missing:~$ man ls
```

## Connecting programs

In the shell, programs have two primary "streams" associated with them:
their input stream and their output stream. When the program tries to
read input, it reads from the input stream, and when it prints
something, it prints to its output stream. Normally, a program's input
and output are both your terminal. That is, your keyboard as input and
your screen as output. However, we can also rewire those streams!

The simplest form of redirection is `< file` and `> file`. These let you
rewire the input and output streams of a program to a file respectively:

```console
missing:~$ echo hello > hello.txt
missing:~$ cat hello.txt
hello
missing:~$ cat < hello.txt
hello
missing:~$ cat < hello.txt > hello2.txt
missing:~$ cat hello2.txt
hello
```

Demonstrated in the example above, `cat` is a program that con`cat`enates
files. When given file names as arguments, it prints the contents of each of
the files in sequence to its output stream. But when `cat` is not given any
arguments, it prints contents from its input stream to its output stream (like
in the third example above).

You can also use `>>` to append to a file. Where this kind of
input/output redirection really shines is in the use of _pipes_. The `|`
operator lets you "chain" programs such that the output of one is the
input of another:

```console
missing:~$ ls -l / | tail -n1
drwxr-xr-x 1 root  root  4096 Jun 20  2019 var
missing:~$ curl --head --silent google.com | grep --ignore-case content-length | cut --delimiter=' ' -f2
219
```

We will go into a lot more detail about how to take advantage of pipes
in the lecture on data wrangling.

## A versatile and powerful tool

On most Unix-like systems, one user is special: the "root" user. You may
have seen it in the file listings above. The root user is above (almost)
all access restrictions, and can create, read, update, and delete any
file in the system. You will not usually log into your system as the
root user though, since it's too easy to accidentally break something.
Instead, you will be using the `sudo` command. As its name implies, it
lets you "do" something "as su" (short for "super user", or "root").
When you get permission denied errors, it is usually because you need to
do something as root. Though make sure you first double-check that you
really wanted to do it that way!

One thing you need to be root in order to do is writing to the `sysfs` file
system mounted under `/sys`. `sysfs` exposes a number of kernel parameters as
files, so that you can easily reconfigure the kernel on the fly without
specialized tools. **Note that sysfs does not exist on Windows or macOS.**

For example, the brightness of your laptop's screen is exposed through a file
called `brightness` under

```
/sys/class/backlight
```

By writing a value into that file, we can change the screen brightness.
Your first instinct might be to do something like:

```console
$ sudo find -L /sys/class/backlight -maxdepth 2 -name '*brightness*'
/sys/class/backlight/thinkpad_screen/brightness
$ cd /sys/class/backlight/thinkpad_screen
$ sudo echo 3 > brightness
An error occurred while redirecting file 'brightness'
open: Permission denied
```

This error may come as a surprise. After all, we ran the command with
`sudo`! This is an important thing to know about the shell. Operations
like `|`, `>`, and `<` are done _by the shell_, not by the individual
program. `echo` and friends do not "know" about `|`. They just read from
their input and write to their output, whatever it may be. In the case
above, the _shell_ (which is authenticated just as your user) tries to
open the brightness file for writing, before setting that as `sudo
echo`'s output, but is prevented from doing so since the shell does not
run as root. Using this knowledge, we can work around this:

```console
$ echo 3 | sudo tee brightness
```

Since the `tee` program is the one to open the `/sys` file for writing,
and _it_ is running as `root`, the permissions all work out. You can
control all sorts of fun and useful things through `/sys`, such as the
state of various system LEDs (your path might be different):

```console
$ echo 1 | sudo tee /sys/class/leds/input6::scrolllock/brightness
```

# Next steps

At this point you know your way around a shell enough to accomplish
basic tasks. You should be able to navigate around to find files of
interest and use the basic functionality of most programs. In the next
lecture, we will talk about how to perform and automate more complex
tasks using the shell and the many handy command-line programs out
there.

# Exercises

All classes in this course are accompanied by a series of exercises. Some give
you a specific task to do, while others are open-ended, like "try using X and Y
programs". We highly encourage you to try them out.

We have not written solutions for the exercises. If you are stuck on anything
in particular, feel free to send us an email describing what you've tried so
far, and we will try to help you out.

 1. For this course, you need to be using a Unix shell like Bash or ZSH. If you
    are on Linux or macOS, you don't have to do anything special. If you are on
    Windows, you need to make sure you are not running cmd.exe or PowerShell;
    you can use [Windows Subsystem for
    Linux](https://docs.microsoft.com/en-us/windows/wsl/) or a Linux virtual
    machine to use Unix-style command-line tools. To make sure you're running
    an appropriate shell, you can try the command `echo $SHELL`. If it says
    something like `/bin/bash` or `/usr/bin/zsh`, that means you're running the
    right program.
 1. Create a new directory called `missing` under `/tmp`.
 1. Look up the `touch` program. The `man` program is your friend.
 1. Use `touch` to create a new file called `semester` in `missing`.
 1. Write the following into that file, one line at a time:
    ```
    #!/bin/sh
    curl --head --silent https://missing.csail.mit.edu
    ```
    The first line might be tricky to get working. It's helpful to know that
    `#` starts a comment in Bash, and `!` has a special meaning even within
    double-quoted (`"`) strings. Bash treats single-quoted strings (`'`)
    differently: they will do the trick in this case. See the Bash
    [quoting](https://www.gnu.org/software/bash/manual/html_node/Quoting.html)
    manual page for more information.
 1. Try to execute the file, i.e. type the path to the script (`./semester`)
    into your shell and press enter. Understand why it doesn't work by
    consulting the output of `ls` (hint: look at the permission bits of the
    file).
 1. Run the command by explicitly starting the `sh` interpreter, and giving it
    the file `semester` as the first argument, i.e. `sh semester`. Why does
    this work, while `./semester` didn't?
 1. Look up the `chmod` program (e.g. use `man chmod`).
 1. Use `chmod` to make it possible to run the command `./semester` rather than
    having to type `sh semester`. How does your shell know that the file is
    supposed to be interpreted using `sh`? See this page on the
    [shebang](https://en.wikipedia.org/wiki/Shebang_(Unix)) line for more
    information.
 1. Use `|` and `>` to write the "last modified" date output by
    `semester` into a file called `last-modified.txt` in your home
    directory.
 1. Write a command that reads out your laptop battery's power level or your
    desktop machine's CPU temperature from `/sys`. Note: if you're a macOS
    user, your OS doesn't have sysfs, so you can skip this exercise.

