[![npm version](https://badge.fury.io/js/redisgraph.js.svg)](https://badge.fury.io/js/redisgraph.js)

# redisgraph.js

[RedisGraph](https://github.com/RedisLabsModules/redis-graph/) JavaScript Client

## Overview

### Official Releases


# Example: Using the JavaScript Client

```javascript
let graph = new RedisGraph('social');
graph
.query("CREATE (:person{name:'roi',age:32})")
.then( () => {
	return graph.query("CREATE (:person{name:'amit',age:30})");
})
.then( () => {
	return graph.query("MATCH (a:person), (b:person) WHERE (a.name = 'roi' AND b.name='amit') CREATE (a)-[knows]->(a)")
})
.then( () => {
	return graph.query("MATCH (a:person)-[knows]->(:person) RETURN a")
})
.then( (res) => {
	while(res.hasNext()){
		let record = res.next();
		console.log(record.getString('a.name'));
	}
	console.log(res.getStatistics().queryExecutionTime());
});

```

## Running tests

A simple test suite is provided, and can be run with:

```sh
$ mocha
```

The tests expect a Redis server with the RedisGraph module loaded to be available at localhost:6379

## License

redisgraph.js is distributed under the BSD3 license - see [LICENSE](LICENSE)

[npm-image]: https://img.shields.io/npm/v/express.svg
[npm-url]: https://npmjs.org/package/redisgraph.js
