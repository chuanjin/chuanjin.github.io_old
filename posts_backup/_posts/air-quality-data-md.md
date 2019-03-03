title: AQI 
date: 2016-11-10 14:50:47
tags: [Python]
categories: R&D
---

# Air Quality Index

I'v been experimenting to fetch data related to [AQI](https://en.wikipedia.org/wiki/Air_quality_index) in China recently.

A good resource is http://aqicn.org, which provides air pollution data in a good way by city, and I try to write a python script to crawl the data from it.

<!--more-->

{% gist chuanjin/07a0f43530464cabe7ff3cb45107e4d1%}

Another website is http://www.stateair.net/, it reports AQI from US consulate in Chinese major cities, i.e. Beijing, Shanghai, Guangzhou, Chengdu and Shenyang. Similarly, the code to fetch data from it shown below.

{% gist chuanjin/4d0307f1dbcb19c2743a348045b137ea%}

Both of the code above are using Python and handy packages like [requests](http://docs.python-requests.org/en/master/) and  [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/).

The stateair website also provides historical data for download in CSV format, therefore I use those data to create a simple visulization page. Check it from http://chuanjin.me/pm25/ and source code is availabe from Github [repo](https://github.com/chuanjin/pm25).


Last but not least, I found [pm25.in](http://pm25.in/) website, and they provide real time data for all Chinese cities, even better, they have opened their API for develper and I also created a Python library based on their API. Code available from https://github.com/chuanjin/python-aqi-zh


