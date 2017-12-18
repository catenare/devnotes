# Tools
## Emmet
### Notes
* [Goodby Zen Coding](https://www.smashingmagazine.com/2013/03/goodbye-zen-coding-hello-emmet/) - Very good intro to Emmet.
* Visual Studio Code - [Emmet](https://code.visualstudio.com/docs/editor/emmet)
    * lorem ipsum screws up what is following it
    * lorem ipsum has to be last
* [Brand Colors](https://www.brandcolors.net) - List of brand colors
### Snippets
* **section#projects>h1>{Projects}^div.card*3>img[src="http://via.placeholder.com/250x200" alt="card"]>div>h2>{card title}^p>lorem10**
```html
<section id="projects">
  <h1>Projects</h1>
  <div class="card">
    <img src="http://via.placeholder.com/250x200" alt="card">
      <div>
        <h2>card title</h2>
        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Libero, blanditiis!</p>
      </div>
  </div>
  <div class="card">
    <img src="http://via.placeholder.com/250x200" alt="card">
      <div>
        <h2>card title</h2>
        <p>Consequatur voluptates repudiandae deserunt fuga. Magni, architecto labore. Ducimus, quisquam.</p>
      </div>
  </div>
  <div class="card">
    <img src="http://via.placeholder.com/250x200" alt="card">
      <div>
        <h2>card title</h2>
        <p>Libero, rerum fuga tempora distinctio sit praesentium labore animi odio!</p>
      </div>
  </div>
</section>
```
* **aside>img[src="http://via.placeholder.com/400x200" alt="main artile"]+p>{article details}^div>a[href="#"]{link}**
```html
<aside>
    <img src="http://via.placeholder.com/400x200" alt="main artile">
    <p>article details</p>
    <div><a href="#">link</a></div>
</aside>
```
* **footer>div>h2>{my title}^img[src="http://via.placeholder.com/200x200" alt="image"]^div>h2>{experience}^ul>li*3>{experience}^^div>h2>{skills}^ul>li*3>{skills}^^div>h2>{contact me}**
```html
<footer>
  <div>
    <h2>my title</h2>
    <img src="http://via.placeholder.com/200x200" alt="image">
  </div>
  <div>
    <h2>experience</h2>
    <ul>
      <li>experience</li>
      <li>experience</li>
      <li>experience</li>
    </ul>
    <div>
      <h2>skills</h2>
      <ul>
        <li>skills</li>
        <li>skills</li>
        <li>skills</li>
      </ul>
      <div>
        <h2>contact me</h2>
      </div>
    </div>
  </div>
</footer>
```

