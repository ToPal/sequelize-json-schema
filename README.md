# sequelize-json-schema

[![NPM Version](https://img.shields.io/npm/v/sequelize-json-schema.svg)](https://npmjs.org/package/sequelize-json-schema)
[![CircleCI](https://circleci.com/gh/chaliy/sequelize-json-schema.svg?style=svg)](https://circleci.com/gh/chaliy/sequelize-json-schema)

Use your Sequelize models in JSON Schemas or Swagger

Main use case for this code is to generate models for hand crafted swagger.json.

## Installation

This is a [Node.js](https://nodejs.org/en/) module available through the
[npm registry](https://www.npmjs.com/). Installation is done using the
[`npm install` command](https://docs.npmjs.com/getting-started/installing-npm-packages-locally):

```bash
$ npm install sequelize-json-schema
```


## Example

```
let Simple = sequelize.define('simple', {
  title: Sequelize.STRING,
  description: Sequelize.TEXT
});

let def = definition(Simple);

console.log(def);
```

And result will be:

```
{
  type: 'object',
  properties: {
    id: {
      type: 'integer',
      format: 'int32'
    },
    title: { type: 'string' },
    description: { type: 'string' },
    createdAt: {
      type: 'string',
      format: 'date-time'
    },
    updatedAt: {
      type: 'string',
      format: 'date-time'
    }
  }
}
```

## Using with Swagger

This tool generates `definitions` part of the Swagger Manifest. So if you have Swagger definition for your API just extend `definitions` with JSON generated by this tool.

```
{
  "swagger": "2.0",
  "info": {
    "title": "API",
    "version": "1.0.0"
  },
  "paths": {
    "simple": {
      "get": {      
        "parameters": [ ],
        "responses": {
          "200": { "$ref": "#/definitions/simple" }
        }
      }
    }
  },
  "definitions": {
    "simple": {
      type: 'object',
      properties: {
        id: {
          type: 'integer',
          format: 'int32'
        },
        title: { type: 'string' },
        description: { type: 'string' },
        createdAt: {
          type: 'string',
          format: 'date-time'
        },
        updatedAt: {
          type: 'string',
          format: 'date-time'
        }
      }
    }
  }
}
```

## LICENSE

[MIT License](http://en.wikipedia.org/wiki/MIT_License)
