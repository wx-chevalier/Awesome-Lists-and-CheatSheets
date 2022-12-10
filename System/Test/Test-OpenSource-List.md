# Quality Assurance OpenSource List

# Platform

- [Metersphere #Project#](https://github.com/metersphere/metersphere): An open source continuous testing platform. MeterSphere 是一站式的开源企业级持续测试平台，涵盖测试跟踪、接口测试、性能测试、团队协作等功能，全面兼容 JMeter、Postman 等开源、主流标准。

- [Gauge #Project#](https://github.com/getgauge/gauge): Gauge is a light weight cross-platform test automation tool. It provides the ability to author test cases in the business language.

- [Karate #Project#](https://github.com/intuit/karate): Karate is the only open-source tool to combine API test-automation, mocks, performance-testing and even UI automation into a single, unified framework. The BDD syntax popularized by Cucumber is language-neutral, and easy for even non-programmers. Powerful JSON & XML assertions are built-in, and you can run tests in parallel for speed.

# API Test

- [Mock.js #Project#](http://mockjs.com/): 生成随机数据，拦截 Ajax 请求

- [Step CI #Project#](https://github.com/stepci/stepci): Step CI is an open-source tool, which helps you automate API testing and monitoring.

- [Prism #Project#](https://github.com/stoplightio/prism): Turn any OpenAPI2/3 and Postman Collection file into an API server with mocking, transformations and validations.

- [newman #Project#](https://github.com/postmanlabs/newman): Manage all of your organization's APIs in Postman, with the industry's most complete API development environment.

- [HttpRunner #Project#](https://github.com/httprunner/httprunner): HttpRunner 是一个开源的 API 测试工具，支持 HTTP(S) / HTTP2 / WebSocket / RPC 等网络协议，涵盖接口测试、性能测试、数字体验监测等测试类型。简单易用，功能强大，具有丰富的插件化机制和高度的可扩展能力。

- [Hurl #Project#](https://github.com/Orange-OpenSource/hurl): Hurl is a command line tool that runs HTTP requests defined in a simple plain text format.

## Load Testing

- [wrk #Project#](https://github.com/wg/wrk): wrk is a modern HTTP benchmarking tool capable of generating significant load when run on a single multi-core CPU.

- [Webbench #Project#](https://github.com/EZLippi/WebBench): Webbench 是 Radim Kolar 在 1997 年写的一个在 linux 下使用的非常简单的网站压测工具。它使用 fork() 模拟多个客户端同时访问我们设定的 URL，测试网站在压力下工作的性能，最多可以模拟 3 万个并发连接去测试网站的负载能力。

- [Vegeta #Project#](https://github.com/tsenart/vegeta): HTTP load testing tool and library. It's over 9000!

- [Locust #Project#](https://github.com/locustio/locust): Scalable user load testing tool written in Python

- [k6 #Project#](https://github.com/loadimpact/k6): k6 is a modern load testing tool, building on Load Impact's years of experience. It provides a clean, approachable scripting API, distributed and cloud execution, and orchestration via a REST API.

- [plow #Project#](https://github.com/six-ddc/plow): A high-performance HTTP benchmarking tool with real-time web UI and terminal displaying.

## Fuzz & Diff

- [Twitter-Diffy #Project#](https://github.com/twitter/diffy): 比较新老系统之间服务差异

- [FuzzBench #Project#](https://github.com/google/fuzzbench): FuzzBench is a free service that evaluates fuzzers on a wide variety of real-world benchmarks, at Google scale.

# Mock

## Data Generator

- [faker.js #Project#](https://github.com/Marak/faker.js): Generate massive amounts of realistic fake data in Node.js and the browser.

- [sysbench 0.5 性能测试工具使用手册](http://blog.csdn.net/clh604/article/details/12108477)

- [open-source-database-testing-tools](http://www.softwaretestingmagazine.com/tools/open-source-database-testing-tools/)

- [big-list-of-naughty-strings](https://github.com/minimaxir/big-list-of-naughty-strings/)

# Database

- [open-source-database-testing-tools](http://www.softwaretestingmagazine.com/tools/open-source-database-testing-tools/)

- [TPC-DS #Project#](http://www.tpc.org/tpcds/): The TPC Benchmark DS (TPC-DS) is a decision support benchmark that models several generally applicable aspects of a decision support system, including queries and data maintenance.

- [Great Expectations #Project#](https://github.com/great-expectations/great_expectations): Great Expectations helps data teams eliminate pipeline debt, through data testing, documentation, and profiling.

# System Test

- [fio #Project#](https://github.com/axboe/fio): Hence I needed a tool that would be able to simulate a given IO workload without resorting to writing a tailored test case again and again.

# Chaos Engineering

- [Jepsen #Project#](https://github.com/jepsen-io/jepsen): A framework for distributed systems verification, with fault injection.

- [ChaosBlade #Project#](https://github.com/chaosblade-io): ChaosBlade 是一款遵循混沌工程实验原理，提供丰富故障场景实现，帮助分布式系统提升容错性和可恢复性的混沌工程工具，可实现底层故障的注入，特点是操作简洁、无侵入、扩展性强。

- [Chaos Mesh #Project#](https://github.com/pingcap/chaos-mesh): Chaos Mesh is a cloud-native Chaos Engineering platform that orchestrates chaos on Kubernetes environments.

- [Pumba #Project#](https://github.com/alexei-led/pumba): Chaos testing, network emulation and stress testing tool for containers.

- [Litmus #Project#](https://litmuschaos.io/): Chaos engineering is fundamental to increasing the resilience of today’s cloud native, highly dynamic applications and infrastructure. Kubernetes developers and SREs use Litmus to create, manage and monitor chaos workflows by extending Kubernetes itself.

# E2E Test | 端到端测试

## Web App

- [Cypress #Project#](https://github.com/cypress-io/cypress): Fast, easy and reliable testing for anything that runs in a browser.

- [Wraith #Project#](https://github.com/bbc-news/wraith): A responsive screenshot comparison tool.

- [Gremlins.js #Project#](https://github.com/marmelab/gremlins.js): Monkey testing library for web apps and Node.js.

### Cross Browser Test | 跨浏览器测试

- [Airtap #Project#](https://github.com/airtap/airtap): Airtap is an easy way to test your JavaScript in browsers, using a TAP-producing harness like tap or tape.

## Mobile App

- [Auto.js #Project#](https://github.com/hyb1996/Auto.js): A UiAutomator on android, does not need root access(安卓平台上的 JavaScript 自动化工具)

## Acceptance Test | 接受度测试

- [CodeceptJS #Project#](https://github.com/codeception/codeceptjs/): CodeceptJS is a new testing framework for end-to-end testing with WebDriver (or others). It abstracts browser interaction to simple steps which is written from a user perspective.

- [Capybara #Project#](https://github.com/teamcapybara/capybara): Capybara helps you test web applications by simulating how a real user would interact with your app. It is agnostic about the driver running your tests and comes with Rack::Test and Selenium support built in. WebKit is supported through an external gem.

## Page Comparison | 界面比较

- [Blink-Diff #Project#](https://github.com/yahoo/blink-diff): A lightweight image comparison tool.

- [Gemini #Project#](https://github.com/gemini-testing/gemini): Gemini is a utility for regression testing the visual appearance of web pages.

- [PhantomCSS #Project#](https://github.com/Huddle/PhantomCSS): CSS regression testing.

- [garris/BackstopJS #Project# ![star](https://img.shields.io/github/stars/garris/BackstopJS) ](https://github.com/garris/BackstopJS): BackstopJS automates visual regression testing of your responsive web UI by comparing DOM screenshots over time.
