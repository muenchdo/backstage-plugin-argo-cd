# Argo CD Plugin for Backstage

![](./docs/argo-cd-plugin.png)

[https://roadie.io/backstage/plugins/argo-cd](https://roadie.io/backstage/plugins/argo-cd)

## Features

- 

## How to add argo-cd project dependency to Backstage app

If you have your own backstage application without this plugin, here it's how to add it:

1. In the `backstage/packages/app` project add the plugin as a `package.json` dependency:

```bash
yarn add @roadiehq/backstage-plugin-argo-cd
```

2. add argo-cd to the proxy object in `app-config.yaml` file in the root directory:

```yml
proxy:

  ...

  '/argocd/api':
    # url to the api of your hosted argoCD instance
    target: https://159.65.209.132/api/v1/
    changeOrigin: true
    # this line is required if your hosted argoCD instance has self-signed certificate
    secure: false
    headers:
      Cookie:
        $env: ARGOCD_AUTH_TOKEN


```

3. Add plugin to the list of plugins:

```ts
// packages/app/src/plugins.ts
export { plugin as ArgoCD } from '@roadiehq/backstage-plugin-argo-cd';
```

4. Add plugin to the `entitytPage.tsx` source file:

```tsx
```

## How to use Argo-cd plugin in Backstage

The Argo CD plugin is a part of the Backstage sample app. To start using it for your component, you have to:

1. Add an annotation to the YAML config file of a component. If there is only a single Argo CD application for the component, you can use
    ```yml
    argo-cd/app-name: <app-name>
    ```
    You can also use labels to select multiple Argo CD applications for a component:
    ```yml
    argo-cd/app-selector: <app-selector>
    ```
    **Note:** You can only use one of the options per component.

1. Add your auth key to the environmental variables for your backstage backend server (you can acquire it by sending a GET HTTP request to Argo CD's `/session` endpoint with username and password):
    ```
    ARGOCD_AUTH_TOKEN="argocd.token=<auth-token>"
    ```
## Develop plugin locally

You can clone the plugin repo into the `plugins/` directory:

```sh
git clone https://github.com/RoadieHQ/backstage-plugin-argo-cd.git argo-cd
```

and run `yarn` in the root backstage directory - it will create a symbolic link so the dependency will be provided from the source code instead of node_modules package.

## Links

- [Backstage](https://backstage.io)
- [Further instructons](https://roadie.io/backstage/plugins/argo-cd/)
- Get hosted, managed Backstage for your company: https://roadie.io
