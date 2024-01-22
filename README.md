## Envado

Envado is a lightweight and type-safe Node.js library designed to streamline the validation and retrieval of environment variables. It supports a variety of validation types, including strings, numbers, and booleans.

 <!-- It also provides a convenient way to parse and validate environment variables that contain JSON, URLs, and email addresses. -->

**Key Features**

- Type-safe environment variable validation
- Auto-completion and type-checking
- Dynamic configuration for environment variables
- Lightweight and easy to integrate

**Installation**

```sh
npm i --save-dev envado
```

or

```sh
yarn add -D envado
```

**Usage**

To use the library, make sure you have your `.env` file in the project root directory. Simply call the `envado` function with an object that defines the environment variables that you need to validate and load. For example:

```ts
import envado from "envado";

const evn = envado({
  API_KEY: { type: "string" },
  PORT: { type: "number" },
});
```

### Setting Default value

You can set the default value for the environment, which will be the fallback value when the value in the `.env` is undefined. For example:

```js
const evn = envado({
  PUBLIC_URL: { type: "string" defaultValue: "https://example.com" },
});
```

Envado supports several validation types to ensure that your environment variables have the expected format. Here are examples of how to use each validation type:

### `string`

```ts
const evn = envado({
  API_KEY: { type: "string" },
  JWT_SECRET: {type: "string" },
});

// Access the validated values
const apiKey = evn.API_KEY; // A string
const jwtSecret = evn.JWT_SECRET; // A string
```

### `number`

```js
const evn = envado({
  PORT: "number",
  TIMEOUT: "number",
});

// Access the validated values
const port = evn.PORT; // A number
const timeout = evn.TIMEOUT; // A number
```

### `boolean`

```js
const evn = envado({
  ENABLE_FEATURE: "boolean",
  DEBUG_MODE: "boolean",
});

// Access the validated values
const enableFeature = evn.ENABLE_FEATURE; // A boolean
const debugMode = evn.DEBUG_MODE; // A boolean
```


### `array`

```js
const evn = envado({
  TAGS: { type: "array" },
  IDS: { type: "array" },
});

// Access the validated values
const tags = evn.TAGS; // An array
const ids = evn.IDS; // An array
```

### `object`

```js
const evn = envado({
  USER_PROFILE: { type: "object" },
  SYSTEM_CONFIG: { type: "object" },
});

// Access the validated values
const userProfile = evn.USER_PROFILE; // An object
const systemConfig = evn.SYSTEM_CONFIG; // An object
```

**Validation Types**

The following validation types are supported:

- `string`: Validates that the environment variable is a string.
- `number`: Validates that the environment variable is a number.
- `boolean`: Validates that the environment variable is a boolean.
- `array`: Validates that the environment variable is a valid array.
- `object`: Validates that the environment variable is a valid object.

**Error Handling**

If the `envado` function detects an invalid environment variable, it will throw an error. You can handle these errors however you like. For example, you could log the error and exit the application.

```ts
import envado from "envado";

try {
  // Define the expected environment variables and their types
  const env = envado({
    SECRET_KEY: { type: "string" },
    API_KEY: { type: "string" },
    PORT: { type: "number" },
    DB_PORT: { type: "number" },
  });

  // Access validated environment variables
  const secretKey = env.SECRET_KEY;
  const port = env.PORT;

  console.log(
    "Environment variables have been successfully loaded and validated:"
  );
  console.log("SECRET_KEY:", secretKey);
  console.log("PORT:", port);
} catch (error) {
  // Handle errors that may occur during environment variable validation
  if (error instanceof Error) {
    console.error(
      "An error occurred while loading environment variables:",
      error.message
    );
    // You can choose to gracefully exit the application here or take other appropriate actions.
    process.exit(1); // Exiting the application with an error code.
  } else {
    console.error("An unexpected error occurred.");
  }
}
```

**License**
[MIT](/LICENSE)
