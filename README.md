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

### State

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
