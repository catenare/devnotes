# Storybook Tutorial

## Doing the Storybook Tutorial [Tutorial](https://www.learnstorybook.com/intro-to-storybook/react/en/get-started/)

- [Learn GraphQL](https://blog.hichroma.com/graphql-react-tutorial-part-1-6-d0691af25858)

### Setup

- Had to remove the global react app. Storybook requires the latest version of the create-react-app - [github issue](https://github.com/storybookjs/storybook/issues/9243)

* `yarn global remove create-react-app` worked to actually remove react cli.
* Trying to make this work.

* Run storybook and react app
  ** Storybook - port 9009
  ** React - port 3000 (will conflict with Rails)

* Checkout out the necessary resources
	* Resources for the tutorial - https://github.com/chromaui/learnstorybook-code.git - Need the `font` and `icon` directories.
  * Checking out the remote files - https://stackoverflow.com/questions/3334475/git-how-to-update-checkout-a-single-file-from-remote-origin-master

```sh
git remote add learn https://github.com/chromaui/learnstorybook-code.git
git fetch learn
git restore -s learn/master -- src/index.css
git restore -s learn/master -- public/font
git restore -s learn/master -- public/icon
```

### Build a simple component

- Had to write a function to handle evenPropogation

```jsx
const handleClick = e => {
  e.stopPropagation();
};
onClick = { handleClick };
```
* href attribute is required
```jsx
      {state !== "TASK_ARCHIVED" && (
          <a href="*" onClick={() => onPinTask(id)}>
            <span className={`icon-star`} />
          </a>
        )}
```

- Have to distinguish between the _storiesOf_ api and _Component Story Format(CSF)_ - [Story snapshot](https://github.com/storybookjs/storybook/tree/master/addons/storyshots/storyshots-core)