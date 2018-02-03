---
layout: post
title: Rust For Web Development Part 1
tags: [Rust, nghenglim-open-source]
---

If you ask what is the rising star of programming language, it will be rust for recent year.

## Potential of Rust in Web Development
- Execution Speed 
- No garbage collection (as compared to JAVA or GO web development)
- Build in code safety
- Compile to binary

## Is 2018 the right time to use Rust for web development?
With the asynchronous I/O libraries of Rust is mostly ready, Rust can  serve web traffic without being I/O bound. However, the only downside is that framework is not mature yet.

## Top Web Development Framework For Rust
- Iron: Not much investigate into it, but seems like not as maintained as Rocket
- Rocket: Currently(0.3.6) is build on synchronous HTTP backend. Provide higher level of abstraction however has less control on what you can do.
- Hyper: Hyper(0.11) is multithreaded asynchronous low-level typesafe abstraction over raw HTTP. However the example on it is not much and too low-level.

## Time for Develop a new Framework?
Well I actually think making a wrapper on top of Hyper will be good enough! I currently name it as [Hyperap](https://github.com/nghenglim/hyperap) and published it to [Github](https://github.com/nghenglim/hyperap)! Have not publish to crates.io yet because I have some issue login into it.

The code is still in development, I plan to use it as the main framework for my pet project.

## Example Usage
To test it (assumed you have rust cargo installed)
~~~bash
git clone https://github.com/nghenglim/hyperap
cd hyperap && cargo run
~~~
~~~rs
extern crate hyperap;
use hyperap::hyper::server::{Response};
use hyperap::hyper::{Method};
use hyperap::server::{HyperApp, Middleware, MiddlewareParam};
use hyperap::response::{resp};

fn get_static(_a: MiddlewareResult) -> Response {
    hyperap::server::static_file("Cargo.toml")
}
fn hello_world(a: MiddlewareResult) -> Response {
    resp(a.hello.clone() + " at path " + &a.path)
}
fn not_found_route(a: MiddlewareResult) -> Response {
    resp("not found route at path ".to_owned() + &a.path)
}
pub struct App {
    pub hello: String,
}
pub struct MiddlewareResult {
    path: String,
    pub hello: String,
}
#[derive(Clone)]
pub struct RouteDefinition {
    parameters: Vec<RouteDefinitionParameters>
}
#[derive(Clone)]
pub struct RouteDefinitionParameters {
    _in: String,
    _name: String,
}
impl Middleware for App {
    type M = MiddlewareResult;
    type R = RouteDefinition;
    fn middleware(&self, p: MiddlewareParam<MiddlewareResult, Self::R>) -> Response {
        let m = MiddlewareResult {
            path: p.req.path().to_owned(),
            hello: self.hello.clone(),
        };
        (p.func)(m)
    }
}
fn main() {
    let the_app = App {
        hello: "Hello World".to_owned(),
    };
    let mut app = HyperApp::new(the_app);
    app.open_browser(true);
    app.set_default_route(not_found_route);
    app.add_route(Method::Get, "/static", get_static, vec![RouteDefinition {
        parameters: vec![RouteDefinitionParameters {
            _in: "query".to_owned(),
            _name: "offset".to_owned(),
        }]
    }]);
    app.add_pure_route(Method::Get, "/", hello_world);
    app.port(3000);
    app.run();
}
~~~

## Other critical part in web development
- ORM: with feature similar to [Sequelize](https://github.com/sequelize/sequelize)
- Query builder
There seems to be some libraries for it, however coming from NodeJS, the feature that these libraries just cannot fulfill my need.

I'm currently working on making a rust ORM library. However most probably will remain as my private repo unless a lot of people interested on it.