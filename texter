import json
import urllib

from twilio.rest import TwilioRestClient 

ACCOUNT_SID = "ENTER_YOURS_HERE" 
AUTH_TOKEN = "ENTER_YOURS_HERE" 
sub = "http://sfbay.craigslist.org/sfc/bik/"
 
results = json.load(urllib.urlopen("https://www.kimonolabs.com/api/ds2da4og?apikey=ENTER_YOUR_APIKEY_HERE"))
data = results['results']['collection1']

latest_post = int(open('cl-text-notif/latest_post.txt').read())
max_topic = latest_post
new_ids = []
new_posts = []


for post in data:
	ad_id = int(post['title']['href'][len(sub):][:-5])

	if ad_id > max_topic:
		new_ids.append(ad_id)
		new_posts.append(post['price']['text'] + " " + post['title']['text'] + " " + post['title']['href'] + " " + post['area'])
		latest_post = max(new_ids)				

with open('bikeapp/latest_post.txt', 'w') as f:
    f.write(str(latest_post))

client = TwilioRestClient(ACCOUNT_SID, AUTH_TOKEN) 

for npost in new_posts:
		client.messages.create(
			to="YOUR_PHONE_NUMBER", 
			from_="YOUR_TWILLIO_NUMBER", 
			body=npost,  
		)
