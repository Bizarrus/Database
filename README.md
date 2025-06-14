# Database
Node.js Database Wrapper

# Installation
> `npm install --save datastorages`

# Usage
**config.json**
```json
{
	"Database": {
		"HOSTNAME":		"localhost",
		"PORT":			3306,
		"CONNECTIONS":		5,
		"DATABASE":		"<Database>",
		"USERNAME":		"<User>",
		"PASSWORD":		"<Password>",
		"PREFIX":		"tbl_",
		"CHARSET":		"utf8mb4"
	},
	"Logging": {
		"MYSQL":	false
	}
}
```

**Script**
```javascript
import Config from './config.json' with { type: 'json' };
import Database from 'datastorages';

Database.setConfig(Config);

/* Examples */
console.log('Current Time:', Database.now());

Database.single('SELECT * FROM `table` WHERE `row`=:name', {
	name: 'Test'
}).then((result) => {
	console.log(result);
});

Database.fetch('SELECT * FROM `table` WHERE `row`=:name', {
	name: 'Test'
}).then((results) => {
	results.forEach((result) => {
		console.log(result);
	});
});

let id = await Database.insert('table', {
	id: null,
	name: 'Test',
	time_now: 'NOW()',
	time_whatever: Database.now()
});
console.log('Inserted with ID:', id);

Database.update('table', [ 'name' ], {
	name: 'Test',
	id: 1
});
```
