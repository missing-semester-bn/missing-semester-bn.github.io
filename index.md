---
layout: page
title: আপনার CS education এর missing  semester।   
nositetitle: true
---

Classes  আপনাকে CS  এর advanced  topic  এর সব কিছু শেখায়, operating systems থেকে শুরু করে machine learning  পর্যন্ত কিন্তু একটা খুব গুরুত্বওপূর্ণ subject  আছে যেটা খুব এ কম পোড়ানো হয় এবং ইটা student  দেড় উপর ছেড়ে দেওয়া হয় শেখার জন্য: tools  কিভাবে দক্ষতার সাথে use  করা হয়। আমরা আপনা কে শেখাবো কিভাবে command-line  এ পারদর্শী হইয়া যাই, কিভাবে একটা powerful  text-editor  use  করতে হয় , কিভাবে version  control  system  এর সুন্দর features  গুলো use  করতে হয় এবং আরো কিছু।

ছাত্ররা ১০০র মতো ঘন্টা এই টুলস গুলো use  করে তাদের শিক্ষার সময় (আর হাজার এর মতো তাদের career  এ)। 
সুতরাং এটার মধ্যে sense  আছে যে এই অভিজ্ঞতা কে আমাদের 
 fluid  আর frictionless  করে উচিত যতটা সম্ভব।
এই tools  গুলি তে দক্ষ হলে আপনি কম সময় লাগাবেন ভেবে উঠতে যে কিভাবে আপনি আপনার ইচ্ছা মতো এই টুলস গুলো কে ব্যবহার করবেন, আর ইটা আপনাকে problem  solve  করতে সাহায্য করতে যে গুলো মনে হতো খুব কঠিন।  


পড়ুন [class  এর পিছনের motivation](/about/).

{% comment %}
# Registration

Sign up করুন  IAP 2020 class  এর জন্য  এই [registration form](https://forms.gle/TD1KnwCSV52qexVt9) form  fill-up  করে।  
{% endcomment %}

# Schedule

{% comment %}
**Lecture**: 35-225, 2pm--3pm<br>
**Office hours**: 32-G9 lounge, 3pm--4pm (every day, right after lecture)
{% endcomment %}

<ul>
{% assign lectures = site['2020'] | sort: 'date' %}
{% for lecture in lectures %}
    {% if lecture.phony != true %}
        <li>
        <strong>{{ lecture.date | date: '%-m/%d/%y' }}</strong>:
        {% if lecture.ready %}
            <a href="{{ lecture.url }}">{{ lecture.title }}</a>
        {% else %}
            {{ lecture.title }} {% if lecture.noclass %}[no class]{% endif %}
        {% endif %}
        </li>
    {% endif %}
{% endfor %}
</ul>

Video recordings  [YouTube  এ ](https://www.youtube.com/playlist?list=PLyzOVJj3bHQuloKGG59rS43e29ro7I57J) available আছে। 

# About the class

**Staff**: এই class  পোড়ানো হয়  [Anish](https://www.anishathalye.com/), [Jon](https://thesquareplanet.com/), and [Jose](http://josejg.com/). দ্বারা <br>
**Questions**: Email করুন  [missing-semester@mit.edu](mailto:missing-semester@mit.edu).

# Beyond MIT

আমরা এই class  MIT  এর বাইরে share  করেছি এই আসা তে যে বাকিরা এই resource  থেকে সুবিধা পাবে।  post  এবং discussion  আপনি এখানে খুঁজে পাবেন 

 - [Hacker News](https://news.ycombinator.com/item?id=22226380)
 - [Lobsters](https://lobste.rs/s/ti1k98/missing_semester_your_cs_education_mit)
 - [/r/learnprogramming](https://www.reddit.com/r/learnprogramming/comments/eyagda/the_missing_semester_of_your_cs_education_mit/)
 - [/r/programming](https://www.reddit.com/r/programming/comments/eyagcd/the_missing_semester_of_your_cs_education_mit/)
 - [Twitter](https://twitter.com/jonhoo/status/1224383452591509507)
 - [YouTube](https://www.youtube.com/playlist?list=PLyzOVJj3bHQuloKGG59rS43e29ro7I57J)

{% comment %}
Some more URLs:

- https://news.ycombinator.com/item?id=27154577
- https://news.ycombinator.com/item?id=34934216
- https://www.reddit.com/r/learnprogramming/comments/nca1v3/mit_the_missing_semester_of_your_cs_education/
- https://www.reddit.com/r/compsci/comments/eyywv8/the_missing_semester_of_your_cs_education_from_mit/
- https://www.reddit.com/r/programming/comments/io7nq3/the_missing_semester_of_your_cs_education_mit/
- https://twitter.com/MIT_CSAIL/status/1349766980413263873
- https://twitter.com/MIT_CSAIL/status/1481676163491659780
- https://twitter.com/MIT_CSAIL/status/1581313961093484545
{% endcomment %}

# Translations

- [Chinese (Simplified)](https://missing-semester-cn.github.io/)
- [Chinese (Traditional)](https://missing-semester-zh-hant.github.io/)
- [Japanese](https://missing-semester-jp.github.io/)
- [Korean](https://missing-semester-kr.github.io/)
- [Portuguese](https://missing-semester-pt.github.io/)
- [Russian](https://missing-semester-rus.github.io/)
- [Serbian](https://netboxify.com/missing-semester/)
- [Spanish](https://missing-semester-esp.github.io/)
- [Turkish](https://missing-semester-tr.github.io/)
- [Vietnamese](https://missing-semester-vn.github.io/)
- [Arabic](https://missing-semester-ar.github.io/)
- [Italian](https://missing-semester-it.github.io/)
- [Persian](https://missing-semester-fa.github.io/)
- [German](https://missing-semester-de.github.io/)
- [Bengali](https://missing-semester-bn.github.io/)

Note: এগুলো হচ্ছে community  translations  এর external  links । আমরা এগুলো যাচাই করে দেখিনি। 

আপনি কি এই class  এর course  notes  এর translation  বানিয়েছেন? একটা 
[pull request](https://github.com/missing-semester/missing-semester/pulls) submit  করুন যাতে আমরা ওটাকে list  এ অ্যাড করতে পারি।  

## Acknowledgements

We thank Elaine Mello, Jim Cain, and [MIT Open
Learning](https://openlearning.mit.edu/) for making it possible for us to
record lecture videos; Anthony Zolnik and [MIT
AeroAstro](https://aeroastro.mit.edu/) for A/V equipment; and Brandi Adams and
[MIT EECS](https://www.eecs.mit.edu/) for supporting this class.

---

<div class="small center">
<p><a href="https://github.com/missing-semester/missing-semester">Source code</a>.</p>
<p>Licensed under CC BY-NC-SA.</p>
<p>See <a href="/license/">here</a> for contribution &amp; translation guidelines.</p>
</div>
