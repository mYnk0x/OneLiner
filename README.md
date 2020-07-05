# OneLiner :fleur_de_lis:

Easy aliases to run via an SSH or terminal

- [Get all param](https://github.com/mYnk0x/OneLiner#get-all-param)
- [Broken Link Checker](https://github.com/mYnk0x/OneLiner#broken-link-checker)
- [XSS](https://github.com/mYnk0x/OneLiner#xss)
- [Takeover](https://github.com/mYnk0x/OneLiner#takeover)

## Get all param
```
gau domain.com | unfurl keys
```
```
gau domain.com|grep -Eio '\?\S*|tr '?' ' '|awk '{print $1}'|tr '&' '\n'|tr '=' ' '|awk '{print $1}'|sort -u
```
```
assetfinder --subs-only domain.com | waybackurls | grep "?url="
```
```
gron "https://otx.alienvault.com/otxapi/indicator/hostname/url_list/$1?limit=100&page=1" | grep "\burl\b" | gron --ungron | jq
```
```
gau $1 -subs | grep "=" | egrep -iv ".(jpg|jpeg|gif|css|tif|tiff|png|ttf|woff|woff2|ico|pdf|svg|txt|js)" | qsreplace -a | python3 dsss.py
```
```
gau domain.com > urls.txt;cat urls.txt | grep "?" | unfurl --unique format %s://%d%p > base.txt;cat base.txt | parallel -j 4 grep {} -m5 urls.txt | tee final.txt
```
```
gau domain.com | antiburl | awk '{print $4}' | grep -E '(callback=|jsonp=|api_key=|api=|password=|email=|emailto=|token=|username=|csrf_token=|unsubscribe_token=|p=|q=|query=|search=|id=|item=|page_id=|secret=|url=|from_url=|load_url=|file_url=|page_url=|file_name=|page=|folder=|folder_url=|login_url=|img_url=|return_url|return_to=|next=|redirect=|redirect_to=|logout=|checkout=|checkout_url=|goto=|next_page=|file=|load_file=|cmd=|ip=|ping=|lang=|edit=|LoginId=|size=|signature=|passinfo=)' | qsreplace
```

## Broken Link Checker
```
subfinder -d $1 | httprobe | waybackurls | egrep -iv ".(jpg|gif|css|png|woff|pdf|svg|js)" | burl | tee brokenlink.txt
```

## XSS
```
cat subdomains.txt | waybackurls >> wayback.txt
cat subdomains.txt | hakrawler -depth 3 -plain >> spider.txt
cat spider.txt wayback.txt | kxss
```

## Takeover
```
subfinder -d $1 >> hosts | assetfinder -subs-only $1 >> hosts | amass enum -norecursive -noalts -d $1 >> hosts | subjack -w hosts -t 100 -timeout 30 -ssl -c ~/subjack/fingerprints.json -v 3 >> takeover
```
