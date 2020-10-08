---
name: 'Interactive Maps'
description: 'Learn JS and HTML while making a fun interactive map'
author: '@JeswinSunsi'
---

# Making an interactive map using Javascript

By the end of this tutorial, you will learn to use functions and if-else statements in nothing but Vanilla JS to create some really good-looking interactive maps. This workshop will also teach you the basics of HTML. As a bonus, read till the end for a fun programming fact.

- Demo - https://interactive-maps.jeswinsunsi.repl.co/
- Final code - https://repl.it/@JeswinSunsi/Interactive-Maps#index.html

![gif demo](https://cloud-fmga8dmlt.vercel.app/gif_one.gif)

## 1 - Prerequisites

- Basic understanding of functions
- Amateur knowledge of HTML and CSS

In case you don't know either of those, don't worry. We'll go through each line of code in depth.

## 2 - Tools and Resources

- For this tutorial, we'll be using repl.it, an online browser-based IDE
- For editing the photos, we can use Pixlr.com or any other full fledged photo editor
- I recommend going through https://www.w3schools.com/js/js_functions.asp for further clarification with the JS part

## 3 - Designing the image

Any suitable image will work, but I have chosen an animated isometric map. The image was of the JPG format, but I removed the background to get a png image. Then from that one image, I selected specific areas and created 5 different images, each with a different area highlighted in red.
For a visual understanding, here is the original image followed by an edited one.

![image 1](https://cloud-fyde5ir0a.vercel.app/image.png)
![image 2](https://cloud-jmd1dy3k8.vercel.app/image.png)

Basically, you'll have to take an image, and seperately highlight/color parts of it, and save it as different images. Here are the image resources I'm using:

- https://cloud-coh6o3mhy.vercel.app/orgbg.png - The original image
- https://cloud-9p8jb8vst.vercel.app/orgocean.png - Here, the ocean is highlighted in red
- https://cloud-gga696gyn.vercel.app/orgresidential.png - Here, the buildings are highlighted
- https://cloud-bzeicw4mm.vercel.app/orgroad.png - The roadway is highlighted
- https://cloud-9ldvvvhb4.vercel.app/orgvendors.png - The shops are highlighted
- https://cloud-3bvmpy2n1.vercel.app/orgbeach.png - The beach is highlighted

## 4 - Coding it up

### The boilerplate

Head over to [this starter project](https://repl.it/@JeswinSunsi/InteractiveMapsStarter). Creating an account is of personal preference, be warned that you may lose your work if you don't have an account. As soon as you start typing, the project will be forked/added over to your account. The CSS is already filled in for you.

![html boilerplate](https://cloud-5egibvgdv.vercel.app/image.png)

As you can see, repl has already created the boilerplate code for your project. Let's take a quick look.
`<!DOCTYPE html>` is a declaration line that means we'll be coding in HTML 5.0. Following up are the `<html>` and `<head>` tags. Our html markup will be contained inside the two `<html>` tags. The `<head>` tag is where we will put some of our specifications which we normally don't want the end-user to see. The first `<meta>` tag tells the browser which character set to use. Here, it is set to UTF-8. The next `<meta>` tag specifies the page's dimensions and scaling. There is no problem in not understanding how these tags work, as they aren't very important.

`<title>` is something that you should probably change. It is the text that is shown on the browser tab. Here it is set to repl.it. Coming next up in the `<head>` tag is `<link>`. It tells the browser to load the CSS styling from the style.css file. It also informs the browser that it a css text file.

Now we see a `</head>` tag. We have already seen a tag similar to this after the title tag, so what is it? having a slash before the name of any tag usually means that particular tag is ending. Here, it is a `</head>` tag, so the head of our html file ends here. It gives way to the body tag. `<body>` is where we write the markup that the viewer will see. Repl.it has already created a `<script>` tag here that imports the JS code. Now that we have finished with understanding the boilerplate, let's start writing some of our own code.

### The HTML Markup

As we can see from the final website gif, our site will have two parts, the first part which houses the buttons, and the second part, which houses the actual map. Let's get on with writing the code for the buttons.

We can use HTML default buttons, but they look like they should've been abandoned along with Windows 1999, so let's spice things up a little and design some buttons of our own. Above the `<script>` tag and below the opening `<body>` tag, add this.

```html
<div class="first" style="margin-left:auto;margin-right:auto;">
  <a onmouseover="changeImage('ocean')" class="button pulse">Ocean</a>
  <a onmouseover="changeImage('beach')" class="button pulse">Beach</a>
  <a onmouseover="changeImage('roadway')" class="button pulse">Roadway</a>
  <a onmouseover="changeImage('vendors')" class="button pulse">Vendors</a>
  <a onmouseover="changeImage('residential')" class="button pulse"
    >Residential</a
  >
</div>
```

Going through the code, we find a `<div>` tag. Divs are a way of grouping multiple obects into one. Divs also have various styling properties. This div tag has two attributes, class and style. Class is just a way to apply similar styles to multiple objects in CSS. The second attribute is style. It's a way of directly styling an element inside HTML. Margin-left and Margin-left sets the margins of the div. Here, to auto.  
Read more about margins at https://www.w3schools.com/css/css_margin.asp.  
Inside the Div, we have 5 `<a>` tags. We will tweak these tags to create the buttons, although some other tags can be used for this too. All these buttons share the same classes -> button & pulse. the other attribute, onmouseover, does exactly what it means. It calls a javascript function when the mouse is over that particular element. Right now if you run the markup, it'd be a total mess. So let's add the rest of it. Immediatly under the closing `</div>` tag, add

```html
<img
  id="map"
  src="https://imgur.com/6MXYopz.png"
  onmouseover="changeImage('normal')"
/>
```

This creates an image with the ID set as map and with its source at that specific url. The ID is basically a way of naming elements. Now when the webpage is rendered, it should be showing the buttons and the map image properly.

### The JavaScript Part

Finally! The functionality to our interactive map. These is where we use functions. Functions are reusable blocks of code that are callable from our HTML document. There are different types of functions in javascript, here we'll be using the most basic one. A function is written like this,

```js
function myFunctionName(parameter) {
  //some code here
}
```

Each function starts with the function keyword. This is followed by the function's name. After this come's the parameters. Parameters are variable values that we can use inside the function. These are specified when the function is being called. Parameters are optional. For example, here is a function that adds two numbers. It has two parameters.

```js
function addNumbers(firstNum, secondNum) {
  console.log(firstNum + secondNum)
}
```

And here is a function without a parameter. It simply prints out 'hello world'.

```js
function sayHello() {
  console.log('Hello World!')
}
```

These can now be called from our HTML file as addNumbers(someNumber, someNumber) and sayHello(). Now that you have a basic understanding of how functions work, head over into your `script.js` file and add this in.

```js
var map = document.getElementById('map')
function changeImage(location) {
  if (location == 'ocean') {
    map.src = 'https://cloud-9p8jb8vst.vercel.app/orgocean.png'
  } else if (location == 'residential') {
    map.src = 'https://cloud-gga696gyn.vercel.app/orgresidential.png'
  } else if (location == 'roadway') {
    map.src = 'https://cloud-bzeicw4mm.vercel.app/orgroad.png'
  } else if (location == 'vendors') {
    map.src = 'https://cloud-9ldvvvhb4.vercel.app/orgvendors.png'
  } else if (location == 'beach') {
    map.src = 'https://cloud-3bvmpy2n1.vercel.app/orgbeach.png'
  } else if (location == 'normal') {
    map.src = 'https://cloud-coh6o3mhy.vercel.app/orgbg.png'
  }
}
```

This snippet declares a variable named map, which corresponds to the map element in our html file. Then it creates a function named changeImage() with the parameter 'location'. When we call this function from our html file with specific values like 'ocean' or 'residential', (These values passed into parameters are called arguments.) they call on the actual function from the JS file.

Inside the function, is an if else-if statement. It does exactly what it means. If the location argument is 'beach', set the map's src attribute to the beach highlighted image, and so on. The syntax is

```js
if (condition) {
  // Do something;
} else if (anotherCondition) {
  // Do something else;
} else {
  // Do something totally different;
}
```

There are three basic if statements in Javascript. The normal if statement, the if - else statement, and the if - else if - Else statement. Not sure what that means? Let's go through some examples.

```js
var name = 'Shane'
if (name == 'Shane') {
  console.log('Hello Shane')
}
```

This snippet shows a basic if statement. It first declares a variable called name which has the value of shane. Then the if statement proceeds to check out if the name is Shane, and if yes, it logs out 'Hello Shane'. Note that nothing happens if the name is not set to Shane. To try this for yourself, create a seperate repl with the language set to JavaScript only. Paste that snippet and tweak the values.

Also, it's time to talk about the equal to symbols. Why only one equal sign at the first and two equal signs at the bottom? This is because one equal sign sets the value of the left hand side to the right hand side and two equal signs compare both the values. Here, we have used an equal sign and set the value of name to Shane. Then we have used two equal signs to check **if** the name and Shane are both the same.

Now, time for the next snippet. This one shows a basic if-else statement.

```js
var pass = prompt('Enter your passcode: ')
if (pass == 'abcd') {
  console.log('Password Accepted')
} else {
  console.log('Access Denied')
}
```

Now you probably wouldn't be knowing about prompt. Prompt is a function that allows us to take in user input. If you run this code in your Javascript-only repl, you'll get what I mean. Now let's dive into the code. It creates a variable named pass which gets user data. It then checks **if** the pass is 'abcd'. If the pass is abcd, it logs out that the password is accepted. **else**, it logs out that access is denied. A quick word about prompt, prompt will appear different when you're using it with html. Here's a look.

![prompt in html/js](https://cloud-i7mb1y4jx.vercel.app/1243.jpg)

Finally, the last if statement. This one checks **if** a condition is true, **else if** that condition is not true, it does something different, **else** it'll do something different. Here's a quick snippet. Be sure to run all these snippets so that you can see it live in-action.

```js
var name = prompt('Enter your name: ')
if (name == 'Shane') {
  console.log('Hello Shane')
} else if (name == 'Leah') {
  console.log('Hello Leah')
} else {
  console.log('Hello!')
}
```

Since you already know about if statements and if - else statements, this one would be a no-brainer. It asks the user for a name, **if** the name is Shane, it logs out Hello Shane, **else if** the name is Leah, it logs out Hello Leah, **else** it simply logs out Hello!.

## Conclusion

And just like that, you have gone through the basics of HTML/CSS and a bit of JS to create your own interactive map. Now it's up to you to add in a bit of your sparkle and tweak it.

- Orginal Demo - https://interactive-maps.jeswinsunsi.repl.co/
  - Source Code - https://repl.it/@JeswinSunsi/Interactive-Maps
- With continents - https://interactivemaps2.jeswinsunsi.repl.co
  - Source Code - https://repl.it/@JeswinSunsi/InteractiveMaps2
- Another use, with a 1 - 10 multiplication table - https://interactivemaps3.jeswinsunsi.repl.co
  - Source Code - https://repl.it/@JeswinSunsi/InteractiveMaps3
- Interactive Solar System - http://interactivemaps4.jeswinsunsi.repl.co/
  - Source Code - https://repl.it/@JeswinSunsi/InteractiveMaps4

A quick word, if the website doesnt look proper on your device, or if the buttons are too sideways, don't worry. This site is not responsive. You'll have to go into your styles.css and tweak the height and width from the `#map` id, and the left style of the `.first` class.

![multiplication table](https://cloud-66xb1ygia.vercel.app/multiplication.gif)
![solar system](https://cloud-ahc3o6oq6.vercel.app/solsys.gif)

## Hacking it

- Try doing the same thing with another image, maybe the inside of a room, maybe a world map with hoverable buttons which highlight different countries
- Tweak the buttons and add new styles to them
- Fork the Solar System project and add a textbox that shows some properties of each planet when the respective planet's button is hovered on or clicked
- Maybe add in a bit of music? The possibilities are endless

### Debugging

If you have followed the tutorial word by word, the end result would come out as expected. Else if you have some trouble in some part, feel free to check up the project's final code at the repl. You can also compare your code with the final source code by visiting https://text-compare.com/.

### A fun fact

The term 'patching' and 'patches', in software development, came from the early days when punch card code was the norm. To fix an error in the punch card, developers used to patch up the hole with a fabric.

And that's it for this workshop, happy coding!