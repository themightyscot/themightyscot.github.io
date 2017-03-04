## Welcome to my how-to on NASA's API for Mars Rover photos

First you'll want to check out the API at [https://api.nasa.gov/index.html](https://api.nasa.gov/index.html).  While you're there, pick up your very own api key [here](https://api.nasa.gov/index.html#apply-for-an-api-key).  That way you can run your own queries and not just the demo ones.

While there are many parts to this API, the part this how-to guide will address is the Mars Rover photos section of the API. Read about what is in the dataset and how the queries work [here](https://api.nasa.gov/api.html#MarsPhotos).  Now that you're set up with the API, let's dig into how to utilize it to get some cool pictures of Mars and to sort through the pictures to find ones from specific dates or specific cameras. All of our queries will start with https://api.nasa.gov/mars-photos/api/v1/ and end with &api_key=xxxx where the 'xxxx' is your api key. A simple first query to try out is https://api.nasa.gov/mars-photos/api/v1/rovers/opportunity/?&api_key=.  This query will return basic information about the Opportunity rover 

```markdown
{"rover":{"id":6,"name":"Opportunity","landing_date":"2004-01-25","launch_date":"2003-07-07",
"status":"active","max_sol":4650,"max_date":"2017-02-22","total_photos":187093,
"cameras":{"name":"FHAZ","full_name":"Front Hazard Avoidance Camera"},
{"name":"NAVCAM","full_name":"Navigation Camera"},
{"name":"PANCAM","full_name":"Panoramic Camera"},
{"name":"MINITES","full_name":"Miniature Thermal Emission Spectrometer (Mini-TES)"},
{"name":"ENTRY","full_name":"Entry, Descent, and Landing Camera"},
{"name":"RHAZ","full_name":"Rear Hazard Avoidance Camera"}}}
```

and similar ones for Curiosity 
```markdown
{"rover":{"id":5,"name":"Curiosity","landing_date":"2012-08-06","launch_date":"2011-11-26",
"status":"active","max_sol":1626,"max_date":"2017-03-03","total_photos":306684,
"cameras":{"name":"FHAZ","full_name":"Front Hazard Avoidance Camera"},
{"name":"NAVCAM","full_name":"Navigation Camera"},
{"name":"MAST","full_name":"Mast Camera"},
{"name":"CHEMCAM","full_name":"Chemistry and Camera Complex"},
{"name":"MAHLI","full_name":"Mars Hand Lens Imager"},
{"name":"MARDI","full_name":"Mars Descent Imager"},
{"name":"RHAZ","full_name":"Rear Hazard Avoidance Camera"}}}
```

and Spirit
```markdown
{"rover":{"id":7,"name":"Spirit","landing_date":"2004-01-04","launch_date":"2003-06-10",
"status":"complete","max_sol":2208,"max_date":"2010-03-21","total_photos":124550,
"cameras":{"name":"FHAZ","full_name":"Front Hazard Avoidance Camera"},
{"name":"NAVCAM","full_name":"Navigation Camera"},
{"name":"PANCAM","full_name":"Panoramic Camera"},
{"name":"MINITES","full_name":"Miniature Thermal Emission Spectrometer (Mini-TES)"},
{"name":"ENTRY","full_name":"Entry, Descent, and Landing Camera"},
{"name":"RHAZ","full_name":"Rear Hazard Avoidance Camera"}}}
```

From this data, we can see that Spirit is no longer active though Opportunity and Curiosity are still up and about and taking pictures!

As you'll see from the data, there are two different ways of calculating the date: by Earth date or by Martian sol. The Martian sol is the amount of time a day takes on Mars and each rover counts the number of Martian days it has been on Mars starting with sol 1 as the Martian day on which it landed.

If you want to see the first pictures that Opportunity took after it landed you can query https://api.nasa.gov/mars-photos/api/v1/rovers/Opportunity/photos?sol=1&api_key=.  Now the first picture from that result is pretty lame so instead let's take a look at picture 268001 taken with the pancam

![Image](http://mars.nasa.gov/mer/gallery/all/1/p/001/1P128287181EFF0000P2303L2M1-BR.JPG)

and right before it, picture 149279 taken with the navcam

![Image](http://mars.nasa.gov/mer/gallery/all/1/n/001/1N128285132EDN0000P1500R0M1-BR.JPG)

What if you want to see the pictures taken by a rover on some specific date on Earth? Here is the query you would use if you wanted to see pictures Spirit took on October 23rd, 2004: https://api.nasa.gov/mars-photos/api/v1/rovers/spirit/photos?earth_date=2004-10-23&api_key=.  Spirit took a lot of photos on that day so let's narrow it down a little and refine our query.  We'll just take a look at photos taken on that day by the Front Hazard Avoidance Camera (FHAZ) by adding the &camera=fhaz constraint to our query.  Now we get data that looks like:  

```markdown
{"photos":{"id":284674,"sol":286,"camera":{"id":27,"name":"FHAZ","rover_id":7,
"full_name":"Front Hazard Avoidance Camera"},
"img_src":"http://mars.nasa.gov/mer/gallery/all/2/f/286/2F151760895EFF8987P1110L0M1-BR.JPG",
"earth_date":"2004-10-23",

```

If we visit the image source (look for the "img_src":.... in the query result) we find a beautiful picture of Mars!!!

![Image](http://mars.nasa.gov/mer/gallery/all/2/f/286/2F151760895EFF8987P1110L0M1-BR.JPG)

Curiosity has a camera called chemcam.  What do those pictures look like you might wonder...  Sadly there is no good way to query which days the rover took pictures with that camera. The best practice I could come up with for finding a "chemcam" picture was to search a certain day and request only chemcam pictures with a query like https://api.nasa.gov/mars-photos/api/v1/rovers/Curiosity/photos?sol=100&camera=chemcam&api_key= which is chemcam pictures from Curiosity's sol 100.

The first picture from that search is 

![Image](http://mars.jpl.nasa.gov/msl-raw-images/ods/surface/sol/00100/soas/rdr/ccam/CR0_406369429PRC_F0050104CCAM01100L1.PNG)

Pretty cool and up close, huh??

One of the most useful queries we can do is a manifest query.  This query will tell us for each sol, how many photos were taken and which cameras were utilized on that day. The query for the photo manifest for the Spirit rover would look like this: https://api.nasa.gov/mars-photos/api/v1/manifests/Spirit?&api_key= and the data looks like 

```markdown
{"photo_manifest":{"name":"Spirit","landing_date":"2004-01-04","launch_date":"2003-06-10",
"status":"complete","max_sol":2208,"max_date":"2010-03-21","total_photos":124550,
"photos":
{"sol":1,"total_photos":77,"cameras":["ENTRY","FHAZ","NAVCAM","PANCAM","RHAZ"]},
{"sol":2,"total_photos":125,"cameras":["MINITES","NAVCAM","PANCAM"]},
{"sol":3,"total_photos":125,"cameras":["NAVCAM","PANCAM","RHAZ"]},
{"sol":4,"total_photos":143,"cameras":["FHAZ","NAVCAM","PANCAM","RHAZ"]},
{"sol":5,"total_photos":353,"cameras":["NAVCAM","PANCAM"]},
{"sol":6,"total_photos":346,"cameras":["FHAZ","NAVCAM","PANCAM","RHAZ"]}
```

Interpreting these results we see that on sol 5 the Spirit rover took 353 pictures and only utilized the navcam and pancam cameras to take those photographs.


##### A couple additional functionalities that it would be nice to include in an update to this api are:
```markdown
1. The ability to search for multiple rovers' photos at the same time /rovers/spirit&curiosity/photos?earth_date=2017-3-1 for instance
2. The ability to search by camera rovers/Spirit?camera=navcam will currently just return the basic rover information instead of returning all the photos Spirit took with its navcam.  
```
###### Maybe there are more features that you would add to make finding cool Mars photos easier.


## Thanks so much for taking the time to visit my site and learn about the Mars Photos portion of the NASA api.  I hope you enjoyed it!!
