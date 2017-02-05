---
layout: post
title: Introduce FawkesJs
tags: [NodeJS, nghenglim-open-source]
---

It has been awhile since I have been inactive in open-source world. Although nowadays trend is in VR, AI and iOT, API development is still needed.

[FawkesJs](https://github.com/fawkesjs/fawkesjs) is a Javascript framework that is built on top of express, typescript and MVC structure. Inspired from Laravel and Loopback, the target of the framework is to make Javascript development even easier.

## Build in structure in this project
- Express
- Sequelize
- Typescript
- Swagger: use `fawkesjs -s ./swagger/swagger.json` to generate swagger document
- Express Rest Param Validation: integration with swagger document generation
- Acl (inside `fawkesjs-starter/src/module`)
- AccessToken (inside `fawkesjs-starter/src/module`)

## Why FawkesJs
- NodeJS has good async support that PHP lack of
- Laravel is the first choice in PHP, however NodeJS is still full of framework choices
- Express in NodeJS is good, however its too minimalist.
- Loopback is good, however personally I think Laravel structure is somehow better than Loopback - more organized
- With Typescript, we can have better type checking during development time. Convenient to develop with atom
- Name is just a symbol, its so hard to come out with a good naming
- Rust seems promising, however I'm still waiting for Hyper to implement async IO.

## Usage
- git clone https://github.com/fawkesjs/fawkesjs-starter
- follow the README
