## Welcome to my how-to on NASA's API for Mars Rover photos

First you'll want to check out the API at [https://api.nasa.gov/index.html](https://api.nasa.gov/index.html).  While you're there, pick up your very own api key [(here)](https://api.nasa.gov/index.html#apply-for-an-api-key).  That way you can run your own queries and not just the demo ones.

While there are many parts to this API, the part this how-to guide will address is the Mars Rover photos section of the API. Read about what is in the dataset and how the queries work here --> https://api.nasa.gov/api.html#MarsPhotos  

Now that you're set up with the API, let's dig into how to utilize it to get some cool pictures of Mars and to sort through the pictures to find ones from specific dates or specific cameras.

All of our queries will start with https://api.nasa.gov/mars-photos/api/v1/ and end with &api_key=xxxx where the 'xxxx' is your api key.

A simple first query to try out is https://api.nasa.gov/mars-photos/api/v1/rovers/opportunity/?&api_key=.  This query will return basic information about the Opportunity rover 

![](https://github.com/themightyscot/themightyscot.github.io/blob/master/Screen%20Shot%202017-03-01%20at%209.11.43%20PM.png)

and similar ones for Curiosity and Spirit

![](https://github.com/themightyscot/themightyscot.github.io/blob/master/Screen%20Shot%202017-03-03%20at%206.00.38%20PM.png)

![](https://github.com/themightyscot/themightyscot.github.io/blob/master/Screen%20Shot%202017-03-03%20at%206.07.46%20PM.png)

From this data, we can see that Spirit is no longer active though Opportunity and Curiosity are still up and about and taking pictures!

As you'll see from the data, there are two different ways of calculating the date: by Earth date or by Martian sol. The Martian sol is the amount of time a day takes on Mars and each rover counts the number of Martian days it has been on Mars starting with sol 1 as the Martian day on which it landed.

So if you wanted to see pictures Spirit took on October 23rd, 2004 you would query https://api.nasa.gov/mars-photos/api/v1/rovers/spirit/photos?earth_date=2004-10-23&api_key=.  Spirit took a lot of photos on that day so let's narrow it down a little and refine our query.  We'll just take a look at photos taken on that day by the Front Hazard Avoidance Camera (FHAZ) by adding the &camera=fhaz constraint to our query.  Now we get the following data:  

```markdown
{"photos":[{"id":284674,"sol":286,"camera":{"id":27,"name":"FHAZ","rover_id":7,"full_name":"Front Hazard Avoidance Camera"},
"img_src":"http://mars.nasa.gov/mer/gallery/all/2/f/286/2F151760895EFF8987P1110L0M1-BR.JPG","earth_date":"2004-10-23",
"rover":{"id":7,"name":"Spirit","landing_date":"2004-01-04","launch_date":"2003-06-10","status":"complete","max_sol":2208,
"max_date":"2010-03-21","total_photos":124550,"cameras":[{"name":"FHAZ","full_name":"Front Hazard Avoidance Camera"},
{"name":"NAVCAM","full_name":"Navigation Camera"},{"name":"PANCAM","full_name":"Panoramic Camera"},{"name":"MINITES","full_name":"Miniature Thermal Emission Spectrometer (Mini-TES)"},
{"name":"ENTRY","full_name":"Entry, Descent, and Landing Camera"},{"name":"RHAZ","full_name":"Rear Hazard Avoidance Camera"}]}},{"id":284675,"sol":286,"camera":{"id":27,"name":"FHAZ","rover_id":7,"full_name":"Front Hazard Avoidance Camera"},"img_src":"http://mars.nasa.gov/mer/gallery/all/2/f/286/2F151760895EFF8987P1110R0M1-BR.JPG","earth_date":"2004-10-23","rover":{"id":7,"name":"Spirit","landing_date":"2004-01-04","launch_date":"2003-06-10","status":"complete","max_sol":2208,"max_date":"2010-03-21","total_photos":124550,"cameras":[{"name":"FHAZ","full_name":"Front Hazard Avoidance Camera"},{"name":"NAVCAM","full_name":"Navigation Camera"},{"name":"PANCAM","full_name":"Panoramic Camera"},{"name":"MINITES","full_name":"Miniature Thermal Emission Spectrometer (Mini-TES)"},{"name":"ENTRY","full_name":"Entry, Descent, and Landing Camera"},{"name":"RHAZ","full_name":"Rear Hazard Avoidance Camera"}]}},{"id":284676,"sol":286,"camera":{"id":27,"name":"FHAZ","rover_id":7,"full_name":"Front Hazard Avoidance Camera"},"img_src":"http://mars.nasa.gov/mer/gallery/all/2/f/286/2F151761042EDN8987P1121L0M1-BR.JPG","earth_date":"2004-10-23","rover":{"id":7,"name":"Spirit","landing_date":"2004-01-04","launch_date":"2003-06-10","status":"complete","max_sol":2208,"max_date":"2010-03-21","total_photos":124550,"cameras":[{"name":"FHAZ","full_name":"Front Hazard Avoidance Camera"},{"name":"NAVCAM","full_name":"Navigation Camera"},{"name":"PANCAM","full_name":"Panoramic Camera"},{"name":"MINITES","full_name":"Miniature Thermal Emission Spectrometer (Mini-TES)"},{"name":"ENTRY","full_name":"Entry, Descent, and Landing Camera"},{"name":"RHAZ","full_name":"Rear Hazard Avoidance Camera"}]}},{"id":284677,"sol":286,"camera":{"id":27,"name":"FHAZ","rover_id":7,"full_name":"Front Hazard Avoidance Camera"},"img_src":"http://mars.nasa.gov/mer/gallery/all/2/f/286/2F151761042EDN8987P1121R0M1-BR.JPG","earth_date":"2004-10-23","rover":{"id":7,"name":"Spirit","landing_date":"2004-01-04","launch_date":"2003-06-10","status":"complete","max_sol":2208,"max_date":"2010-03-21","total_photos":124550,"cameras":[{"name":"FHAZ","full_name":"Front Hazard Avoidance Camera"},{"name":"NAVCAM","full_name":"Navigation Camera"},{"name":"PANCAM","full_name":"Panoramic Camera"},{"name":"MINITES","full_name":"Miniature Thermal Emission Spectrometer (Mini-TES)"},{"name":"ENTRY","full_name":"Entry, Descent, and Landing Camera"},{"name":"RHAZ","full_name":"Rear Hazard Avoidance Camera"}]}},{"id":284678,"sol":286,"camera":{"id":27,"name":"FHAZ","rover_id":7,"full_name":"Front Hazard Avoidance Camera"},"img_src":"http://mars.nasa.gov/mer/gallery/all/2/f/286/2F151759317ESF8987P1127L0M1-BR.JPG","earth_date":"2004-10-23","rover":{"id":7,"name":"Spirit","landing_date":"2004-01-04","launch_date":"2003-06-10","status":"complete","max_sol":2208,"max_date":"2010-03-21","total_photos":124550,"cameras":[{"name":"FHAZ","full_name":"Front Hazard Avoidance Camera"},{"name":"NAVCAM","full_name":"Navigation Camera"},{"name":"PANCAM","full_name":"Panoramic Camera"},{"name":"MINITES","full_name":"Miniature Thermal Emission Spectrometer (Mini-TES)"},{"name":"ENTRY","full_name":"Entry, Descent, and Landing Camera"},{"name":"RHAZ","full_name":"Rear Hazard Avoidance Camera"}]}}]}
```

If we visit the image source (look for the "img_src":.... in the query result) we find beautiful pictures of Mars!!!

![Image](http://mars.nasa.gov/mer/gallery/all/2/f/286/2F151760895EFF8987P1110L0M1-BR.JPG)


You can use the [editor on GitHub](https://github.com/themightyscot/themightyscot.github.io/edit/master/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/themightyscot/themightyscot.github.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
