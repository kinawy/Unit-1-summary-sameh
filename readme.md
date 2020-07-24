# Unit 1 Review

## HTML Summary

1. Learned how to properly set up boilerplate, and arranging forms/ sections/ divs inside the body of the document.
2. Learned how to set id's for specific elements, and classes for elements that can share traits.
3. Learned how HTML forms operate, used one on my reddit search engine set up like this:

```javascript
<form action="">
    <input type="text" id = "input" placeholder="Enter Search Terms">
    <i class="fa fa-search" ></i>
  </form>
  <button type="button" class="btn btn-primary">Retry?</button>
```

## CSS Summary

1. Learned how to apply styling to HTML elements by using class and id selectors.
2. Learned proper order specificity, and how the page cascades down to get it's stylying.
3. Learned how to properly apply Bootstrap elements to HTML and CSS, one example being:

```HTML
<link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.3.1/css/all.css" integrity="sha384-mzrmE5qonljUremFsqc01SB46JvROS7bZs3IO2EmfFsd15uHvIt+Y8vEf7N7fWAU" crossorigin="anonymous">
  <link href="https://fonts.googleapis.com/css2?family=Codystar&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/css/bootstrap.min.css" integrity="sha384-9aIt2nRpC12Uk9gS9baDl411NQApFmC26EwAOH8WgZl5MYYxFfc+NcPb1dKGj7Sk" crossorigin="anonymous">
  <link rel="stylesheet" href="css/style.css">
```

```css
body {
    padding: 0;
    margin: 0;
    height: 100vh;
    width: 100%;
    background: #07051a;
    display: grid;
    justify-content: center;
}

#header {
    font-family: 'Codystar', cursive;
    color: red;
    text-align: center;
}

#description {
    font-family: 'Codystar', cursive;
    color: white;
    text-align: center;
}


form{
    position: relative;
    top: 50%;
    left: 50%;
    transform: translate(-50%,-50%);
    transition: all 1s;
    width: 50px;
    height: 50px;
    background: white;
    box-sizing: border-box;
    border-radius: 25px;
    border: 4px solid white;
    padding: 5px;
    
}

input{
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;;
    height: 42.5px;
    line-height: 30px;
    outline: 0;
    border: 0;
    display: none;
    font-size: 1em;
    border-radius: 20px;
    padding: 0 20px;
}

.fa{
    box-sizing: border-box;
    padding: 10px;
    width: 42.5px;
    height: 42.5px;
    position: absolute;
    top: 0;
    right: 0;
    border-radius: 50%;
    color: #07051a;
    text-align: center;
    font-size: 1.2em;
    transition: all 1s;
}

form:hover{
    width: 200px;
    cursor: pointer;
}

form:hover input{
    display: block;
}

form:hover .fa{
    background: #07051a;
    color: white;
}

button {
    font-family: 'Codystar', cursive;
    /* width: 50px;
    height: 25px; */
    align-self: center;
    visibility: hidden;
    
}
```

## JS Summary

1. Learned the fundamentals of javascript, how for loops and conditions work, how to properly execute functions, and how call back functions can be helpful and how they work.
2. Learned the basics of fetch/Async/Await, and what promises are, execute on successfully in my reddit fetch slide show and use a callback function to parse the data, and ultimately push that data onto my html:
```javascript
fetch(input)
        .then(response => {
            return response.json();
        })
        .then(data => {


            makeImage(data)

        })
        .catch(error => {
            console.log('Error', error)
        })
```
3. This function rotates the source of an existing image tag at a set interval, allowing for a little slide show of archived reddit images, pulled by typing in a search parameter:
```javascript
function makeImage(data) {

    let loopArray = data.data.children;

    console.log(loopArray)

    setInterval(function () {



        console.log(count)
        image1.src = picArray[count]
        image1.style.height = '500px';
        image1.style.width = '500px';
        image1.style.borderRadius = '10px';
        count++;

        if (count === picArray.length) {
            count = 0;
        }

    }, 1000);



    for (let i = 0; i < loopArray.length; i++) {
        let pic = loopArray[i].data.url;
        if (pic.includes('jpg')) {
            picArray.push(pic);

            console.log(picArray)
        }
    };

}
```
4. Learned about classes and how to apply a constructor function to them, essentially allowing you to create a factory that can pump out objects with set key value pairs, and add more in at your leisure:
```javascript
class GitHubProfile {
    // constructor is a function that creates the class
    constructor(username, name, url) {
        this.username = username;
        this.name = name;
        this.url = url;
    }
    // You can call functions inside, not sure why yet
    intro() {
        console.log(`My name is ${this.name}, and my username is ${this.username}. Check me out at ${this.url}.`)
    }
}

// Fetching from my github
fetch('https://api.github.com/users/kinawy')
    .then(response => {
        return response.json();
    })
    .then(data => {
        console.log(data);
        let url = data.url;
        let login = data.login;
        let type = data.type;
        let sameh = new GitHubProfile(type, login, url);
        sameh.intro();
        console.log(sameh);

    })
```