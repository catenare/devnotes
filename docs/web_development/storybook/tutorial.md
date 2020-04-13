# Storybook

## About

- [Storybook](https://storybook.js.org/)
- [Examples](https://storybook.js.org/docs/examples/)
- [Mirage](https://miragejs.com/)
- [Microsoft Playwright](https://github.com/microsoft/playwright)
- [TypeScript](https://www.typescriptlang.org/)
- [Jest](https://jestjs.io/)

### Create a component

```jsx
import { React } from "react";
```

## Doing the Storybook Tutorial [Tutorial](https://www.learnstorybook.com/intro-to-storybook/react/en/get-started/)

### Notes

- [Storybook on medium](https://medium.com/storybookjs)

### Updates

- Storybook with main.js - [Declarative Storybook Configuration](https://medium.com/storybookjs/declarative-storybook-configuration-49912f77b78

### Setup

- Had to remove the global react app. Storybook requires the latest version of the create-react-app - [github issue](https://github.com/storybookjs/storybook/issues/9243)

* `yarn global remove create-react-app` worked to actually remove react cli.
* Trying to make this work.
* Using create react app - Storybook 3.5
  - `npx -p @storybook/cli sb init --type react_scripts`
* Run storybook and react app
  ** Storybook - port 9009
  ** React - port 3000 (will conflict with Rails)

* Checkout out the necessary resources \* Resources for the tutorial - https://github.com/chromaui/learnstorybook-code.git - Need the `font` and `icon` directories.
  - Checking out the remote files - https://stackoverflow.com/questions/3334475/git-how-to-update-checkout-a-single-file-from-remote-origin-master
* Url for personal github in .git/config "url = git@personal:catenare/TaskBox.git"

```
[remote "origin"]
	url = git@personal:catenare/TaskBox.git
	fetch = +refs/heads/*:refs/remotes/origin/*

```

```sh
git remote add learn https://github.com/chromaui/learnstorybook-code.git
git fetch learn
git restore -s learn/master -- src/index.css
git restore -s learn/master -- public/font
git restore -s learn/master -- public/icon
```

- Update package.json to run storybook on a different port and without going to the browser.

```json
"storybook": "start-storybook -p 9009 -s public --ci"
```

### Tutorial

#### Simple Component

- href attribute is required

```jsx
{
  state !== "TASK_ARCHIVED" && (
    <a href="*" onClick={() => onPinTask(id)}>
      <span className={`icon-star`} />
    </a>
  );
}
```

#### Screens

- InboxScreen.js - Import PureTaskList rather than TaskList
- Update App.test.js to no longer look for the test link.

```js
test("render taskbox screen", () => {
  const { getByText } = render(<App />);
  const linkElement = getByText(/Taskbox/i);
  expect(linkElement).toBeInTheDocument();
});
```

### Testing using chromatic
* Start chromatic without starting storybook - `--do-not-start`
