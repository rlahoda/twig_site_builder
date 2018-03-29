# Simple Twig Site Builder
### A basic site builder that uses Twig templating

This is a simple site builder template that will let you quickly and easily get up and running to practice using Twig templating. It also includes SASS compiling (SCSS) and will automatically copy any images, scripts or other files you put into certain "dev" (development) folders over to the "prod" (production) folder.

### Requirements
- You need to have [Node.js](https://nodejs.org/en/) installed to use NPM for instalation
- You need to have some type of command line program and an understanding of how to use it *(if you're not familiar with how to use the command line, I would highly recommend Wes Bos' [Command Line Power User series](https://commandlinepoweruser.com/). It's free and will walk you through more than you ever thought you'd need to know about using the command line)*
- You need to understand the basics of working with SASS
- You need an understanding of how to write JSON data - It's pretty easy and a basic overview is below, but if you get confused, check out this [tutorial that will give you a good overview](https://beginnersbook.com/2015/04/json-tutorial/).

### Getting Started
- Copy the contents of this repo into your folder
- In your command line utility navigate to the folder and type "npm install" and press enter - this should install all the necessary bits that you'll need to build the site with
- To get started type "gulp" and press enter - this will run through all of the build steps then start a webserver on your computer and pull up the index.html page on your browser. If everything worked you should see the welcome message on the page
- To run the build process without starting a webserver type "gulp build" and press enter

### How Does This Work
#### SASS Compiling
- The SASS files are structured under the "scss" folder and you work with them as you would normally work with SASS.
- If you want to avoid Gulp errors, be sure to first create the file, then add the @import to the file you're importing it into. Otherwise, this will throw an error and you'll have to restart the Gulp process

#### Twig compiling
- Create the file you want to have as a .twig file in the "templates" folder. By doing this, an equivalent .html file will be created in the "prod" directory.
- Create any partials that you want to import in the "templates/partials" folder and they won't be created as stand-alone .html files in the "prod" directory.
- Create the data you want inserted into each file with a .twig.json file for the appropriate file (so index.twig would have index.twig.json)
- Add in the variables to the Twig template using standard Twig formatting {{ variable.sub.content }}
- The Gulp process will scan through the JSON and insert the appropriate content for each variable in your templates

#### Other File copy
- Anything you put into the "assets", "scripts", and "vendor" folders will be copied over to the equivalent folder in the "prod" folder
- The purpose of this is that if you write any scripts you can put them into the "scripts" folder and have them copied to the "prod/scripts" folder, same with images or other assets and if you have any 3rd party vendor plugins that you're using. So you can always have your working files in one place and the finished production files in another place. Once you're done working, you can copy the "prod" folder to a webserver and have your site ready to go.

#### Basic JSON Technique
This is going to be a pretty basic look at how to set up your JSON files for this project.

- To start with, always have an opening and closing curly bracket: `{ }`
- You set up pairs of information with the variable name in quotes on the left, a colon, then the content for that variable on the right in quotes: `"variable": "contents"`. This would translate into `{{ variable }}` when you want to access it in your Twig template
- You can nest values inside of others by enclosing them in further curly brackets:
```
{
  "page": {
    "contenttitle": "test page"
    }
}
```
To access this you would type `{{ page.contenttitle }}` in your Twig template.


- Make sure that each value has a unique name if you're putting more than one value together:
```
"bgs": {
      "bg1": {
        "path": "assets/img/photo63",
        "extension": ".jpg"
      },
      "bg5": {
        "path": "assets/img/photo60",
        "extension": ".jpg"
      },
      "bg4": {
        "path": "assets/img/photo71",
        "extension": ".jpg"
      },
      "bg3": {
        "path": "assets/img/photo30",
        "extension": ".jpg"
      },
      "bg2": {
        "path": "assets/img/photo2",
        "extension": ".jpg"
      }
```
- As you can see, each of these has a unique name: bg1, bg2, bg3, etc. The content inside of them, though, is consistently structures with a "path" and an "extension".
- **Always make sure you put a comma between values! Forgetting this will cause JSON errors**
- To access a value from the above array you can type: `{{ bgs.bg1.path }}` but that's tedious and neglects one of the many powerful features of Twig: loops.

If you create a for loop you can loop through the variables you've created:
```
{% for bg in bgs %}
  <a href="{{ bg.path }}{{ bg.extension }}"></a>
{% endfor %}
```

But wait, that doesn't have as many layers into it as I expected! Because when you do a loop like this, you're starting at the level that's being looped, in this case it's bg1, bg2, bg3...

There are a lot of other things you can do with this so check out the Twig documentation at [https://twig.symfony.com/](https://twig.symfony.com/)

For help checking out why your JSON isn't working, here's a [JSON validator](https://jsonlint.com/)

For any other questions, feel free to reach out to me via twitter: [@rlahoda](https://twitter.com/rlahoda/)
