---
title: AWS Global Infrastructure Part 2
course: aws-global-infrastructure-part-2
order: 5
layout: aws_post
---


### ইনফ্রাস্ট্রাকচার: AWS-এর ভিত্তি

Cloud অ্যাপ্লিকেশনের ভিত্তি হিসেবে এখনো ফিজিক্যাল ইনফ্রাস্ট্রাকচার, যেমন ডেটা সেন্টার ও নেটওয়ার্ক কানেক্টিভিটি বিদ্যমান। AWS-এ এই ফিজিক্যাল ইনফ্রাস্ট্রাকচার গঠন করে **AWS Global Infrastructure**, যার কাঠামোতে রয়েছে **Availability Zones (AZ)** এবং **Regions**।

---

### **Regions কী?**

**Regions** হলো বিশ্বের বিভিন্ন ভৌগলিক অবস্থানে অবস্থিত জায়গা, যেখানে AWS তাদের ডেটা সেন্টার হোস্ট করে। প্রতিটি AWS Region-এর নাম সেই এলাকার নাম অনুসারে দেওয়া হয়।

উদাহরণস্বরূপ:

* যুক্তরাষ্ট্রে **Northern Virginia Region** (us-east-1) এবং **Oregon Region** (us-west-2) রয়েছে।
* এশিয়া প্যাসিফিক, কানাডা, ইউরোপ, মধ্যপ্রাচ্য এবং দক্ষিণ আমেরিকাতেও রয়েছে একাধিক Region।
* AWS ক্রমাগত নতুন Region যোগ করছে, যাতে গ্রাহকদের চাহিদা পূরণ করা যায়।

প্রতিটি Region-এর দুটি পরিচয় থাকে:

1. ভৌগলিক নাম (Geographical Name)
2. Region কোড (Region Code)

**Region কোডের কয়েকটি উদাহরণ:**

* `us-east-1` → প্রথম Region যা যুক্তরাষ্ট্রের পূর্বাঞ্চলে তৈরি হয়। নাম: **N. Virginia**
* `ap-northeast-1` → এশিয়া প্যাসিফিক অঞ্চলের উত্তর-পূর্বের প্রথম Region। নাম: **Tokyo**

> মনে রাখবেন, প্রতিটি AWS Region একে অপর থেকে **সম্পূর্ণ স্বতন্ত্র (independent)**। আপনার স্পষ্ট অনুমতি ও নির্দেশনা ছাড়া একটি Region-এর ডেটা আরেকটি Region-এ **স্বয়ংক্রিয়ভাবে কপি হয় না**।

---

### **সঠিক AWS Region কীভাবে বেছে নেবেন?**

আপনার অ্যাপ্লিকেশন ও ওয়ার্কলোড কোন Region-এ হোস্ট করবেন তা নির্ধারণের সময় চারটি গুরুত্বপূর্ণ বিষয় বিবেচনা করতে হবে:

#### ১. Latency (বিলম্ব বা প্রতিক্রিয়ার সময়)

যদি আপনার অ্যাপ্লিকেশন latency-তে সংবেদনশীল হয়, তাহলে ইউজারদের কাছাকাছি অবস্থিত Region বেছে নেওয়াই ভালো।
উদাহরণ: **Gaming**, **VoIP/Telephony**, **WebSockets**, **IoT** — এসব অ্যাপ্লিকেশনে উচ্চ latency পারফরম্যান্সে বড় প্রভাব ফেলে। এমনকি Asynchronous অ্যাপ্লিকেশন যেমন **eCommerce**-এও latency সমস্যা তৈরি করতে পারে।

#### ২. Price (মূল্য)

প্রত্যেকটি Region-এ দাম ভিন্ন হতে পারে। এর পেছনে বিভিন্ন কারণ থাকে—ইন্টারনেট কানেক্টিভিটি, যন্ত্রাংশ আমদানির খরচ, কাস্টমস, রিয়েল এস্টেট মূল্য ইত্যাদি।
AWS সারা পৃথিবীজুড়ে একরকম দাম রাখে না—প্রতিটি Region-এর নিজস্ব অর্থনৈতিক কাঠামো অনুসারে দাম নির্ধারণ করে।

#### ৩. Service Availability (সার্ভিসের প্রাপ্যতা)

সব Region-এ সব AWS সার্ভিস পাওয়া যায় না। AWS ডকুমেন্টেশনে প্রতিটি Region-এ কোন সার্ভিসগুলো পাওয়া যায় তার একটি টেবিল দেওয়া থাকে।

#### ৪. Data Compliance (নিয়মনীতি মেনে চলা)

Enterprise প্রতিষ্ঠানগুলোকে অনেক সময় এমন নিয়ম মানতে হয়, যাতে গ্রাহকের ডেটা একটি নির্দিষ্ট ভৌগলিক এলাকায় সংরক্ষণ করতে হয়।
যদি এমন কোনো নিয়ম প্রযোজ্য হয়, তাহলে অবশ্যই সে অনুযায়ী Region নির্বাচন করতে হবে।

---

### **Availability Zones (AZ) কী?**

প্রত্যেকটি Region-এর মধ্যে থাকে একাধিক **Availability Zone (AZ)**।

AZ হলো এক বা একাধিক **ডেটা সেন্টারের সমষ্টি**, যেখানে বিদ্যুৎ, নেটওয়ার্কিং এবং কানেক্টিভিটিতে redundancy থাকে।

* প্রতিটি AZ operates করে সম্পূর্ণ আলাদা ফিজিক্যাল অবস্থান থেকে (ঠিকানা প্রকাশ করা হয় না)
* AZ-গুলোর মধ্যে থাকে দ্রুতগতির ও কম latency-র সংযোগ

**AZ গুলোর নামকরণ কিভাবে হয়?**
AZ-কে চিহ্নিত করা হয় Region কোডের সঙ্গে একটি অক্ষর (letter) যুক্ত করে।

উদাহরণ:

* `us-east-1a` → Northern Virginia Region-এর একটি AZ
* `sa-east-1b` → São Paulo Region-এর একটি AZ

যদি কোনো রিসোর্স `us-east-1c`-এ থাকে, তাহলে বুঝবেন এটি **us-east-1 Region**-এর **c AZ**-তে অবস্থান করছে।

---

### **AWS সার্ভিসের Scope (পরিসর) বোঝা**

আপনি যেই AWS সার্ভিস ব্যবহার করছেন, তার ওপর নির্ভর করে রিসোর্সটি নিচের যেকোনো একটি স্কোপে অপারেট করতে পারে:

* **AZ-level**
* **Region-level**
* **Global-level**

প্রতিটি সার্ভিসের কাঠামো আলাদা, তাই বুঝতে হবে—সার্ভিসটি কোন Scope-এ চলে, এবং এটি আপনার অ্যাপ্লিকেশন আর্কিটেকচারে কেমন প্রভাব ফেলে।

#### Region-scoped সার্ভিস:

* Region নির্বাচন করলেই চলবে, আলাদা করে AZ উল্লেখ করতে হয় না।
* AWS স্বয়ংক্রিয়ভাবে ডেটার durability এবং availability নিশ্চিত করে।
* যেমন: **Amazon S3**, **Amazon DynamoDB**, **AWS Lambda** ইত্যাদি।

#### AZ-scoped সার্ভিস:

* আপনাকে নির্দিষ্ট করে AZ বেছে নিতে হয়।
* এর ক্ষেত্রে, **উচ্চ availability ও ডেটার durability বজায় রাখা আপনার দায়িত্ব**।
* যেমন: **Amazon EC2 instance**, **Amazon RDS instance** ইত্যাদি।

---

### **Resiliency বজায় রাখা**

আপনার অ্যাপ্লিকেশন সর্বদা সচল রাখতে চাইলে আপনাকে নিশ্চিত করতে হবে:

* **High availability**
* **Resiliency**

একটি প্রতিষ্ঠিত Best Practice হলো **Region-scoped Managed Services** ব্যবহার করা—যেগুলোর ভেতরেই redundancy ও resiliency বিল্ট-ইন থাকে।

যদি তা সম্ভব না হয়, তাহলে আপনার ওয়ার্কলোড কমপক্ষে দুটি AZ-এ replicate করুন।
এর ফলে একটি AZ পুরোপুরি নষ্ট হলেও, দ্বিতীয় AZ থেকে আপনার অ্যাপ্লিকেশন সচল থাকবে এবং ইউজারদের ট্রাফিক পরিচালনা করতে পারবে।


<a href="https://aws.amazon.com/about-aws/global-infrastructure/" target="_blank" rel="noopener noreferrer">AWS: Global Infrastructure</a>

<a href="https://docs.aws.amazon.com/whitepapers/latest/aws-overview/global-infrastructure.html" target="_blank" rel="noopener noreferrer">AWS: AWS Global Infrastructure Documentation</a>

<a href="https://aws.amazon.com/about-aws/global-infrastructure/regions_az/" target="_blank" rel="noopener noreferrer">AWS: AWS Regions and Availability Zones</a>

<a href="https://docs.aws.amazon.com/general/latest/gr/rande.html" target="_blank" rel="noopener noreferrer">AWS: AWS service endpoints</a>

<a href="https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/" target="_blank" rel="noopener noreferrer">AWS: AWS Regional Services</a>
