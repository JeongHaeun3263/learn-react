# React

## Basic

### Component

1.

**App.js**

```javascript
import React from 'react';

const Header = () => {
	return (
		<header>
			<h1>Header</h1>
		</header>
	);
};

const App = (props) => {
	return <Header />;
};

export default App;
```

2.

**App.js**

```javascript
import React from 'react';
import Header from './components/Header';

const App = (props) => {
	return <Header />;
};

export default App;
```

**Header.js**

```javascript
import React from 'react';

const Header = (props) => <h1>Header</h1>;

export default Header;
```

### Props

```javascript
import React from 'react';

const Header = (props) => <h1>Welcome, {props.name}</h1>;

const Footer = (props) => {
	// destructuring
	const { year } = props;
	return <div>copyright {year}</div>;
};

const App = (props) => {
	return (
		<React.Fragment>
			<Header name='Grace' />
			<Footer year={new Date().getFullYear()} />
		</React.Fragment>
	);
};

export default App;
```

**Result**
![result](/src/assets/images/1.png)

#### Working with list

**App.js**

```javascript
import React from 'react';
import SkillsList from './components/SkillsList';

const App = (props) => {
	const skills = ['HTML5', 'CSS3', 'JavaScript', 'React'];

	return (
		<React.Fragment>
			<SkillsList skills={skills} />
		</React.Fragment>
	);
};

export default App;
```

**SkillsList.js**

```javascript
import React from 'react';

const SkillsList = ({ skills }) => {
	return (
		<ul>
			{skills.map((skill) => (
				<li>{skill}</li>
			))}
		</ul>
	);
};

export default SkillsList;
```

**Result**
![result](/src/assets/images/2.png)

_Key props have to be included_

**App.js**

```javascript
import React from 'react';
import SkillsList from './components/SkillsList';

const App = (props) => {
	const skills = ['HTML5', 'CSS3', 'JavaScript', 'React'];
	// const skillObjs = skills.map((skill, i) => ({ id: i, title: skill }));
	const skillObjs = [
		{ id: 1, title: 'HTML5' },
		{ id: 2, title: 'CSS3' },
		{ id: 3, title: 'JavaScript' },
		{ id: 4, title: 'React' },
	];

	return (
		<React.Fragment>
			<SkillsList skills={skillObjs} />
		</React.Fragment>
	);
};

export default App;
```

**SkillsList.js**

```javascript
import React from 'react';

const SkillsList = ({ skills }) => {
	return (
		<ul>
			{skills.map((skill) => (
				<li key={skill.id}>{skill.title}</li>
			))}
		</ul>
	);
};

export default SkillsList;
```

### Hooks

#### useState

##### Example 1

```javascript
import React, { useState } from 'react';

const App = (props) => {
	const [number, setNumber] = useState(0);

	const increaseNumber = () => {
		setNumber(number + 1);
	};

	const decreaseNumber = () => {
		setNumber(number - 1);
	};

	return (
		<>
			<h1>number: {number}</h1>
			<button onClick={decreaseNumber}>-</button>
			<button onClick={increaseNumber}>+</button>
		</>
	);
};

export default App;
```

##### Example 2

```javascript
import React, { useState } from 'react';

import './App.css';

const CheckBox = () => {
	const [checked, setChecked] = useState(false);

	return (
		<>
			<input
				type='checkbox'
				value={checked}
				onChange={() => setChecked((checked) => !checked)}
			/>
			{checked ? 'checked' : 'not checked'}
		</>
	);
};

const App = () => {
	return <CheckBox />;
};

export default App;
```

#### useEffect

##### Data fetching example

**App.js**

```javascript
import React from 'react';

import './App.css';
import User from './components/User';

const App = () => {
	return (
		<div className='app'>
			<User login='mojombo' />
		</div>
	);
};

export default App;
```

**User.js**

```javascript
import React, { useEffect, useState } from 'react';

const User = ({ login }) => {
	const [data, setData] = useState(null);

	useEffect(() => {
		fetch(`https://api.github.com/users/${login}`)
			.then((res) => res.json())
			.then(setData)
			.catch(console.error);
	}, [login]);

	if (data) {
		return (
			<div>
				<h1>{data.login}</h1>
				<img width='200px' src={data.avatar_url} alt='user profile' />
			</div>
		);
	}

	return null;
};

export default User;
```

##### Manually update DOM example

**Without using useEffect**

```javascript
import React, { useState } from 'react';

const App = () => {
	const [count, setCount] = useState(0);

	return (
		<div>
			<p>You clicked {count} times</p>
			<button
				onClick={() => {
					setCount(count + 1);
					document.title = `You clicked ${count} times`;
				}}
			>
				Click me
			</button>
		</div>
	);
};

export default App;
```

![result](/src/assets/images/useEffect1.png)

**Using useEffect**

```javascript
import React, { useState, useEffect } from 'react';

const App = () => {
	const [count, setCount] = useState(0);

	useEffect(() => {
		document.title = `You clicked ${count} times`;
	});

	return (
		<div>
			<p>You clicked {count} times</p>
			<button
				onClick={() => {
					setCount(count + 1);
				}}
			>
				Click me
			</button>
		</div>
	);
};

export default App;
```

![result](/src/assets/images/useEffect2.png)
