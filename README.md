# Ethereum Beacon APIs

![CI](https://github.com/ethereum/beacon-APIs/workflows/CI/badge.svg)

Collection of RESTful APIs provided by Ethereum Beacon nodes

API browser: [https://ethereum.github.io/beacon-APIs/](https://ethereum.github.io/beacon-APIs/)

## Outline

This document outlines an application programming interface (API) which is exposed by a beacon node implementation
 which aims to facilitate [Phase 0](https://github.com/ethereum/eth2.0-specs#phase-0) of the Etheruem consensus layer.

The API is a REST interface, accessed via HTTP. The API should not, unless protected by additional security layers, be exposed to the public Internet as the API includes multiple endpoints which could open your node to denial-of-service (DoS) attacks through endpoints triggering heavy processing.
 Currently, the only supported return data type is JSON.

The beacon node (BN) maintains the state of the beacon chain by communicating with other beacon nodes in the Ethereum network.
Conceptually, it does not maintain keypairs that participate with the beacon chain.

The validator client (VC) is a conceptually separate entity which utilizes private keys 
to perform validator related tasks, called "duties", on the beacon chain.
 These duties include the production of beacon blocks and signing of attestations.

The goal of this specification is to promote interoperability between various beacon node implementations.

## Render 
To render spec in browser you will need any http server to load `index.html` file
in root of the repo.

##### Python
```
python -m SimpleHTTPServer 8080
```
And api spec will render on [http://localhost:8080](http://localhost:8080).

##### NodeJs
```
npm install simplehttpserver -g

# OR

yarn global add simplehttpserver

simplehttpserver
```
And api spec will render on [http://localhost:8000](http://localhost:8000).

### Usage

Local changes will be observable if "dev" is selected in the "Select a definition" drop-down in the web UI.

Users may need to tick the "Disable Cache" box in their browser's developer tools to see changes after modifying the source. 

## Contributing
Api spec is checked for lint errors before merge. 

To run lint locally, install linter with
```
npm install -g @stoplight/spectral-cli@6.2.1

# OR

yarn global add @stoplight/spectral-cli@6.2.1
```
and run lint with
```
spectral lint beacon-node-oapi.yaml 
```

## Implementations

- [TypeScript Wrapper](https://www.npmjs.com/package/@chainsafe/eth2.0-api-wrapper)

https://www.npmjs.com/package/@chainsafe/eth2.0-api-wrapper
## Releasing

1. Create and push tag

   - Make sure info.version in beacon-node-oapi.yaml file is updated before tagging.
   - CD will create github release and upload bundled spec file
   
2. Add release entrypoint in index.html

In SwaggerUIBundle configuration (inside index.html file), add another entry in "urls" field (SwaggerUI will load first item as default).
Entry should be in following format(replace `<tag>` with real tag name from step 1.):
```javascript
         {url: "https://github.com/ethereum/beacon-APIs/releases/download/<tag>/beacon-node-oapi.yaml", name: "<tag>"},
```
