---
id: bd7158d8c443edefaeb5bd0f
title: Microsserviço de metadados de arquivos
challengeType: 4
forumTopicId: 301506
dashedName: file-metadata-microservice
---

# --description--

Crie um aplicativo full stack em JavaScript que seja funcionalmente semelhante a este: <a href="https://file-metadata-microservice.freecodecamp.rocks" target="_blank" rel="noopener noreferrer nofollow">https://file-metadata-microservice.freecodecamp.rocks</a>. Trabalhar nesse projeto vai fazer com que você escreva seu código usando um dos seguintes métodos:

-   Clone <a href="https://github.com/freeCodeCamp/boilerplate-project-filemetadata/" target="_blank" rel="noopener noreferrer nofollow">este repositório do GitHub</a> e complete o projeto localmente.
-   Use <a href="https://replit.com/github/freeCodeCamp/boilerplate-project-filemetadata" target="_blank" rel="noopener noreferrer nofollow">nosso projeto inicial do Replit</a> para completar o projeto.
-   Use um construtor de site de sua escolha para completar o projeto. Certifique-se de incorporar todos os arquivos do nosso repositório no GitHub.

If you use Replit, follow these steps to set up the project:

-   Start by importing the project on Replit.
-   Next, you will see a `.replit` window.
-   Select `Use run command` and click the `Done` button.

When you are done, make sure a working demo of your project is hosted somewhere public. Then submit the URL to it in the `Solution Link` field. Optionally, also submit a link to your project's source code in the `GitHub Link` field.

# --instructions--

**HINT:** You can use the `multer` npm package to handle file uploading.

# --hints--

You should provide your own project, not the example URL.

```js
(getUserInput) => {
  assert(
    !/.*\/file-metadata-microservice\.freecodecamp\.rocks/.test(
      getUserInput('url')
    )
  );
};
```

You can submit a form that includes a file upload.

```js
async (getUserInput) => {
  const site = await fetch(getUserInput('url'));
  const data = await site.text();
  const doc = new DOMParser().parseFromString(data, 'text/html');
  assert(doc.querySelector('input[type="file"]'));
};
```

The form file input field has the `name` attribute set to `upfile`.

```js
async (getUserInput) => {
  const site = await fetch(getUserInput('url'));
  const data = await site.text();
  const doc = new DOMParser().parseFromString(data, 'text/html');
  assert(doc.querySelector('input[name="upfile"]'));
};
```

When you submit a file, you receive the file `name`, `type`, and `size` in bytes within the JSON response.

```js
async (getUserInput) => {
  const formData = new FormData();
  const fileData = await fetch(
    'https://cdn.freecodecamp.org/weather-icons/01d.png'
  );
  const file = await fileData.blob();
  formData.append('upfile', file, 'icon');
  const data = await fetch(getUserInput('url') + '/api/fileanalyse', {
    method: 'POST',
    body: formData
  });
  const parsed = await data.json();
  assert.property(parsed, 'size');
  assert.equal(parsed.name, 'icon');
  assert.equal(parsed.type, 'image/png');
};
```

# --solutions--

```js
/**
  Backend challenges don't need solutions, 
  because they would need to be tested against a full working project. 
  Please check our contributing guidelines to learn more.
*/
```
