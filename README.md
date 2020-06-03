# week-6

Simple lab on connecting to APIs, getting objects, and storing data


Please sign up for the free account in (https://home.openweathermap.org) or (https://register.metoffice.gov.uk/WaveRegistrationClient/public/newaccount.do?service=datapoint) and get an API Key (remember sometimes it takes few mins/hours for API key to be enabled, so do this earlier. OpenWeatherMap emails you the API key when it;'s activated

Now let's test the curret weather:
`http://api.openweathermap.org/data/2.5/weather?q=london&appid=YourAPIKey`

So, I get:
`{"coord":{"lon":-0.13,"lat":51.51},"weather":[{"id":804,"main":"Clouds","description":"overcast clouds","icon":"04d"}],"base":"stations","main":{"temp":292.94,"feels_like":290.07,"temp_min":292.04,"temp_max":293.71,"pressure":1020,"humidity":48},"visibility":10000,"wind":{"speed":3.6,"deg":300},"clouds":{"all":97},"dt":1591090621,"sys":{"type":1,"id":1414,"country":"GB","sunrise":1591069687,"sunset":1591128561},"timezone":3600,"id":2643743,"name":"London","cod":200}`

* Try some online JSON parsers (http://json.parser.online.fr/)

Now, I don;t get that unit, so let me try another unit via (https://openweathermap.org/current#data):

`http://api.openweathermap.org/data/2.5/weather?q=london&units=metric&appid=YourAPIKey`

Now I get:
`{"coord":{"lon":-0.13,"lat":51.51},"weather":[{"id":804,"main":"Clouds","description":"overcast clouds","icon":"04d"}],"base":"stations","main":{"temp":20.11,"feels_like":17.31,"temp_min":18.89,"temp_max":21.11,"pressure":1020,"humidity":48},"visibility":10000,"wind":{"speed":3.6,"deg":300},"clouds":{"all":97},"dt":1591091701,"sys":{"type":1,"id":1414,"country":"GB","sunrise":1591069687,"sunset":1591128561},"timezone":3600,"id":2643743,"name":"London","cod":200}`


Let's see what's the temperature like:

`curl -s 'http://api.openweathermap.org/data/2.5/weather?q=london&units=metric&appid=YourAPIKey' `

Or can prase the string directly using Python json.load:

`curl -s 'http://api.openweathermap.org/data/2.5/weather?q=london&units=metric&appid=YourAPIKey' |  python3 -c "import sys, json; print(json.load(sys.stdin)['main']['temp'])"`

or here's one for Forex (please don;t abuse my key) 
(http://data.fixer.io/api/latest?access_key=d9f5f84da3c4a1d8c970d21c39c0824b)

Now, let's play around some nice images:

`brew install imagemagic`

Where's Freddie?
`curl https://www.imperial.ac.uk/ImageCropToolT4/imageTool/uploaded-images/website2--tojpeg_1523002441553_x1.jpg --output f.jpg `

Or a heart?
`curl https://www.desicomments.com/wp-content/uploads/2017/07/Hearts-Vortex-Heart.png --output h.png `

Now, let's merge them:
`composite -compose Dst_Over -geometry 520x320+20+80 f.jpg h.png FH.png`

`composite -compose Dst_Over -geometry 520x320+1050+700 f.jpg h.png FH.png`

`composite -gravity center "f.jpg" \( "h.png" -resize 400x400 \) "f.jpg" "new.png" `


Finally, let's put a label:
`convert new.png -gravity North -font Arial -annotate +0+100  'some text here' newnew.png`

I've messed up ghostscript installation so have to specify the full path 
`convert new.png -gravity North -font /System/Library/Fonts/HelveticaNeue.ttc -annotate +0+100  'some text here' newnew.png`

Now, Let's make it more fun "

First, let's get the temperature and store as a variable:
`myvar="$(curl -s 'http://api.openweathermap.org/data/2.5/weather?q=london&units=metric&appid=YourAPIKey' |  python3 -c "import sys, json; print(json.load(sys.stdin)['main']['temp'])") "`

`echo "$myvar"`

Then, let's complete the loop:

`convert new.png -font /System/Library/Fonts/HelveticaNeue.ttc -pointsize 20 
          -draw "gravity south 
                 fill white  text 5,25 'How hot is Freddie?' 
                 fill white  text 1,5 '$myvar' " 
          wmark_text_drawn.jpg `

Endless other tricks using (https://www.imagemagick.org/)

## Some exercises and fun


* Open and understand a schema
* Open and play with a payload
* Open a JSON payload (from the app-layer services) just to see it.
* Read a JSON object into your web app
* Query an API to convert £20 to Euros from your Web App
* Convert XML to and from JSON

** Feeling brave? Try getting some instragram data (my code might be out of date) (https://github.com/haddadi/Instagram)
