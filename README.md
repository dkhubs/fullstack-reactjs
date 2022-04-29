# Full Stack ReactJS

[React Tutorial: An Overview and Walkthrough](https://www.taniarascia.com/getting-started-with-react)

- Basic familiarity with [HTML & CSS](https://internetingishard.com)

- Basic knowledge of [JavaScript](https://www.digitalocean.com/community/tutorial_series/how-to-code-in-javascript) and programming

- Basic understanding of the [DOM](https://www.taniarascia.com/introduction-to-the-dom)

- Familiarity with [ES6 syntax and features](https://www.taniarascia.com/es6-syntax-and-feature-overview)

- Install **[Node.js](https://nodejs.org) and [npm](https://www.npmjs.com)**

```
cd /usr/local/src/
wget https://nodejs.org/dist/v16.15.0/node-v16.15.0-linux-x64.tar.xz
tar xf node-v16.15.0-linux-x64.tar.xz -C /usr/local/ > /dev/null 2>&1

rm -rf /usr/local/bin/node /usr/bin/node /usr/local/bin/npm /usr/bin/npm /usr/local/bin/npx /usr/bin/npx
ln -s /usr/local/node-v16.15.0-linux-x64/bin/node /usr/local/bin/node
ln -s /usr/local/node-v16.15.0-linux-x64/bin/node /usr/bin/node
ln -s /usr/local/node-v16.15.0-linux-x64/bin/npm /usr/local/bin/npm
ln -s /usr/local/node-v16.15.0-linux-x64/bin/npm /usr/bin/npm
ln -s /usr/local/node-v16.15.0-linux-x64/bin/npx /usr/local/bin/npx
ln -s /usr/local/node-v16.15.0-linux-x64/bin/npx /usr/bin/npx
```
- [GitHub](https://www.taniarascia.com/getting-started-with-git)
### Setup and Installation ReactJS
#### Static HTML File
1. touch index.html
2. load in three CDNs in the head - React, React DOM, and Babel
3. make a `div` with an id called root
4. create a script tag and add some code
5. exec command `python3.9 -m http.server 8100`
6. browsing index.html
```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />

    <title>Hello React!</title>

    <script src="https://unpkg.com/react@16/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>
    <script src="https://unpkg.com/babel-standalone@6.26.0/babel.js"></script>
  </head>

  <body>
    <div id="root"></div>

    <script type="text/babel">
      class App extends React.Component {
        render() {
          return <h1>Hello world!</h1>
        }
      }

      ReactDOM.render(<App />, document.getElementById('root'))
    </script>
  </body>
</html>
```
#### [Create React App](https://github.com/facebook/create-react-app)
```
npx create-react-app my-app
cd my-app
npm start
```
#### Chrome Extensions
1. [React Developer Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)
2. [JSONView](https://chrome.google.com/webstore/detail/jsonview/chklaanhfefbnpoihckbnefhakgolnmc)

### React Usage
#### Components
1. touch Table.js
```
import React, {Component} from "react";

class Table extends Component {
    render() {
        return(
            <table>
            <thread>
                <tr>
                    <th>Name</th>
                    <th>Job</th>
                </tr>
            </thread>
            <tbody>
                <tr>
                    <td>Charlie</td>
                    <td>Janitor</td>
                </tr>
                <tr>
                    <td>Mac</td>
                    <td>Bouncer</td>
                </tr>
                <tr>
                    <td>Dee</td>
                    <td>Aspiring actress</td>
                </tr>
                <tr>
                    <td>Dennis</td>
                    <td>Bartender</td>
                </tr>
            </tbody>
        </table>
        )
    }
}

export default Table
```
2. modify App.js
```
import './App.css';
import Table from './Table';

function App() {
  return (
    <div className='App'>
      <Table />
    </div>
  )
}
```
#### Props
One of the big deals about React is how it handles data, and it does so with properties, referred to as `props`, and with `state`
1. First let's remove all the data from our TableBody component in `Table.js`
```
const TableHeader = () => {
  return (
    <thead>
      <tr>
        <th>Name</th>
        <th>Job</th>
      </tr>
    </thead>
  )
}

const TableBody = (props) => {
  const rows = props.data.forEach(element => {
    return (
      <tr>
        <td>{element.name}</td>
        <td>{element.job}</td>
      </tr>
    )
  })
  console.log(rows)

  return <tbody>{rows}</tbody>
}

class Table extends Component {
  render() {
    return (
      <table>
        <TableHeader />
        <TableBody data={this.props.data} />
      </table>
    )
  }
}

export default Table
```
2. Then let's move all that data to an array of objects, We'll have to create this array inside our render() in `App.js`
```
import Table from './Table';
import React, {Component} from 'react';

class App extends Component {
  render() {
    const data = [
      {
        name: 'Charlie',
        job: 'Janitor',
      },
      {
        name: 'Mac',
        job: 'Bouncer',
      },
      {
        name: 'Dee',
        job: 'Aspring actress',
      },
      {
        name: 'Dennis',
        job: 'Bartender',
      },
    ]

    return (
      <div className="container">
        <Table />
      </div>
    )
  }
}

export default App;
```
3. Now, we're going to pass the data through to the child component (Table) with properties in `App.js`. We can call the property whatever we want, and I'll put curly braces around it as it's a JavaScript expression
```
return (
  <div className="container">
    <Table data={data} />
  </div>
)
```
#### state
You can think of `state` as any data that should be saved and modified without necessarily being added to a database - for example, adding and removing items from a shopping cart before confirming your purchase
1. To start, we're going to create a state object. The object will contain properties for everything you want to store in the state
```
class App extends Component {
  state = {
    data: [
      {
        name: 'Charlie',
        job: 'Janitor',
      },
      {
        name: 'Mac',
        job: 'Bouncer',
      },
      {
        name: 'Dee',
        job: 'Aspring actress',
      },
      {
        name: 'Dennis',
        job: 'Bartender',
      },
    ],
  }
}
```
2. create a removeCharacter method on the parent App class
```
removeData = (index) => {
  const data = this.state

  this.setState({
    data: data.filter((data, i) => {
      return i !== index
    })
  })
}
```
3. Now we have to pass that function through to the component
```
render() {
  const data = this.state.data

  return (
    <div className="container">
      <Table data={data} removeData={this.removeData} />
    </div>
  )
}
```
5. In the TableBody component, we'll pass the key/index through as a parameter, so the filter function knows which item to remove
```
<tr key={index}>
  <td>{row.name}</td>
  <td>{row.job}</td>
  <td>
    <button onClick={() => props.removeCharacter(index)}>Delete</button>
  </td>
</tr>
```
#### Submitting Form Data

#### Pulling in API Data
[How to Connect to an API with JavaScript](https://www.taniarascia.com/how-to-connect-to-an-api-with-javascript)

A public API we can test with is the [Wikipedia API](https://en.wikipedia.org/w/api.php), and I have a [URL endpoint right here](https://en.wikipedia.org/w/api.php?action=opensearch&search=Seona+Dancing&format=json&origin=*) for a random* search

We're going to use [JavaScript's built-in Fetch](https://www.taniarascia.com/how-to-use-the-javascript-fetch-api-to-get-json-data) to gather the data from that URL endpoint and display it

1. touch Api.js
```
import React, { Component } from "react";

class App extends Component {
    state = {
        data: []
    }

    // Code is invoked after the component is mounted/inserted into the DOM tree
    componentDidMount() {
        const url = 'https://en.wikipedia.org/w/api.php?action=opensearch&search=Seona+Dancing&format=json&origin=*'

        fetch(url).then((result) => result.json()).then((result) => {
            this.setState({
                data: result
            })
        })
    }

    render() {
        const result = this.state.data.map((entry, index) => {
            return <li key={index}>{entry}</li>
        })
        return <ul>{result}</ul>
    }
}

export default App
```
2. Modify index.js
```
import App from './Api';
```

You can [read more about React components here](https://reactjs.org/docs/react-component.html)

#### Building and Deploying a React App
1. First, we're going to add a homepage field to package.json, that has the URL we want our app to live on
```
"homepage": "https://taniarascia.github.io/react-tutorial",
```
2. We'll also add these two lines to the scripts property
```
"scripts": {
  // ...
  "predeploy": "npm run build",
  "deploy": "gh-pages -d build"
}
```
3. In your project, you'll add gh-pages to the devDependencies
```
npm install --save-dev gh-pages
```
4. We'll create the build, which will have all the compiled, static files
```
npm run build
```
5. Finally, we'll deploy to gh-pages
```
npm run deploy
```
