---
title: Interacting with AWS Part 2
course: aws-cloud-technical-essentials-week-1
order: 7
layout: aws_post
---


### **Reading 1.4: AWS-এর সঙ্গে ইন্টারঅ্যাকশন করা**

আপনি AWS-এ যেকোনো কাজ করলে সেটি মূলত একটি **API কল**, যেটি **অথেন্টিকেটেড** (সনাক্ত) এবং **অথরাইজড** (অনুমোদিত) হয়।

AWS-এ আপনি যেকোনো সার্ভিস বা রিসোর্সের সঙ্গে **API কলের মাধ্যমে** কাজ করতে পারেন। এই কলগুলো করা যায় তিনটি প্রধান উপায়ে:

1. **AWS Management Console**
2. **AWS Command Line Interface (CLI)**
3. **AWS Software Development Kits (SDKs)**


### **AWS Management Console**

Cloud রিসোর্স পরিচালনার একটি উপায় হলো **ওয়েব-ভিত্তিক কনসোল** ব্যবহার করা।
এখানে আপনি ব্রাউজারে লগইন করে প্রয়োজনীয় সার্ভিসে ক্লিক করে কাজ করতে পারেন।

যারা প্রথমবার ক্লাউডে কাজ শুরু করছেন, তাদের জন্য রিসোর্স তৈরি ও ম্যানেজ করার এটি সবচেয়ে সহজ উপায়।

নিচের স্ক্রিনশটটি দেখায়, আপনি যখন প্রথমবার AWS Management Console-এ লগইন করবেন তখন কী ধরনের ল্যান্ডিং পেজ দেখতে পাবেন।

![AWS-MANAGEMENT-CONSOLE]({{ site.baseurl }}/assets/images/AWS-MANAGEMENT-CONSOLE.png)


এই কনসোলে সার্ভিসগুলো **বিভিন্ন বিভাগে** সাজানো থাকে, যেমন:

* Compute
* Database
* Storage
* Security, Identity and Compliance

উপরে ডান পাশে থাকে **Region Selector**।
আপনি যদি সেখানে ক্লিক করে Region পরিবর্তন করেন, তাহলে আপনি যে সার্ভিসে রিকোয়েস্ট পাঠাবেন তা **নতুন Region**-এ যাবে।

এই সময় **URL-টিও পরিবর্তিত** হয়।
Region পরিবর্তন করার মানে, আপনি ব্রাউজারকে বলছেন একটি **আলাদা AWS Region**-এ রিকোয়েস্ট পাঠাতে, যার জন্য ব্যবহৃত হয় একটি ভিন্ন **Subdomain**।


### **AWS Command Line Interface (CLI)**

একটি পরিস্থিতি কল্পনা করুন—আপনার অ্যাপ্লিকেশনের Frontend-এর জন্য আপনি AWS-এ **দশ বা তার বেশি সার্ভার** চালাচ্ছেন।

আপনি প্রতিদিন **এই সব সার্ভার থেকে ডেটা সংগ্রহ করে একটি রিপোর্ট চালাতে** চান। কারণ সার্ভারের বিবরণ (Details) প্রতিদিন পরিবর্তিত হতে পারে।

এখন যদি আপনি প্রতিদিন ম্যানুয়ালি AWS Console-এ লগইন করে সেই তথ্য কপি-পেস্ট করেন, তাহলে সেটা সময়সাপেক্ষ ও ঝুঁকিপূর্ণ।

এই কাজটি আপনি সহজেই করতে পারেন **AWS CLI দিয়ে একটি Script চালিয়ে**—যা স্বয়ংক্রিয়ভাবে API কল করে সেই তথ্য নিয়ে আসবে।

**AWS CLI** হলো একটি **Unified Tool**, যা দিয়ে AWS-এর অনেক সার্ভিস আপনি কমান্ড লাইন থেকেই নিয়ন্ত্রণ ও স্ক্রিপ্ট করে অটোমেট করতে পারেন।

CLI ওপেন-সোর্স, এবং এটি Windows, Linux এবং Mac OS-এর জন্য ইনস্টলারসহ পাওয়া যায়।

**একটি CLI API কলের উদাহরণ:**

```bash
aws ec2 describe-instances
```

**এই রকম একটি Response আপনি পেতে পারেন:**

```json
{
  "Reservations": [
    {
      "Groups": [],
      "Instances": [
        {
          "AmiLaunchIndex": 0,
          ...
        }
      ]
    }
  ]
}
```


### **AWS Software Development Kits (SDKs)**

AWS-এ API কল আপনি **কোড লিখেও** করতে পারেন—এবং এর জন্য ব্যবহৃত হয় **AWS SDKs**।

**SDK** হলো একটি ওপেন-সোর্স টুলসেট, যেটি AWS তৈরি ও রক্ষণাবেক্ষণ করে **জনপ্রিয় প্রোগ্রামিং ভাষাগুলোর জন্য**, যেমন:

* C++
* Go
* Java
* JavaScript
* .NET
* Node.js
* PHP
* Python
* Ruby

ডেভেলপাররা সাধারণত **নিজেদের অ্যাপ্লিকেশনের সোর্স কোডকে AWS সার্ভিসের সঙ্গে ইন্টিগ্রেট** করতে SDK ব্যবহার করেন।

**উদাহরণ:**
ধরুন অ্যাপ্লিকেশনের ফ্রন্টএন্ড Python-এ লেখা।
প্রতিবার যখন একটি **বিড়ালের ছবি (cat photo)** আসে, তখন সেটি AWS-এর একটি Storage সার্ভিসে আপলোড করতে হয়।

এই কাজটি আপনি সরাসরি সোর্স কোডের ভেতর থেকেই করতে পারেন **Python AWS SDK** ব্যবহার করে।


### **একটি Python SDK কোডের উদাহরণ:**

```python
import boto3

ec2 = boto3.client('ec2')

response = ec2.describe_instances()

print(response)
```

এই কোডটি `boto3` লাইব্রেরি ব্যবহার করে EC2 সার্ভিস থেকে instance-এর তথ্য এনে প্রিন্ট করে।


এই অংশে আপনি AWS-এ কাজ করার **তিনটি প্রধান উপায়** শিখলেন:

* **Console:** শুরু করার জন্য সবচেয়ে সহজ
* **CLI:** স্ক্রিপ্ট করে দ্রুত এবং নির্ভুলভাবে কাজ
* **SDK:** কোডের মাধ্যমে প্রোগ্রাম্যাটিকভাবে AWS-কে নিয়ন্ত্রণ

এই কোর্সে আমরা প্রধানত **Console ব্যবহার করব**, তবে আপনি যদি একটু অভিজ্ঞ হন, তাহলে **CLI ব্যবহার করে নিজের দক্ষতা বাড়াতে পারেন**।


#### Resources:

<a href="https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/getting-started.html" target="_blank" rel="noopener noreferrer">AWS: Working with the AWS Management Console</a>

<a href="https://aws.amazon.com/cli/" target="_blank" rel="noopener noreferrer">AWS: AWS Command Line Interface</a>

<a href="https://aws.amazon.com/tools/" target="_blank" rel="noopener noreferrer">AWS: Tools to Build on AWS</a>
