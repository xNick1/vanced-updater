import os
from requests import get
from bs4 import BeautifulSoup
from re import compile

size = os.path.getsize('version.txt')
if size == 0:
	oldver = "0"
else:
	f = open("version.txt", "r")
	oldver = f.read()

request = get("https://vanced.azurewebsites.net/apks?type=nonroot")
soup = BeautifulSoup(request.content, "lxml")
td = soup.find("td", text=compile("White/Black"))
version = td.find_next("td").text.strip()

if oldver != version:
	f = open("version.txt", "w")
	f.write(version)
	
	link = "https://vanced.azurewebsites.net{}".format(td.parent.find("a", text=compile("Download"), href=True)["href"])
	print(version, link)
	
	local_filename = "YoutubeVanced-version" + version + ".apk"
	r = get(link, stream=True)
	with open(local_filename, 'wb') as f:
		for chunk in r.iter_content(chunk_size=1024): 
			if chunk: 
				f.write(chunk)
