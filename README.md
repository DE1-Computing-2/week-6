# week-6

Simple lab on connecting to APIs, getting objects, and storing data



`brew install imagemagic`

`curl https://www.imperial.ac.uk/ImageCropToolT4/imageTool/uploaded-images/website2--tojpeg_1523002441553_x1.jpg --output f.jpg `

`curl https://www.desicomments.com/wp-content/uploads/2017/07/Hearts-Vortex-Heart.png --output h.png `

`composite -compose Dst_Over -geometry 520x320+20+80 f.jpg h.png FH.png`

`composite -compose Dst_Over -geometry 520x320+1050+700 f.jpg h.png FH.png`

`composite -gravity center "f.jpg" \( "h.png" -resize 400x400 \) "f.jpg" "new.png" `

Endless other tricks using (https://www.imagemagick.org/)


## Some exercises and fun

* Try some online JSON parsers (http://json.parser.online.fr/)
* Open and understand a schema
* Open and play with a payload
* Play with REST services, and use the UI to see the effects.
* Open a JSON payload (from the app-layer services) just to see it.
* Convert XML to and from JSON
