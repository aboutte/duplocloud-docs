---
description: >-
  Ensuring continuous integration, delivery, and deployment of your Cloud
  applications
---

# Introduction to CI/CD

DuploCloud supports nearly all available CI/CD platforms, including some of the most popular such as GitLab Actions, CircleCI, and GitLab. This ease of supportability is due to the fact that  DuploCloud views CI/CD platforms agnostically, using [cURL commands](https://en.wikipedia.org/wiki/CURL) to communicate requests.

In addition to third-party CI/CD products, DuploCloud provides [Katkit](katkit/), a built-in CI/CD platform that allows you to build, test, and deploy your application from GitHub commits and pull requests. Katkit is an arbitrary code execution engine that allows you to run any code before and after deployment. Conforming to DuploCloud's architecture, Katkit uses [Tenants](../getting-started/application-focussed-interface/tenant.md), tying together CI and CD.&#x20;

Some of the CI/CD toolchains that are directly supported by DuploCloud include, but are not limited, to the following:

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>GitHub Actions</strong></td><td>Documentation guides for getting started using CI/CD with GitHub Actions</td><td><a href="github-actions/">github-actions</a></td></tr><tr><td><strong>CircleCI</strong></td><td>Documentation guides for getting started using CI/CD with CircleCI</td><td><a href="circleci/">circleci</a></td></tr><tr><td><strong>GitLab CI/CD</strong></td><td>Documentation guides for getting started using CI/CD with GitLab CI/CD</td><td><a href="gitlab-ci-cd/">gitlab-ci-cd</a></td></tr><tr><td><strong>Katkit</strong></td><td>Documentation guides for getting started using CI/CD with Katkit</td><td><a href="katkit/">katkit</a></td></tr></tbody></table>



