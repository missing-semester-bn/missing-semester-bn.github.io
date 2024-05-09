---
layout: page
title: আপনার সি. এস শিক্ষার মিসিং সেমিস্টার
nositetitle: true
---

ক্লাসগুলি আপনাকে অপারেটিং সিস্টেম থেকে মেশিন লার্নিং পর্যন্ত সিএস-এর মধ্যে উন্নত বিষয়গুলি সম্পর্কে সমস্ত কিছু শেখায়, তবে একটি সমালোচনামূলক বিষয় রয়েছে যা খুব কমই আচ্ছাদিত হয় এবং এর পরিবর্তে শিক্ষার্থীদের নিজেরাই খুঁজে বের করার জন্য ছেড়ে দেওয়া হয়ঃ তাদের সরঞ্জামগুলির সাথে দক্ষতা। আমরা আপনাকে শিখিয়ে দেব কিভাবে কমান্ড-লাইনে দক্ষতা অর্জন করতে হয়, একটি শক্তিশালী টেক্সট এডিটর ব্যবহার করতে হয়, সংস্করণ নিয়ন্ত্রণ ব্যবস্থার অভিনব বৈশিষ্ট্যগুলি ব্যবহার করতে হয় এবং আরও অনেক কিছু!

শিক্ষার্থীরা তাদের শিক্ষা চলাকালীন (এবং তাদের কর্মজীবনে হাজার হাজার) এই সরঞ্জামগুলি ব্যবহার করে শত শত ঘন্টা ব্যয় করে তাই অভিজ্ঞতাকে যতটা সম্ভব তরল এবং ঘর্ষণহীন করে তোলা বোধগম্য। এই সরঞ্জামগুলিতে দক্ষতা অর্জন করা আপনাকে কেবল আপনার ইচ্ছার সাথে কীভাবে আপনার সরঞ্জামগুলি বাঁকানো যায় তা নির্ধারণ করতে কম সময় ব্যয় করতে সক্ষম করে না, এটি আপনাকে এমন সমস্যাগুলি সমাধান করতেও সহায়তা করে যা আগে অসম্ভব জটিল বলে মনে হত।

[এই ক্লাসের পিছনে অনুপ্রেরণা](/about/) সম্পর্কে পড়ুন

{% comment %}
# Registration

Sign up করুন  IAP 2020 class  এর জন্য  এই [registration form](https://forms.gle/TD1KnwCSV52qexVt9) form  fill-up  করে।  
{% endcomment %}

# সময়সূচী

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

বক্তৃতাগুলির ভিডিও রেকর্ডিং [ইউটিউবে](https://www.youtube.com/playlist?list=PlyzOVJj3bHQuloKGG59rS43e29ro7I57J)পাওয়া যায়

#ক্লাস সম্পর্কে

**স্টাফ**: এই ক্লাস সহ-শেখানো হয় [Anish](https://www.anishathalye.com/) [জন](https://thesquareplanet.com/) এবং [জোসে](http://josejg.com/)<br>
**প্রশ্ন**: আমাদের ইমেল করুন [Missing-semester@mit.edu](mailto:Missing-semester@mit.edu)

# এমআইটির বাইরে

আমরা এই ক্লাসটি এম. আই. টি-র বাইরেও ভাগ করে নিয়েছি এই আশায় যে অন্যরা এই সংস্থানগুলি থেকে উপকৃত হতে পারে। আপনি পোস্ট এবং আলোচনা খুঁজে পেতে পারেন

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

দ্রষ্টব্যঃ এগুলি কমিউনিটি অনুবাদের বাহ্যিক লিঙ্ক। আমরা তাদের পরীক্ষা করিনি।

আপনি কি এই ক্লাসের কোর্স নোটগুলির একটি অনুবাদ তৈরি করেছেন? একটি [pull request](https://github.com/missing-semester/missing-semester/pulls) জমা দিন যাতে আমরা এটি তালিকায় যুক্ত করতে পারি!

#স্বীকৃতি

আমরা ইলেইন মেলো, জিম কেইন, এবং [এমআইটি ওপেন লার্নিং](https://openlearning.mit.edu/) আমাদের জন্য বক্তৃতা ভিডিও রেকর্ড করা সম্ভব করার জন্য ধন্যবাদ; অ্যান্টনি Zolnik এবং [এমআইটি AeroAstro](https://aeroastro.mit.edu/) এ/ভি সরঞ্জামের জন্য; এবং ব্র্যান্ডি অ্যাডামস এবং [এমআইটি EECS](https://www.eecs.mit.edu/) এই ক্লাস সমর্থন করার জন্য।

---

<div class="small center">
<p><a href="https://github.com/missing-semester/missing-semester">Source code</a>.</p>
<p>Licensed under CC BY-NC-SA.</p>
<p>See <a href="/license/">here</a> for contribution &amp; translation guidelines.</p>
</div>
