# node-chatgpt-api

Connect a Node.js application to ChatGPT or try prompts from the terminal. This JavaScript ChatGPT API client provides module access, a REST API server, and a CLI, with experimental Bing AI support.

## Features

- Send prompts through the official OpenAI API with `ChatGPTClient`.
- Set the model through `modelOptions.model` and supply system instructions through `promptPrefix`.
- Access the clients from JavaScript, a REST API server, or a CLI.
- Try Bing conversations through the experimental `BingAIClient` module.

**Provider access can change.** The donor documentation describes integrations from 2023; historical model names, pricing, and unofficial access methods should not be treated as current guarantees. Official OpenAI API requests require credentials and may incur charges.

## Installation

Install the package in your Node.js project:

```sh
npm install node-chatgpt-api
```

For a source checkout, install dependencies from the repository directory with `npm install`.

To download the standalone project's release archive, replace `OWNER` with its GitHub owner. This URL assumes the repository has published a `v0.1.0` release:

```sh
curl -fL https://github.com/OWNER/node-chatgpt-api/archive/refs/tags/v0.1.0.tar.gz -o node-chatgpt-api-v0.1.0.tar.gz
```

## Usage

Save this module example as `node-chatgpt-api.mjs`. It reads credentials and a model name from the environment, then sends the prompt supplied on the command line.

```js
import { ChatGPTClient } from 'node-chatgpt-api';

const prompt = process.argv[2];
const apiKey = process.env.OPENAI_API_KEY;
const model = process.env.OPENAI_MODEL;

if (!apiKey || !model || !prompt) {
  console.error(
    'Set OPENAI_API_KEY and OPENAI_MODEL, then pass a prompt as the first argument.'
  );
  process.exit(1);
}

const client = new ChatGPTClient(apiKey, {
  modelOptions: { model },
});

try {
  const result = await client.sendMessage(prompt);
  console.log(result.response);
} catch (error) {
  console.error(error.message);
  process.exitCode = 1;
}
```

Choose a model supported by your account and this client's API implementation:

```sh
export OPENAI_API_KEY='your-api-key'
export OPENAI_MODEL='your-supported-model'
node node-chatgpt-api.mjs 'Explain HTTP keep-alive in two sentences.'
```

Keep API keys out of source control. Unofficial browser or reverse-proxy integrations carry additional account and credential risks; a third-party proxy can receive the tokens you send through it.

## License

MIT. This standalone project is based on [waylaidwanderer/node-chatgpt-api](https://github.com/waylaidwanderer/node-chatgpt-api). Retain the original copyright notice and MIT permission notice when redistributing its code or substantial portions of it.

## Related projects

Other tools from the same author are listed below. Their functionality was not included in the supplied project information; consult each repository for its scope and usage.

- [layeronestudio1-a11y/ratel-doc](https://github.com/layeronestudio1-a11y/ratel-doc): See the repository for documentation and usage details.
- [boostlyapi/seagull](https://github.com/boostlyapi/seagull): See the repository for documentation and usage details.
- [Songraf/stagerag](https://github.com/Songraf/stagerag): See the repository for documentation and usage details.

